# Assignment 1

## Domains
1. Music resurfacing and recollection - Remember forgotten "bangers" and sort them into new playlists!

I love listening to music. I love discovering new songs and going back to old ones even! Sometimes I spontaneously make new playlists and lose track of songs over time. As my catalogue of liked songs grows, it becomes more difficult to remember those good ol' tunes. I feel like there is definitely a fun way to be able to rediscover and sift through your liked songs!

2. Music playing simplified (guitarists) - Make finding songs within your level by being able to notate which chords you know and finding a catalogue of songs within that level.

I love playing music! I remember starting as a beginner on the guitar and having no idea what I could do with the limited chords I knew. When learning music, one of the things you realize is a lot of the same songs use the same chords so how cool would it be to be able to learn songs from a few chords you know? Even for trained musicians, you could find songs that use certain progressions which would definitely be useful! I think there is a lot of potential here in being able to make a fun music finder.

3. College workout pinger - Workout with your friends in the same house or dorm by sending a message/ping for when you are heading out to the gym! As someone who lives with friends, we find that we sometimes run into each other at the gym or just ask each other at random times to go and it would be nice to have a good quick system. 

I've recently been getting into working out again. My friends, especially at the frat house, have been pushing me to go but sometimes our schedules don't always align or we can't always find each other at the house. It would be super neat to have a method of sending an alert to your friends of when you're going so then you could eventually meet up with one another!


4. Live-show radar with friends - track venues/events/shows/artists you and your friends care about! Make it easier to coordinate who is in and add your notes!

5. Centralized message system - Make communicating with friends a more simple process by being able to do it all on one system. Helps with managing between so many apps like Signal, Whatsapp, Discord, Messenger, Instagram, Slack, etc.

6. Gaming modlist sync - Create a portfolio of modlists for different games to share with friends. Allows to share presets and check version compatibility 

7. Remote jam collab - Find a way to jam (artistically - music or art) with your friends virtually! For experienced people, you can provide your own stems/loop and trade ideas with friends. Non-experienced users will have easy interactive systems to use!

8. Social virtual quests - Daily or weekly challenges to do with your friends (it could be like "what app did you doomscroll on the most?" or "favorite tiktok of the day?")

9. Instrument practice tracker - Achieve micro-goals, keep some streaks, and even make some notes about your learning progress on guitar/piano/vocal or any instrument!

10. Lyric highlighter - Create a portfolio of your favorite lyrics by highlghting lyrics when you are listening to songs

11. Personal music journal - Add notes about songs you've listened. Keep track of songs you've listened to across different platforms

## Problems

1. Rediscovering and Recollecting Music
    * Forgotten likes: Your "liked" library grows fast! Great tracks fade and don't get replayed
    * Playlist quality decay: Over time a playlist loses its vibes (duplicates, deleted tracks, or even mood outliers) and you stop using it
    * Cross-platform scatter: No method of pulling liked songs from different platforms, and hopping to different apps can cause to miss songs

2. Music Playing with Chords Simplified
    * Beginner-friction: As a beginner, you know a few chords but can't find playable songs that match your skill
    * Relevant chords: As a beginner, it is hard to know which might be the next best chord to learn. Ex: (B7 instead of Bm if playing a progression)
    * Tab/Chord Inconsistency: Chords/tabs vary in quality/key, this makes it more difficult for beginners to find the right versions especially with their skillset. 

3. College Workout Pinger
    * Coordination Latency: Group chats are always dead or super noisy. Even when people respond, the window is closed
    * Lack of availability: You know who's nearby, free in the next 30-60 minutes, or even going to the same gym!
    * Motivation fade: Without having some lightweight nudge or form of accounability, it's hard to keep a streak! Having friends helps!

### Selected Problems
1. Forgotten Likes Resurfacer (Domain 1)  
As your likes grow and pile up (ex. 2500 for me!), great songs can get buried! For me, I try to always scroll through my liked songs to revisit the classics but it is just super time consuming especially when I am trying to read through the titles one by one. It is just time consuming to have to sift through all of your like songs to try and find an old classic. It would be nice to have a format to sift through your liked songs and even be able to add them to a playlist. I think it is possible to build a dymanic system that can help re-queue tracks from your earlier likes

    Why Included: For deep fans of music who have large catalogues, it can be a bit cumbersome to navigate through all of those songs. It is a pain I share as well and just feel that it is certainly feasible to design a certain application and has lots of potential for fun UX experiences!

2. Beginner-Friction with Chords (Domain 2)  
Beginners stall and lose confidence when they are unable to play songs. As someone who remembers the troubles of having to learn the guitar, it can be so frustrating and discouraging when your efforts can't even amount to playing a song. However, many popular songs actually utilize the same chords and this can be helpful for beginners that are looking to learn new songs. A matcher that takes your chord inventory and returns playable songs can help build better practice habits and improve progress.

    Why Included: It has clear value and I think it is an application that has a lot of potential to be adopted by novices. It seems to be within a reasonable technical scope. Authentic demand.

3. Motivation Fade Reducer (Domain 3)  
Going to the gym alone can be a mentally taxing task for those. However, having a friend to help or join you can always improve the experience. As someone who has been getting back into the gym, I find that having friends really helps push me forward and hold me accountable. Seeing my friends go to the gym, makes me want to drop any lazy task I am doing and be more productive. Having a gym pinger that tells you when your friends in the house are going to the gym can help push people to go to the gym with their friends without the need of needing to ask when it is happening!

    Why Included: I included this problem because I think that motivation is a really big problem for me but having friends has made it possible for me to push forward on days that are difficult. I believe an application to tackle this problem is very buildable and possible.


### Unselected Problems
1. Playlist quality decay: I believe this issue can be resolved with the forgotten likes resurfacer. With rediscovering songs, you can find a better arrangement for the songs in an old playlist that you once liked
2. Cross-platform scatter: This is also a capabilty that can be added onto the forgotten likes resurfacer as it can be used to gather all liked songs from different platforms

1. Relevant chords: Seems like a two-phase system that is hard to implement where you would need to have statistics of what players know beforehand and at an intermediate level. Additionally, you need to assess what chords fall into that category and how they fit into the song. Just a bit complicated.
2. Tab/Chord Inconsistency: It seems like it would just fail since there are already other such great websites that do this (ex. Ultimate-Guitar) but it could be free!

1. Coordination latency: Similar to Domain 1, it just feels like this issue can be resolved with the pinger that immediately lets you know when a friend is on their way or will be.
2. Lack of availability: Requires users to give up more of their privacy by having their location share whereas a pinger gives a notification without giving up location. Just an extra step but still can be implemented with our pinger!
## Stakeholders

1. Forgotten Likes Resurfacer
    * Listener (primary user): Heavy music fan with a large music catalog
    * Artist & Label (owners): Content holders whose catalog benefits from renewed plays
    * Platform: Spotify/Apple/music platforms whose APIs and policies shape what's possible and receive additional plays
    * Friends (secondary): Friends who receive the new mixes

    Impacts: The listener gains joy and variety by re-hearing buried favorites; success comes from higher replay of older tracks and newer playlists wth old tracks. Friends can benefit from better recommendations which can drive social sharing. The platform can see deeper engagement but might be the bottleneck with constraints (i.e. rate limits) that influence app development. Artists/labels gain incremenental streams from older songs and can use this feature as a metric to show replayablity of a song. 

2. Beginner-Friction with Chords
    * Beginner Guitarist (primary): Learner with a small chord inventory who wants to learn songs
    * Teachers: Instructor who can track progress
    * Songwriters/Artists: The entities whose works are being learned and performed 

    Impacts: The beginner gets a clear path from "What I know" to "What I can play", boosting motivation and practice frequency. Mentors can align homework with beginner's chord set, saving prep time. Songwriters/artists benefit when legal, credited resources are used; however if the solution leans on unlicensed content then the impact can be negative.

3. Motivation Fade Reducer
    * Initiator (primary user): Person sending the "heading out now / in 20" ping. 
    * Responders (friends/housemates): People who join the ping based on their proximity and availability
    * Campus Gym Staff and Faculty (Service provider): Facility experiences small surges when pings align and meet up

    Impacts: The initiator benefits from quick responses that convert intent to action. Success looks like faster coordination and more co-workout sessions with friends. Responders can also receive the same benefits but can be overwhelmed with pings so spam management is important. The staff and faculty will see boost in gym attendance but can suffer from equipment bottlenecks. 

## Evidence
1. Forgotten Likes Resurfacer  
    Evidence:
    * [Spotify removes it's 10,000-song library limit](https://www.theverge.com/2020/5/26/21270409/spotify-song-library-limit-removed-music-downloads-playlists-feature)/ Spotify removing the limit shows how users are running into large, unwieldly libraries.
    * [Users share their library sizes](https://www.reddit.com/r/spotify/comments/1j6g2mf/how_many_liked_songs_do_you_have_and_how_long). Demonstrating the need for Spotify to make this change and providing anecdotal evidence of users reaching this limit
    * [200 million songs on streaming services](https://www.musicbusinessworldwide.com/there-are-now-more-than-200m-tracks-on-audio-streaming-services-nearly-100m-of-them-attracted-no-more-than-10-plays-each). This demonstrates how the firehose is real and that not only are users discovering new music but the catalog for new music is massive and ever-growing.
    * [Preferences for Last.fm](https://medium.com/the-riff/why-i-still-use-last-fm-and-you-should-too-d193a5a20521). Many users had negative opinions about Spotify Wrapped these past few years. As a result, some Last.fm users spoke up about how they believe Last.fm provides better insight since they have longer listening histories and you don't always have to wait until November.
    * [Users note songs vanishing from liked songs](https://www.narendravardi.com/vanishing-tunes-ten-percent-of-my-liked-songs-disappeared-on-spotify/). Some users ranting about how a percentage of their songs vanish which could be due to license renewal. This causes issues where some users may never know and forget about songs they once loved!

    Comparables:
    * [Spotify Wrapped](https://support.spotify.com/uk/article/spotify-wrapped/). A recap of a user's listening patterns over the year. Helpful to see statistics about one's listening and can help show songs. The downside is that it is a long process (over a year) and isn't intended for resurfacing songs beyond a year.
    * [Spotify Daylist](https://newsroom.spotify.com/2023-09-12/ever-changing-playlist-daylist-music-for-all-day/). A dynamic, mood-titled playlist that refreshes multiple times a day. Curated to a user's vibe but doesn't necessarily tackle the issue of resurfacing old past liked songs. A good fun way of discovering music.
    * [Spotify Daily Mixes](https://www.vox.com/2016/9/27/13070726/spotify-daily-mix-playlist). Spotify has a feature that analyzes your latest listening patterns and curates "daily mixes" with liked songs based on your listening patterns. If I was listening to Rock n Roll for a week, I can expect to find some Rock n Roll daily mixes.
    * [Youtube Music Recap](https://blog.youtube/news-and-events/2024-music-recap-youtube/). Similar to Spotify Wrapped, this is intended for Youtube Music users. Can gain useful insight about one's listening patterns especially on content across Youtube.
    * [Apple Music Replay](https://support.apple.com/en-us/109356). Similar to Spotify Wrapped and Youtube Music Recap, instead curated for users of Apple Music. See listening statistics over the past year. Something to note is that none of these yearly recaps have a way to export this information into a viable format for potentially creating some interface for revisiting songs.



2. Beginner-Friction with Chords  
    Evidence:
    * [90% of guitarists quit within a year](https://www.guitarworld.com/news/90-percent-of-new-guitarists-abandon-the-instrument-within-a-year-according-to-fender). Beginner drop-off is massive! It is a real problem so being able to push motivation and early wins is critical for minimizing beginner drop-off.
    * [Guitarists quit from not feeling successful](https://holisticmusicianship.com/blog/why-so-many-beginners-quit-guitar).  As beginners begin to learn guitar and songs, they compare studio recordings to their own performance and do not feel that sense of accomplishment. This can be discouraging for new players
    * [Three-chord songs](https://en.wikipedia.org/wiki/Three-chord_song). Many songs consist of 3 chords which are formatted into a standard progression. The use of the tonic, subdominant, and dominant is a fundamental basis for these progressions. 
    * [Four-chord songs lawsuit](https://www.fretzealot.com/2023/05/what-ed-sheerans-court-case-tells-us-about-four-chord-songs/). A slight step-up from the 3-chord songs to spice up your songs is four-chords. This article dives into a court case over trying to copyright chord progressions which shows how progressions are so standard.
    * [Memorizing chords and chord techniques](https://melbourneguitaracademy.com/how-to-quickly-memorise-guitar-chords-and-develop-smooth-chord-changes-my-simple-5-minute-routine/). One of many examples on how many websites focus on the practice of chords with tips and techniques. Many teachers offer different insights but it only drives how important it is to know chords and find a method that is easy for beginners.

    Comparables:
    * [Ultimate-Guitar](https://www.ultimate-guitar.com/). The main source of refined guitar chords (and even tabs) for songs. Gives different versions which can be community-rated. However, for more exclusive content or features, it is locked behind a paywall. Not able to personalize chord inventory.
    * [Chordify](https://chordify.net/). A simple easy way of discovering new music and following along with songs. A minimal design and clean interface, however, no explicit way of sorting songs by chords.
    * [Yousician](https://yousician.com/). A game-like way of learning music that is supposed to make learning guitar a more fun and interactive experience. Encourages practice with more visuals and more robust systems. No method of sorting songs by chords.
    * [Oolimo](https://www.oolimo.com/en/). A chord analyzer/finder. Doesn't provide songs based on chords but it can help analyze fingerings of chords and decipher methods of playing chords. Useful tool for beginners to learn fingerings and different chords but no song testing.
    * [Hooktheory](https://www.hooktheory.com/trends). Allows you to learn and discover songs based on a chord progression built from a starting chord. Very useful, however, it is not entirely beginner friendly as it requires knowledge about progressions and knowing which progressions you want to play.

3. Motivation Fade Reducer  
    Evidence:
    * [Exercise groups can help strengthen exercise identity](https://pmc.ncbi.nlm.nih.gov/articles/PMC9053316/). Reviews in college and adult populations have been able to link workout buddies and groups with better exercise initiation and persistence!
    * [The impact of exercising with a partner](https://journals.sagepub.com/doi/full/10.1177/02654075211012086). Research was able to show that people were more successful at exercising if they did so with their romantic partner. The study illustrates a reason as to why people are more successful at maintaining their exercise routine when they exercise with their partner. It drives the point of working out with a partner or friend.
    * [The surprising benefit of working out with friends](https://www.anthro.ox.ac.uk/article/why-exercising-friends-could-be-better-you). The article provides deeper insight into our need for socializing as creatures but also as to how the comfort of having a friend (socializing) can offset the feeling of fatigue in the human cautious system. 
    * [Benefits of walking with friends](https://www.health.harvard.edu/staying-healthy/better-together-the-many-benefits-of-walking-with-friends). While focusing on walking, this article reviews the many benefts of going on walks with friends. It states how it is a great social activity, helps put you on a schedule and stay motivated, and is practical. While maintaining a gym routine may be more complicated, going on a brisk walk with friends is a lot easier.
    * [Promoting activity in college-aged students](https://www.cdc.gov/pcd/issues/2025/25_0118.htm). CDC authors note that most college-aged students fail to meet physical activity guidelines, and physical activity levels decline after high school. Having a means of being able to push college students toward exercise in a meaningful and beneficial way is a necessity which is highlighted by this article.

    Comparables:
    * [Step Up](https://thestepupapp.com/). A free social step counter that allows you to create a group with your friends and compete on who can reach the highest step count by the end of the day. Limited in being only a step-counter but it is a quick, fun, and minimal way of being able to collaborate with friends even on separate times.
    * [Liftoff](https://liftoffrank.com/). A fun competitive workout app that puts it in a game-like ranked system. Allows you to compete with friends and see who reaches a higher rank, which is based off your workout consistency, performance, and progress but is more geared towards progress tracking.
    * [Strava](https://www.strava.com/). A running app that allows the users to keep track of their progress. It remembers records, and it allows one to see their friends activites -- runs, hikes, swimming sessions, and even workouts. The users can give each other 'kudos' and comment on their friends; activities which appear on the user's feed but doesn't have immediate notice features.
    * [Discord Scheduled Events](https://support.discord.com/hc/en-us/articles/4409494125719-Scheduled-Events). Able to plan sessions on discord with friends. A bit limiting since it's only for Discord users. Adds platform friction for non-gamers but can be beneficial and useful for the gaming community since Discord is geared towards gamers.
    * [When2Meet Scheduling](https://www.when2meet.com/). A form of being able to share availability with friends for any form of event. More optimized for calendar polls and hard to gauge immediate availability. Requires all users to input schedules in order to see the optimal time for working out. Lacks a feature for sending out immediate notices of events.

## Features
1. Forgotten Likes Resurfacer
    * Time-Capsule Shuffling
        * What it does: Applies a "score" to your library based on factors like: last play date, liked date, skip rate. It can create auto-mixes based on these scores and provide a one-tap feature to save any old track to a fresh playlist.
        * Why it helps: The listener gets a low-effort rediscovery method that can be integrated seamlessly into their music listening habits already. Friends benefit because revived tracks can feed into better shared playlists. 
    * Song Memory Cards Swiper
        * What it does: Presents songs as swipeable cards with quick actions such as: Keep in rotation, Skip for 90 days, Add to playlist. Rather than trying to seamlessly add old songs into the users music, the user can decide to swipe through songs and sort them into playlists in a manner similar to Tinder or Tiktok. 
        * Why it helps: Reduces decision fatigue and provides a fun alternative of sorting through songs for the listener. Platforms benefit from deeper engagement and artists gain plays.
    * Music Catalog Gatherer
        * What it does: Gathers songs from the users connected music platforms and displays in a centralized interface. Helps gather information across different platforms to capture listeners full library.
        * Why it helps: Helps the listener gather songs faster rather than having to meticulously go through each platform's liked songs. Can help produce shareable mixes for friends without cross-platform complexity. 

2. Beginner-Friction with Chords
    * Chord inventory -> playable songs
        * What it does: You tick the chords you know (plus are bar/capo comfort with). The app returns a sortable list of songs playable with exactly those chords, with optional learning filters to stretch your skills.
        * Why it helps: Gives the beginner guitarist a catalog of songs to play and can help motivate them to keep learning new techniques and chords. Teachers can also assign students songs within their ability.
    * Unlock chord map
        * What it does: Start from a chord and build up your chord skills. It can show which new single chord would unlock the largest set of additional songs (Ex. B7 chord would help unlock 63 more rock songs).
        * Why it helps: Targets focal points for beginners to learn more songs and give more momentum to their learning. Can also be a helpful tool for teachers.
    * 15-minute setlists
        * What it does: Generate a 3-4 song setlist from the chords you know. Gives the ability to practice strumming, train your rhythm, stay in tempo, and practice different transpositions.
        * Why it helps: Can begin to develop a repetoire for a beginner and focus on their techniques aside from the chord theory. Teachers can receive a log to review and develop further lesson plans!

3. Motivation Fade Reducer
    * One tap ping
        * What it does: The user taps a button to broadcast an announcement to friends about their gym intent such as: leaving in 30, leaving now, or a window. Pings expire, don't spam, and don't require location.
        * Why it helps: Maintains privacy for users (initiator and responders). Initiator can have friends join and responders have a clear window to join. The opportunity for a group workout is open without the necessity of much coordination.
    * Smart escalation          
        * What it does: If no one responds within a timeframe (ex. 10 min), the app offers the opportunity to expand the ping to friends-of-friends or go into a Solo Mode.
        * Why it helps: Preserves momentum for the initiator (primary user) by allowing them to find a buddy or just go solo and still get a productive workout. Prevents disrupting other users by allowing the initiator to go solo.
    * Buddy streaks and accountability nudges
        * What it does: Track pair and group streaks (which occur when people check in within the time window). Offers gentle reminders to those not keeping up.
        * Why it helps: Streaks can drive motivation between the initiator and responder. It can also push other responders without streaks to join if they are not keeping up!