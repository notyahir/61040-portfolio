# Assignment 2

## Exercise 1: Reading A Concept - Gift Registration

1. Invariants: 
    - Request Count: All purchases made for a corresponding request item (P), must not exceed the request's original count (R). Essentially, for a request, P <= R.
    - Request-Purchase: Every purchase made must be connected/tied to an existing request in the registry. (Relevancy)

    The Request Count invariant might be more important because if it is broken, then purchases will be made for items that are already bought leading to duplicate redundant gifts.

    The action affected by this invariant the most is the purchase action. It preserves this invariant since it requires enough count in the request to allow for a purchase, and then decrementing it after a purchase

2. Fixing an action: 
    - Concurrency Issue: purchase can break the invariant if two gifters purchase at the same when the request count is 1. If it is done at the same time, the system can register the two purchases, and the count will drop to -1 breaking the Request Count. 
    0 <= R - P. The purchases must not exceed the request count otherwise we go to -1 breaking the invariant. Can use atomic actions to fix

    - When concurrency isn't an issue, removeItem can also break the Count/Request-Purchase invariant! This is because if gifters purchase a gift for a recipient, but then a recipient removes an item. The gifts initially purchased are now redundant! The count of R is now less than P also! Not good! To fix this, we REQUIRE removeItem to ensure that there are no purchases of the item beforehand.

3. Inferring behavior:
    - A behavior is that we are able to open and close a registry repeatedly. The spec of the concept only mentions the use of toggling whether it is open/close (through an active bool/enum/flag maybe) but not that it must occur ONLY once! As a result, this gives user flexibility in being able to temporarily pause (close) their registry and reactivate (open) whenever needed.

4. Registry deletion:
    - There is no specific delete action for a registry. This doesn't really matter because closed registries remain inactive and "archived". This can be good for purchase history and references, however, it could take up a lot of storage over time which is an issue for the companies. Deletion could be good for data cleanup!

5. Queries:
    - Owner: Show me list of purchases alongside who purchased the requested items (and how many of each).
    - Gifter: Show me list of requested items in active registry that are available to purchase

6. Hiding purchases: 
    - Introduce a hide (or call it "surprise") bool/enum/flag to the registry that when active, the recipient cannot see purchases until the registry is closed. Purchases are recorded as usual, however, if hide is active, the recipient has the purchase hidden until registry is closed.

7. Generic types:
    - If we define these concepts as generic parameters, we keep them independent of whatever representation may be used. This makes it more reusable and avoids irrelevant details in the concept. This is preferable, as an Item can be represented in different formats which includes SKU codes, which is good since representations might vary across systems (different pricing, descriptions, etc.)

## Exercise 2: Extending A Familiar Concept

1. Defining the concept state

    state:
    - a set of Users with:
        - a username String
        - a password String  

2. requires/effects for actions

    actions:
    - register (username: String, password: String): (user: User)
        - requires no user exists with the username string
        - effects: create a new user with the username and password which is returned
    - authenticate (username: String, password: String): (user: User)
        - requires: a user exists with this username, and corresponding user password equals inputted password
        - effects: return that user 

3. essential invariant must hold
    - Usernames must be unique across all users! It is preserved through register as it requires a unique username when signing up by checking if a user already exists with that username. authenticate does not mutate a state, thus our invariant is preserved

4. confirmation of email functionality

PasswordAuthentication

    concept: PasswordAuthentication

    purpose: limit access to known users

    principle: after a user registers with a username and a password,
    they can authenticate with that same username and password
    and be treated each time as the same user
    
    state:
    - a set of Users with:
        - a username String
        - a password String
        - an email   String

    - a set of pendingRegistrations with:
        - a username String
        - a password String
        - an email   String
        - a token    String

    Note: Not entirely sure if a new state is entirely needed but to handle how emails are handled and confirmed, we add a new state that holds the email as well so we can know where to route the token to securely. Good to have the additional email parameter on a user too just in case they forget password.
        
    actions:
    - register (username: String, password: String, email: String): (token: String)
        - requires no user exists with this username and no pending registration exists
        - effects create a PendingRegistration with given fields and a token which is sent to user email, returns token
    - confirm  (username: String, token: String) (user: User)
        - requires a PendingRegistration exists for username (names match) with a matching token
        - effects remove the pendingRegistration, create a user with username and password, returns user
    - authenticate (username: String, password: String): (user: User)
        - requires: a user exists with this username, and corresponding user password equals inputted password
        - effects:  return that user

## Exercise 3: Comparing Concepts

PAT Specification

    concept: PersonalAccessToken

    purpose: provide an alternative for authenticating users rather than passwords, with the ability to generate, manage, and revoke (delete) access tokens

    principle: users generate one or more tokens, which can then be used as authentication rather than a password, and any mutations to a token does not affect the user's password

    state:
    - a set of Tokens with:
        - a username String
        - a token  String

    actions:
    - generate(owner: User) (token: Token)
        - requires user exists
        - effects create a new token, token returned
    - delete(token: Token)
        - requires token exists
        - effects delete the token
    - authenticate(username: String, token: Token): (user: User)
        - requires user exists with username and token is a match
        - effects return that user 

### Passwords vs. Personal Access Tokens

The difference between Passwords versus PATs is:
-  A user may only have one password but multiple PATs
-  Tokens can be revoked individually without losing account access whereas passwords affect access entirely.

GitHub says "treat your access tokens like passwords" but doesn't explain differences so it would be helpful if they explicitly state why tokens exist (creating multiple access tokens and revoking) and perhaps what intended uses could be. In my experience, I've always used PATs for programming which could be emphasized for non-programmers (to streamline simplicity).

## Exercise 4: Defining Familiar Concepts

1. URL Shortener

Concept #1

    concept: URLShortener

    purpose: Map long URLs to short URLs for easier sharing, readability, and use

    principle: A user submits a long URL with choice of user-defined suffixes, which the module then generates a shortened URL (randomly), where the short URL redirects them to the original long URL.

    state
        a set of URLs pairs with
            - an original URL String
            - a shortened URL String
    actions:
        - shorten(url: String): (newURL: String)
            - requires: a valid URL
            - effects: generates (and returns) a new uncollided shortened URL which is added to our set of URL pairs
        - userShorten(url: String, suffix: String): (newURL: String)
            - requires: a short URL doesn't already exist for our suffix
            - effects:  creates and returns a new url from the long url with the suffix 
        - resolve(shortURL String): (longURL: String)
            - requires: that the shortURL exists
            - effects: returns the long (original) URL

    Notes: Initially, I had the idea of assigning shortened URLs to users, but users cannot have URLs that work only for them since the DNS protocol doesn't work that way, so I removed that part to generalize. However, we could use it if we wanted to keep track of which users made what URLs. Collisions should be prevented since we are checking if the user suffix exists already and shorten should handle collisions in itself.
    

2. Electronic Boarding Pass

Concept #2

    concept: EBoardingPass

    purpose: provide traveling passengers an e-boarding pass (stored on a digital device) with updates in real-time

    principle: after checking in, travelers are issued an electronic boarding pass with flight and passenger info

    state:
        - a set of BoardingPass with
            - a passenger String
            - a flight Flight
            - a gate String
            - a departure time String
            - a seat String
            - a status Enumeration

    actions:
        - issue(user: User, flight: Flight): (boardingPass: BoardingPass)
            - requires: a valid booking from the user and user checked in
            - effects: creates a new e-boarding pass, returns the pass
        - update(boardingPass: BoardingPass, gate: String [Optional], departureTime: String [Optional], status: Enum [Optional], seat: String [Optional])
            - requires: pass exists and is not cancelled
            - effects:  update any flight information with updated information (also handles boarded status). If only boarding passed in, then no new info to update
        - cancel(boardingPass: BoardingPass)
            - requires: a boarding pass to exist, and status is active
            - effects:  cancels our boarding pass and sets status to cancelled

    Notes: Since we have to have real-time changes, the state of the boarding HAS to be in sync with airline flight data. Also, multiple boarding passes may exist.

    Note 2: I think Enumeratin might be the best term for status since we can't use bool here (more than 2 possible vals). Bool: [True, False], status: [active, boarded, cancelled]. I also use flag to mean the same thing

3. Conference Room Booking

Concept #3

    concept: ConferenceRoomBooking

    purpose: Allow users to reserve conference rooms for specific times, while ensuring no collisions (double-booking).

    principle: a user selects a room and time from available non-overlapped slots, and has a booking created if valid, which the user can choose to cancel later

    state:
        - a set of Bookings with 
            - an organizer User
            - a room Room
            - a start time Time
            - an end time  Time

    actions:
        - book(user: User, room: Room, startTime: Time, endTime: Time): (booking: Booking)
            - requires: No previous booking exists already for room and event time. Ensures user doesn't have an overlapping booking
            - effects: creates a booking associated with the room and time, returned
        - cancel(booking: Booking)
            - requires: booking is valid
            - effects: remove booking entirely


    Notes: If we wanted to limit users to 1 booking per user, we can require that no user has a booking already in the book function. We also preserve the invariant of non-overlapping slots by ensuring that no previous booking exists for the same room during that time.