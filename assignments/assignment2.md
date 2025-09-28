# Assignment 2
## Problem Statement
### Personal Music Listening & Playlist Curation
- Focused on how heavy listeners or users of a music listening service save, revisit, and organize the music they love over time. 
- For me, I am a big lover of music, I specifically use Spotify as my main streaming service. As a result, my liked songs has grown into the thousands, and I know there have been tracks that have slipped from my memory or are tracks on my playlists that just don't fit the vibe anymore, which means old bangers get played less! 
- This is an important domain because "great listening" isn't solely about discovery, but it's also about resurfacing the right songs so that the favorites keep on living, not just aggregating dust
- The goal isn't just about finding new music, it's about reusing old favorites at the right moment. No one wants to sit down and scroll their liked songs every single time just to revisit some old classics!

### "Forgotten Bangers" get buried as libraries grow
- For listeners with a very large "Liked Songs" catalog, great tracks fade from a user's rotation. Perhaps it is because the user no longer enjoys but there are also additional factors contributing to that. Finding them becomes a huge time-sink manually scrolling, and it's not fun when all you're doing is looking at tracks you probably don't even remember. An algorithm such as Tiktok or Instagram Reels would make it fun but that's not what it is.
- Beyond time-sinks, older playlists decay in quality as a user's music taste changes or shifts over time, while there can also be streaming platform issues such as duplicate songs and removed songs.
- While there are recap features such as Spotify Wrapped, it is "retrospective" and the playlist is comprised of only 100 songs from the past year. It doesn't necessarily target continuous resurfacing on a day-to-day level. The result of all this is that users replay fewer older favorites and end up with once-beloved playlists they don't listen to as much anymore as they don't feel "right".

### Stakeholders
- Listener (primary): Heavy music service user with a large music catalog, wants a low-effort way to bring buried favorites and revive old playlists
- Friends/Followers (secondary): Benefit from shared mixes with older classics added
- Platform: Spotify/Apple/music platforms whose APIs, scopes, and rate limits define what’s feasible; furthermore, if users receive older classics, the platform receive additional plays and engagement
- Artists & Label (owners): Content holders who benefit from new plays and streams as tracks resurface.

### The Evidence and Comparables
* [Spotify removes it's 10,000-song library limit](https://www.theverge.com/2020/5/26/21270409/spotify-song-library-limit-removed-music-downloads-playlists-feature) Spotify removing the limit shows how users are running into large, unwieldly libraries.
* [Users share their library sizes](https://www.reddit.com/r/spotify/comments/1j6g2mf/how_many_liked_songs_do_you_have_and_how_long). Demonstrating the need for Spotify to make this change and providing anecdotal evidence of users reaching this limit
* [200 million songs on streaming services](https://www.musicbusinessworldwide.com/there-are-now-more-than-200m-tracks-on-audio-streaming-services-nearly-100m-of-them-attracted-no-more-than-10-plays-each). This demonstrates how the firehose is real and that not only are users discovering new music but the catalog for new music is massive and ever-growing.
* [Users note songs vanishing from liked songs](https://www.narendravardi.com/vanishing-tunes-ten-percent-of-my-liked-songs-disappeared-on-spotify/). Some users ranting about how a percentage of their songs vanish which could be due to license renewal. This causes issues where some users may never know and forget about songs they once loved!
* [Spotify Wrapped](https://support.spotify.com/uk/article/spotify-wrapped/). A recap of a user's listening patterns over the year. Helpful to see statistics about one's listening and can help show songs. The downside is that it is a long process (over a year) and isn't intended for resurfacing songs beyond a year.
* [Spotify Daylist](https://newsroom.spotify.com/2023-09-12/ever-changing-playlist-daylist-music-for-all-day/). A dynamic, mood-titled playlist that refreshes multiple times a day. Curated to a user's vibe but doesn't necessarily tackle the issue of resurfacing old past liked songs. A good fun way of discovering music.

## Application Pitch

### Resurfacer 
Your "Liked Songs" turned into an ocean! Great tracks get buried and old playlists fall apart. Resurfacer brings back your forgotten bangers into rotation and keeps your playlists healthy.
#### Time-Capsule Shuffle
- An auto-mix that favors "slept-on" favorites by scoring each saved track with a "staleness" score (based off how long it's been since you saved it, when you saved it, and how often you've been skipping it), and resurfaces it to try and fit the listener's vibe. One tap saves any resurfaced song to a new fresh playlist
- Why it helps: You get effortless rediscovery instead of needing to endlessly scroll. The mix stays personal and intentionally backward-looking to revive old gems!
- Impact on stakeholders: Listeners replay more of their old favorites, friends get mixes from friends with resurfaced classics, artists & labels see revived streams on older catalogs, and platforms benefit from overall engagement

#### Memory Cards
- A swipeable song card mode for bite-sized resurfacing sessions. A "Tiktok/Tinder" setup where a user can swipe a song if they like it or not! "Keep" boosts a tracks presence in future mixes, "Add" drops it straight into a playlist, and "Snooze" hides it for a while so it doesn't pop up again for a while. Adapts to your feedback over time!
- Why it helps: Reduces decision fatigue and turns a tedious monotonous scrolling hunt into a playful 15-30 second activity that actively works towards rebuilding playlists
- Impact on Stakeholders: Listeners control the pace and vibes through a fun resurfacing session, friends benefit from better mixes, platforms/artists gain listeners, and platforms get engagement but also limit the scope of what is feasible through their API.

#### Playlist Surgery Suggestions
- A health check for any playlist that flags duplicates, removes broken tracks, and even tags specific mood outliers that don't fit the vibe of a playlist anymore. This is possible through one-tap buttons and a visible change log that lets you revert back to certain states!
- Why it helps: Old playlists can come back alive again, keep a "copy" of the original but have a refurbished version, so you can actually reuse them!
- Impact on stakeholders: Listeners get renewed reusable playlists, friends with shared playlists get revitalized updates, artists benefit from tracks being recirculated, and platforms see higher retention/use.

## Concept Design
**Concept 1: Platform Linker**

    concept: PlatformLink

    purpose: Provide authenthicated access to a streaming platform. Give other concepts a safe way of talking to the streaming platform

    principle: Once a user begins using our app, a user will need to be authenticated to their streaming platform. Our only concept that touches token/rate limits. All other concepts making requests with the platform pass it through our platform linker.

    state:
        - a set of Users with
            a username          String
            an email            String
            a timestamp         Float
        - a set of Links with
            a user              User
            a platform          String
            a token_access      String
            a token_refresh     String
            an expiry_timestamp Float
        
    actions:
    - link(user: User, platform: String): (platformLink: Link)
        requires: user exists, platform is valid music platform
        effects: creates and returns a Link

    - refresh(user: User, platform: String, token_refresh: String)
        requires: Link exists for user on platform
        effects: updates token, prolongs expiration
        
    - revoke(user: User, platform: String)
        requires: Link exists
        effects: deletes Link with associated tokens

    - can(user: User, link: Link): (ok: Boolean)
        effects: returns whether a Link has the needed access and availability to do an action on the platform

**Concept 2: Library Tracks and Playlist Grabber**

    concept: LibraryCache

    purpose: Keep a local, queryable snapshot of the user's liked tracks and playlists, metadata, and useful statistics 

    principle: Fetch a user's snapshot that updates every once in a while, and provides information needed for track analysis, scoring, and surgery

    state:
        - a set of Tracks with
            a title       String
            an artist     String
            an available  Boolean
            a tempo       Float [Optional]
            an energy     Float [Optional]
            a valece      Float [Optional]
        - a set of Likes with
            a user        User 
            a track       Track
            a added_at    Float
        - a set of Plays with
            a user        User
            a track       Track
            a last_played Float
        - a set of Playlists with
            a playlist    String
            a set of Tracks
        
    actions:
        - ingest(user: User)
            requires: PlatformLink.can(user, "read-library") = True
            effects: populates Tracks/Likes/Playlists/Plays

        - sync(user: User)
            requires: PlatformLink.can(user, "read-library") = True
            effects: updates Tracks/Likes/Plays/Playlists every so often

        - getLiked(user: User): (tracks: List<{idx: Integer, track: Track}>)
            effects: returns user’s liked tracks

        - getPlaylist(playlist: Playlist): (entries: List<{idx, track}>)
            effects: returns entries

**Concept 3: Track Analyzer and Scorer**

    concept: TrackScoring

    purpose: Compute a score for each track in a user's liked song catalog and get top candidates

    principle: After fetching a user's liked song catalog, we score tracks in the catalog in terms of "staleness" based off the track meta that will aid in resurfacing

    state:
        - a set of Weights with
            a user              User
            a last_playedW      Float
            a liked_whenW       Float
            a times_skippedW    Float
        - a set of Boosts with
            a user              User
            a track             Track
            an amount           Float
            an update_time      Float
        - a set of Snoozes with
            a user              User
            a track             Track
            a snoozed_timestamp Float
        
    actions:  
        - score(user: User, track: Track): (s: Float)
            effects: computes a "staleness" score from a user's statistics and adds it to the weights, returns the score

        - keep(user: User, track: Track)
            effects: Adds a track to the set of boosts or boosts the float amount that decays over time

        - snooze(user: User, track: Track, until: Float [Optional])
            effects: adds a track to the snooze set and keeps it snoozed for 2 weeks unless specified otherwise

**Concept 4: Track Session Swiper**

    concept: SwipeSessions

    purpose: Run lightweight "Memory Card" sessions on tracks! Present different snippets of tracks and record user's decision to keep/snooze/add.

    principle: A user decides to go into Session Swipe mode, this pulls songs from their Liked Song catalog and presents them in a Tiktok/Memory Card format where they can listen to a snippet of a track and swipe left to keep, swipe right to snooze, or swipe up to add the song to a playlist!

    state:
        - a set of Sessions with
            a sessionId     String
            a user          User
            a queue         List<Tracks>
            a started_at    Float
        
    actions:   
        - start()

        - next()

        - keep()

        - snooze()

        - add()

**Concept 5: Playlist Analyzer and Fixer**

    concept: PlaylistHealth

    purpose: Detect duplicate, unavailable, and mood outliers of a user's liked songs or playlists, applies reversible modificatons to the playlists to revive.

    principle: A user can analyze a playlist, which then reports any duplicate songs, unavailable songs, or highlights which songs may no longer fit a user's current vibe. It can calculate from track score but if the user enters an overall theme for a playlist, there is capability for analysis of the overall playlist. Any adjustments made to the playlists can be reversed so a user can retain a "copy" of the original playlist.

    state:
        - a set of Reports with
            a playlist      Playlist
            a scanned_at    Float
            a findings      List<index: Integer, track: Track, Enum(Duplicate, Unavailable, Outlier)>
        - a set of Changes with
            a changeId      String
            a playlist      Playlist
            an applied_at   Float
        
    actions:
        - analyze(playlist: Playlist): (report: Report)
            requires: playlist is available and valid
            effects: generates and returns a report of the playlist analyzing each song as a duplicate, unavailable, or mood outlier. 

        - apply(playlist: Playlist, report: Report): (changeId: String)
            requires: PlatformLink gives us access to modify playlists and access information
            effects: modifies the playlist based off the report and findings
            
        - undo(user: User, changeId: String): (changeId: String)
            requires: changeId String
            effects: reverts changes from changeId and returns a new changeId

**Essential Synchronizations** (Not All But A Few)

1.   
    **sync** linkIngest  
    **when**  PlatformLink.link(user, platform)  
    **then** LibraryCache.ingest(user)  

2.  
    **sync** updateScores  
    **when**  LibraryCache.sync(user: User)  
    **then** TrackScoring.score(user: User, track: Track)  

3.  
    **sync** cardKeep  
    **when**  SwipeSessions.keep(sessionId, track)  
    **then** TrackScoring.keep(user, track)  

4.  
    **sync** cardSnooze  
    **when**  SwipeSessions.snooze(sessionId, track, days [Optional])  
    **then** TrackScoring.snooze(user, track, days [Optional])  


## UI Sketches

## User Journey