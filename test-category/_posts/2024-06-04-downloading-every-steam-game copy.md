---
layout: blog_post
title: "Yeet test"
---

So I wanted to make a game, and to make that game I needed to download every game on Steam.

<!--more-->

<br><br>

Well, not the games themselves.
I needed the games' metadata so I can make a Cine2Nerdle-esque game as described in my previous blog post.
If I had to download every game on Steam I'd probably run out of space after three AAA titles with uncompressed audio files.
But it turns out that almost all the metadata I could want, for every game on Steam, only takes up about 30MB.
<br><br>
That doesn't mean getting that data was easy, though.
I wanna document the process I ultimately used, and the journey to get there, because it turns out scraping data from Steam is a huge pain in the ass.
I'm hoping that anybody trying to do the same in the future will find this and not have the repeat this process, because I would not wish it upon anyone.
<br><br>
Let's start with the basics.

# So you want to download every game on Steam

To start with, let's establish the common ways of acquiring huge datasets on the web.

<ol>
<li>Finding an existing datasource, and downloading it</li>
<li>Using a webscraper to manually scrape the data you want from relevant webpages</li>
<li>Getting the data from an API</li>
</ol>

Finding an existing datasource is usually preferable if it's possible.
For example, you can just <a href="https://github.com/jesstess/Scrabble/blob/master/scrabble/sowpods.txt">download the SOWPODS Scrabble dictionary as plaintext</a>.
If you're looking to make your own Scrabble-like or any other kind of word game, this may be exactly what you need.
Also, the SOWPODS dictionary doesn't update too often, and when it does update it isn't by much.
This makes it a solid approach for that problem.
<br><br>
Unfortunately, I couldn't find a datasource like this for Steam games.
Even if I could, it'd rapidly become outdated as new releases hit the shelves and people tried to use them in the game to no avail.
So this approach won't work here.
<br><br>
I've done a little webscraping before (for my thesis, actually) using Selenium.
For those unaware, webscraping basically involves loading a webpage then acting on it as if you were just a regular user.
Using code to click on buttons, read text, and so on.
Using this, you could find some way to scroll through every game on Steam, manually open the store page for every Steam game,
read all the information you need and store it, then close it.
<br><br>
While this works, there are a few issues for doing this on Steam, especially in order to acquire the details of tens of thousands of games.
First of all, if Steam updates the format of its website (which you have to assume it will) then your scripts might break and require fixing.
Second, when you load a webpage you end up loading a lot of unneeded information that makes the process slower and more bandwidth-intensive than it has to be.
A steam store page seems to take up a few megabytes, so scraping the entire thing would take up hundreds of gigabytes of bandwidth.
In addition to all that, I'm just not very experienced with webscrapers, and this seems like a poor choice of project to improve on those skills with.
<br><br>
That just leaves us with...

# Using the Steam API

APIs let you get all the relevant data you want without also loading an entire webpage that you don't need.
Right now you can load up <a href="https://store.steampowered.com/api/appdetails?appids=632470">the Steam appdetails endpoint</a>
or <a href="https://steamspy.com/api.php?request=appdetails&appid=632470">SteamSpy</a> and get up a pretty useful list of details for any given game.
(if you're looking for the appid to put in the URL, it's the number in the URL of the game on its Steam store page)
<br><br>
Unfortunately, this does not mean we are home free. Even within that official steam endpoint, documentation is hazy at best.
<br><br>
SteamSpy looks good initially but for some reason - of all the stuff to exclude - you can't get the date the game was added to Steam.
That's a pretty important piece of info, because it helps disambiguate games with identical names without giving away much else.
Not only that, but you get throttled pretty quickly while using it.
<br><br>
The official Steam API also seems like an obvious choice - but, of all the thing it could not include, it doesn't include Steam tags.
Since that's the whole point of the game, that basically makes it unusable.
Not to mention it also starts throttling you pretty quickly if you make a lot of requests.
<br><br>
If it weren't for the throttling, I could just combine both APIs to get me full information on every game I want.
But as it stands that's way too cumbersome.
<br><br>
With the throttling in mind, I estimated you could probably get all the data you needed from Steam in about a week of continuously running the script,
pausing whenever you get rate throttled.
That's not _terrible_ but it isn't great, either.
It's also bad enough that if the game ended up being played by a few people at a time I probably couldn't fetch any of this data live - you'd be making too many
requests too quickly.
<br><br>
Surely there had to be a better way?

# node-steam-user and SteamCMD

I looked to SteamDB for wisdom and <a href="https://steamdb.info/faq/#how-are-we-getting-this-information">their FAQ page</a>
helpfully explains how they get their data and how one might go about getting it themselves.
<br><br>
It's here that they mention SteamCMD, a command line you can access in Steam and perform various operations with.
It also references <a href="https://github.com/DoctorMcKay/node-steam-user">node-steam-user</a>, a node module with a function called `getProductInfo`
that lets you get the results of running `app_info_print`, a SteamCMD command.
This wasn't obvious at first, but you can run this function while 'anonymous'.
In node-steam-user terms, this means you don't have to login and authenticate with an actual Steam account to use this functionality.
<br><br>
This is a huge relief, because doing that is scary.
Or, maybe it isn't scary. But all the stuff I could find on it online made it sound undesirable.
<br><br>
This is a good time to mention that most people looking to do similar stuff to me are looking to make Steam Trading Bots.
As such, they need full access to a Steam account and the ability to interact with it autonomously.
This requires way more permissions than anything I need,
but because every tool is set up to accomodate that it makes it look like you can't do it without performing some scary steps.
A <a href="https://www.reddit.com/r/SteamBot/comments/10dgejp/question_how_to_get_steams_shared_secret_for_totp/">guy on Reddit</a>
tried to solve this problem then <a href="https://gist.github.com/mathielo/8367e464baa73941a075bae4dd5eed90">wrote a guide</a> to step you through
the process of getting all the necessary secrets and there's a big Disclaimer at the start screaming
"If you mess this up you might lose your Steam account or get exposed to hackers".
<br><br>
Those are things I would like _not_ to happen.
So I'm glad that I eventually dug deep enough to realise that none of that is necessary for what I'm attempting.
<br><br>
Before moving on, I'd like to make the amusing observation that a lot of the people making these bots are likely children.
I found a lot of threads <a href="https://steamcommunity.com/discussions/forum/0/1638669204732688825/">like this one</a>
where the person trying to figure out how to get their shared secret can't root their phone and might not even have access to a USB cable.
I feel for them, since the main person responding to them in the thread is exceptionally unhelpful (but in an amusingly abrupt way).
I'm not judging the (presumed) kid for this - that was me, long ago (and asking much stupider questions) - I just find stuff like this funny to read.
<br><br>
Anyway.

# Getting a list of AppIDs

This process is much easier, but I alsmost missed something that made it much easier.
<a hef="https://steamapi.xpaw.me/">Here</a> you can use Steam's public API to make various requests as long as you have a WebAPI key.
Also - no, the `appdetails` endpoint I mentioned earlier is not listed here and no, I don't know why.
A WebAPI key is something you can just get for free with the link provided on that page.
I don't think the domain name you use even matters, it's just for Steam's record keeping or something.
Unfortunately, if you're like me, it might take a day or so to get that key because whenever you try and get it Steam tells you you've been making too many requests.
I _suspect_ this is because I've been using that `appdetails` endpoint a bunch and whatever system is rate limiting me is also holding me back from accessing this.
<br><br>
One way or another, once you have that you can use <a href="https://steamapi.xpaw.me/#IStoreService/GetAppList">this endpoint</a> to get a list of all Steam games
fulfilling certain critera.
Of course, you could also be a fool, a rube, a buffoon, even, and use the <a href="https://steamapi.xpaw.me/#ISteamApps/GetAppList">identically named endpoint</a>
listed under a different service and get a completely unfiltered list of games including test projects not listed on the store page.
This decoy is listed under the ISteamApps service too, which seemed far more intuitive to find than the one under IStoreService.
<br><br>
Oh well.

# Getting a list of tags

Of all the APIs discussed, only SteamSpy actually gives you the plaintext names of a game's store tags.
So I have a bunch of numbers representing tags, but no way to know what they refer to.
Finding out isn't too hard though - I downloaded the <a href="https://steamdb.info/tags/time/">SteamDB list of Steam tags</a>
(notice how I've listed them chronologically because the default way of viewing the page repeats tags across multiple categories)
then I used a script to scrape the data off of it.
<br><br>
There are definitely other ways to do this but this technique has the added bonus of giving me a corresponding emoji for every tag, which I think is cute.

# Results and Notable Complications

Using this method you can scrape all 101017 Steam games on Steam (at time of writing) after running the script for under 10 hours.
That may still seem like a while, but I can let it run in the background while I do some other stuff and it's done in under a day.
<br><br>
When I set all of this up I made it so that the program autosaves every 100 games and also remembers any games which it experienced an error while retrieving.
It turns out that no matter how hard I try to only get the IDs of valid games some weird edge case always comes up,
so I made sure that if something happened it'd just record the game's ID, put it in the "don't bother" bucket, then move on.
<br><br>
I didn't expect one of the first games to do this to be Portal 2.
<br><br>
For whatever reason, Portal 2 does not have a listed release date when you retrieve its data the way I did.
This is bizarre to me.
If it was Half Life 2 - the first game you could get on Steam - I could understand there being some kind of edge case there.
But Portal 2 is a Valve title released in 2011, seven years later.
And it isn't like this data is unavailable - you can see the release date on the store page.
It's not even that games older than a certain date had it stored in a legacy format you can't retrieve - I can get Half Life 2's release date just fine.
So Portal 2 and a select few other titles just don't have dates available in the game, and I had to rewrite the code to make including a date optional.
<br><br>
It's worth mentioning that now that I have all the data I need for almost every game, I could make a script that uses the more reliable APIs I described earlier
(but didn't use because they throttled me) to 'repair' the database and find these missing dates.
In fact, I could even gradually build up a list of all sorts of useful tidbits from those APIs as people play the game, only fetching them when necessary,
slowly building up a full database of them. I haven't implemented this yet, so that's a task for another day.

# Other Discoveries

As I continued to develop this process I was constantly looking for more ways to do more stuff with less API calls.
One thing I discovered is that the banner image - the one above the description of the game is Steam - is stored at a reliable URL.
As long as you know the AppID, you can just insert a hyperlink to it.
<br><br>
I think this is very cool.
In Cine2Nerdle you can get lifelines which help you get unstuck if you don't know what to do.
Since the banner images for these games generally include art meant to represent what the game is about, revealing this can be a good hint for what tags it might have.
And I can retrieve all of these whenever I want, don't even need to store them.
Excellent.

# Conclusion

So ultimately the process I followed was:

<ul>
<li>Scrape tags from <a href="https://steamdb.info/tags/time/">SteamDB</a></li>
<li>Get list of IDs from <a href="https://steamapi.xpaw.me/#IStoreService/GetAppList">GetAppList endpoint</a></li>
<li>For each ID, get the data through the `getProductInfo` function of <a href="https://github.com/DoctorMcKay/node-steam-user">node-steam-user</a></li>
</ul>

However, now that I've done this, you don't have to!
On the off chance you want the exact same data I do,
<a href="https://github.com/Jinan-Dangor/TagTeam-Videogame-Battle/tree/singleplayer-battle">you can get it here</a>!
I'll be keeping the repository updated so that it contains instructions in the README for retrieving the data currently in the repo,
and later the instructions for running the scripts yourself.
<br><br>
In the future I'll also try and refactor everything so that you can get the scripts and modify them easily to get any data available through the means I'm using.
<br><br>
I learned a lot from all of this!
I've already got the important features of the game working in couch co-op, so the next step is polishing it all up and setting it up as a proper hosted service.
<br><br>
The latter is something I'm not particularly familiar with, so that'll probably be the subject of my next post!
