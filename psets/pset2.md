# PSET 2 

## Concepts for URL Shortening

### 1. Contexts

A good way to think about contexts is to think about them as scopes. In what context, does your task need to function? Creating these contexts prevents accidental overlap between unrelated parts of a system. If we were to not have a context for our URL shortener, it would have to ensure uniqueness globally forever! It overloads the URL shortener as the URL shortener concept would have to know domain and DNS structure which violates the separation of concerns.

In short, contexts "scope" uniqueness to a certain level so that something like a nonce can exist across different spaces. 

For our URL shortener, the context will be the domain. This makes nonces (generated strings) unique to each domain, which means different users get to reuse the same suffix and generated strings under different domains without conflicts.

### 2. Storing Used String

The principle of NonceGeneration is each generate returns a string not returned before for that context", the key here is "not returned before for that context". This is a principle that must be held across time, thus, we need to store the set of used strings to ensure we remember so we can reject repeats.

The set of used strings in the specification is going to be exactly equal to the generated strings made each time our counter incremented (when generate was called). Essentially, after n calls, our counter will be at n and we will have generated n strings which is exactly equal to the number of used strings. AF(s) = {s[i]; 0 < i <= n}

### 3. Words As Nonces

From the perspective of the user, an advantage would be memorability & sharability (if you would want to do that). Words are easier to say, remember, and type than just a random string. A disadvantage, however, would be guessability since the string space is reduced to words which makes it easier to brute-force. To combat, longer phrases would have to be used but for the tradeoff of simplicity

WordNonceGeneration

    concept: WordNonceGeneration[Context]

    purpose: generate unique common word strings within a context 

    principle: each generate returns a phrase not returned before for that context

    state:
        a set of Contexts with
            a used set of Strings
            a vocabulary set of Strings

    actions:
        configure(context: Context, vocabulary: Set[Strings])
            effects sets vocabulary for context
        generate(context: Context): (nonce: String)
            requires vocabulary is non-empty
            effects: returns a nonce generated from vocabulary, not in used (not returned before), and adds it to the used set. 

    notes:
        - normalize capitalization
        - could add a filter for profanity? could add opportunity to have phrases

## Synchronizations for URL Shortening

### 1. Partial Matching

generate needs to create a shortened url, thus it will call to NonceGeneration.generate() which only requires the shortUrlBase to do this.  The targetUrl is not needed for this step. However, for register, we must call UrlShortening.register() which requires the nonce, shortUrlBase, and the targetUrl to do this which is why we have targetUrl in that step. In short, targetUrl is irrelevant to nonce generation, no dependency on targetUrl

### 2. Omitting Names

Omitting names is great for brevity and making things more readable/simple. However, you shouldn't do this if you ever need to clarify disambiguities like when you are using an action twice. For example, if we use NonceGeneration.generate() twice so we can use the nonces in different ways, it would become necessary to name the nonces to clarify their use and avoid collisions. Additionally, it would be useful to clarify the name if you are ever passing in a value like a constant 

### 3. Inclusion of Request

The request action is in the first two syncs as it is handling user input captured by the Request.shortenUrl and passing it through the sync.
generate() needs shortUrlBase, register needs targetUrl, nonce, and shortUrlBase which comes from the request. However, the third sync does not deal with the user input but rather the effect of completion of the UrlShortening.register function. We don't need the original request since the purpose of expiry concept is to be applicable to any type of registration, not just the ones that came from a specific type, so we omit the request.

### 4. Fixed domain

**sync** generateFixed  
**when** Request.shortenUrl ()  
**then** NonceGeneration.generate(context: "https://bit.ly/")


**sync** registerFixed  
**when** Request.shortenUrl(targetUrl)
         NonceGeneration.generate(): (nonce)  
**then** UrlShotening.register(shortUrlSuffix: nonce, shortUrlBase: "https://bit.ly/", targetUrl)


**sync** setExpiry  
**when** UrlShortening.register(): (shortUrl)  
**then** ExpiringResource.setExpiry(resource: shortUrl, seconds: 3600)

### 5. Adding a sync

**sync** expire  
**when** ExperingResource.expireResource(): (resource: shortUrl)  
**then** UrlShotening.delete(shortUrl)

**Note**: Here we are deleting the shorturl which we set an expiry on. However, a user could choose to delete a url before the expiry is done. As a result, the expiry can fire even though it is deleted. We can make a requirement that we check if the url exists before issuing the command to expire the resource.

## Extending the Design

### 1. Additional Concepts
Our constraints are to not change any of the existing concepts however we want to add a way of counting the number of accesses to our shortUrl WHICH should only be viewable to the user who registered the shortening (owner). We can divide this idea into two concepts. First, we'll develop a UrlOwnership concept because in order to enforce that it is only viewable to the owner, we need to have an ownership concept to handle this. Second, we need to develop a AccessCount concept to count the accesses. Mixing these together would cause a violation for separation of concerns, there's no reason why AccessCount, a counter idea, should ideas of ownership embedded into it!


**UrlOwnership**

    concept UrlOwnership[User]

    purpose record the user who registered a shortening URL

    principle when a shortening is created, the user who registered that shortening will have ownership, which gives ability to see things such as analytics

    state
        a set of Ownerships with
            a shortUrl String
            a user (owner) User

    actions
        record(shortUrl: String, owner: User)
            requires: no ownership exists for a shortUrl already
            effects: saves the shortUrl to the user who registered the shortened url (owner)
        isOwner (shortUrl: String, requested_user: User): (ownerResult: Boolean)
            effects true if user is owner of the shortUrl, false otherwise
        owner (shortUrl: String) : (owner: User)
            requires that ownership of the shortUrl exists
            effects returns the owner


**AccessCount**
    
    concept AccessCount

    purpose count how many times a url was accessed
    
    principle after an access to a short url, begin a counter if not already made and increment by 1. also readable to see current total
    
    state
        a set of Counters with
            shortUrl String
            count Number
    
    actions
        ensure (shortUrl: string)
            requires no counter exists
            effects creates a counter for shortUrl at 0
        increment (shortUrl: string)
            requires a counter exists for shortUrl
            effect increments count: count = count + 1, count -> count + 1
        read (shortUrl: string): (count: Number)
            requires a counter exists for shortUrl
            effect: returns count

### 2. Three Essential Synchronizations

**sync** createAnalytics  
**when**  
    Request.shortenUrl(owner: User, targetUrl, shortUrlBase)  
    UrlShortening.register(): (shortUrl)  
**then**  
    UrlOwnership.record(shortUrl: owner:User)  
    AccessCounting.ensure(shortUrl)

**sync** countLookup  
**when** UrlShortening.lookup(shortUrl)  
**then** AccessCount.increment(shortUrl)

**sync** viewAnalytics  
**when** UrlOwnership.isOwner(shortUrl, requester: User): (result: True)  
**then** AccessCount.read(shortUrl): (count: Number)

Notes: for viewAnalytics, in order for **then** to fire, the condition for **when** must be TRUE. Enforces that only the owner can see it

### 3. Modularity of our Solution

#### 1. Allowing users to choose their own short URLs

A new concept should not be needed. Instead, we can utilize a sync. We will make a new request where a user can give a desired suffix
Request.chooseShortUrl(owner: User, targetUrl: String, shortUrlBase: String, desiredSuffix: String)

**sync** userChosenUrl  
**when** Request.chooseShortUrl(owner: User, targetUrl: String, shortUrlBase: String, desiredSuffix: String)  
**then** UrlShortening.register(shortUrlSuffix: desiredSuffix, shortUrlBase, targetUrl)

UrlShortening.register will ensure uniqueness. Should work!

#### 2. "Word as Nonce" Strategy

For a word as nonce strategy, we can use the word generation concept from earlier, which we end up routing with syncs. So, if we take our WordNonceGeneration concept, we can develop these syncs.

**sync** wordGenerate  
**when** Request.shortenUrlMemorable(owner: User, targetUrl, shortUrlBase)  
**then** WordNonceGeneration.generate(context: shortUrlBase): (nonce: String)

**sync** wordRegister  
**when**   
    Request.shortenUrlMemorable(owner: User, targetUrl, shortUrlBase)  
    WordNonceGeneration.generate(context: shortUrlBase): (nonce: String)  
**then** UrlShortening.register(nonce: String, shortUrlBase, targetUrl)


#### 3. targetUrl In Analytics

This feature is undesirable because it violates privacy intent as it was described in the requirement where analytics are only viewable to the "user who registered the shortening". Grouping by targetUrl pushes shortUrl aggregation whch risks exposing information from links you didn't create. It also breaks clean modularity since grouping by target forces analytics to depend on UrlShortening

#### 4. Less Guessable Urls

It would be to include this to enhance privacy and reduce any hacker capabilities. It reduces brute-force risks at a low cost without affecting ownership or analytic concepts. To do this, we can modify our NonceGeneration to a more secure form called SecureNonceGeneration that is designed to output less guessable urls which can be done by adding additional contexts. The syncs would be the same but a bit more private.

**sync** generatePrivate  
**when** Request.shortenUrlPrivate(owner, targetUrl, shortUrlBase)  
**then** SecureNonceGeneration.generate(context: shortUrlBase): (nonce: String)

**sync** registerPrivate  
**when**   
    Request.shortenUrlPrivate(owner, targetUrl, shortUrlBase)  
    SecureNonceGeneration.generate(context: shortUrlBase): (nonce: String)  
**then**  UrlShortening.register(nonce: String, shortUrlBase, targetUrl)

#### 5. Support Reporting Analytics to Unregistered Creators

While this feature is definitely possible to implement, it would be undesirable because it violates the main requirement that analytics are supposed to be viewable only by the "user who registered the shortening". If there is no registration, there is no authorized analytics to view. To fix this, it adds significant operational complexity with tokens issuing, expiry, etc. Not only this, but it weakens privacy + control since tokens can be lost or even leaked. While possible, it seems that the tradeoffs are not worth given our initial idea as well.