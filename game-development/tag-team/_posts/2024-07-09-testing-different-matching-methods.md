---
layout: blog_post
title: "Testing Different Matching Methods"
category: game-development
subcategory: tag-team
---

I finished making an offline version of my game, and have playtested it with some friends. Here are the results.

<!--more-->

First of all, here's some screenshots of the game!
<br><br>
![Screenshot of the Game](/assets/images/screenshots/tag-team/tagteam-screenshot-01.png)
<br>
_The art and tags for a game can be revealed using lifelines._
<br><br>
![Another Screenshot of the Game](/assets/images/screenshots/tag-team/tagteam-screenshot-02.png)
<br>
_If you hover over a game's art it zooms in to let you get a better look at it._
<br><br>

When I started developing Tag Team (I title I've found myself not using when referring to the game, meaning I'll likely change it in the future)
[I described a few different techniques]({% post_url 2024-05-27-tag-team-motivation %})
I might use to jump from one game to another using its Steam tags.
Now that I've done some testing I have a clearer idea of which of those techniques I prefer and the design of 'graph traversal trivia' games generally.
<br><br>
Let's start with some of my findings with regards to which technique I like better.

# Top 5 Tags

This was the first technique my friend and I tried when playing this game manually.
Basically: you pick a game that has at least one of its top five Steam tags in the top five Steam tags of the game you've been given.
<br><br>
When I first described this strategy I didn't like the fact that the top five Steam tags for a game can be a little bit random.
Core mechanics might not get mentioned if other more generic tags take precedence.
Obvious genre tags might not get mentioned if something else is considered more important.
An example I used was HuniePop and The Legend of Bum-bo, both games where Match 3 is the core mechanic, yet both games where it isn't in the top five.
<br><br>
As testing continued, this was very frustrating.
It often prevented you from using unique and interesting tags to jump between games.
And, as early tests suggested, it was not intuitive what elements of a game were considered essential enough to make it into the top five.
<br><br>
Overall, this resulted in games that didn't last long and ended unsatisfyingly.
It was very easy to get to a game where a common tag like Action gets used up,
and the top 5 tags to link off of are 'Action-Adventure', 'Action RPG', etc.
And now you need a game which has Action-Adventure but not Action, which isn't impossible but it's difficult and hard to predict.
You basically need to guess hordes of Action Adventure games with the hope one of them randomly doesn't have Action in its top five tags.
<br><br>
So not exactly phenomenal results from this method.

# Called Shots

This worked excellently.
I was surprised that this only took an hour or so to build upon my original system,
and as soon as I tested it I got fantastic results.
<br><br>
A reminder if you haven't read my previous post: this mode only lets you link on a tag if you specify which tag you're using to do so.
Links on developers or publishers are done as normal, and have precedence
(you can't go between Final Fantasy games using tags if Square Enix has three strikes),
but if two games both have Action (which has three strikes) and you specify you're linking on Action-Adventure that's totally allowed.
<br><br>
This really opens you up to use basically any tag you want that might apply to a game,
and experimentally this seems to have worked excellently in all but one instance.
Shout out to [The Rewinder](https://store.steampowered.com/app/1161170/The_Rewinder/) (which I jumped to via the third strike of Mythology)
for not having Time Manipulation or Time Travel despite those both being central mechanics of the game.
<br><br>
There was also another interesting consequence of this approach.
As I discussed in a previous post, a classic Cine2Nerdle technique is to play something like Avengers: Endgame if you get stuck.
Since Steam games all have thereabout the same number of tags and none of them fill this niche the same way,
instead of panic picks you get panic tags.
Singleplayer, Multiplayer, Action, Mystery, Story-Rich, there are several tags you can use as an escape rope from almost any game.
Not only is it almost guaranteed that one of them works, you can use them to jump into an obscure game your opponent might not recognise.
In response your opponent might try and use the same tag to escape,
but now you have the opportunity to play an even more obscure game with that incredibly broad tag and force them to use a lifeline.
If your opponent evades this trap by recognising either if your obscure games, there is now one less 'panic lifeline' at your disposal.
<br><br>
While this fulfils a similar purpose to panic picks like Avengers: Endgame, in my opinion this feels more satisfying.
It's more skill-based, both in needing to learn common panic tags as well as needing an obscure game to jump to them with.
When you use Singleplayer to jump to Mouthwashing or Bombe you feel like you pulled off a sick trick rather than a desperate ploy.
To me this makes games feel a lot better paced - you go back and forth, jumping between common games using clever tags,
when suddenly someone gets cornered and is forced to send you to the shadow realm by going to PataNoir via Adventure.
It also makes your panic picks feel more unique to you rather than being generic movies everyone uses.
<br><br>
This actually brings me to a point I want to explore further:

# Linking Analysis

The gameplay with Called Shots felt like the best way to play the game, and so with that in mind I wanted to compare the gameplay to Cine2Nerdle's.
Cine2Nerdle's gameplay, from experience, has the following properties:

-   **High Barrier to Entry** - Casual moviegoers may not know their actors very well and will quickly get lost in lesser known films
-   **High Skill Ceiling** - Players can become [unfathomably skilled](https://www.youtube.com/watch?v=P8sxtgN9c24) and express this skill,
    most of this comes from having encyclopedic film knowledge
-   **Emphasis on Opening Theory** - Players taking the game seriously can memorise obscure links to movies they otherwise wouldn't have heard of,
    particularly using links to cast members present in the day's roster of starting films
-   **High Variance in Link Fame** - Some actors are easy to name a film for, others are practically unknown to all but the most skilled players
-   **High Variance in Target Fame** - If you get a movie you haven't heard of and your opponent just got the third strike on the only link into it,
    it's rarely easy to intuit the cast of a movie simply by its name
-   **Early Floundering** - A skilled player can immediately put an unskilled player somewhere they'll need to use a lifeline to escape
    (I find such games unsatisfying)
-   **Satisfying High Skill Volleys** - When two skilled players go against each other, games are tense and fun to play and watch
-   **Inconsistent Pacing** - Games can be over instantly (which I find unsatisfying) or go for a satisfying but inconsistent amount of time
-   **Tight Strategic Control** - If you love romcoms then trying to constantly link back to romcoms can be a huge advantage
    since you'll be familiar with the regular cast of actors in that space
-   **Expressive** - The movies you pick and the genres you're comfortable in say a lot about your film taste and provide opportunities for self expression

Comparatively, Tag Team has:

-   **Low Barrier to Entry** - Casual PC gamers, after only one or two games, can usually hold their own in the early game
    (this applies inconsistently to console gamers, depending on how many of their favourite games have found themselves a PC port on Steam)
-   **High Skill Ceiling** - Encyclopedic game knowledge contributes less to skill because games are unlikely to have exclusively rare tags
    (unlike the many movies with exclusively obscure actors) but many games have well known tags you didn't realise they did,
    meaning you can instead gain skill by learning common tags and their patterns
-   **Minimal Opening Theory** - Thanks to panic links, there are usually tens of thousands of games you could go to from your starting game,
    making memorising opening theory impossible
-   **Mild Variance in Link Fame** - Since tags are designed to be intuitive descriptions of games,
    there is a high minimum fame for tags, with many being guessable without you having heard of them before, though panic tags do still dwarf others
-   **Mild Variance in Target Fame** - Since the name of a game is part of its marketing material, you can often intuit a game's tags through its name,
    meaning that even obscure games have plausible ways out (and learning games that have misleading names becomes another area for skill expression)
-   **Consistent Early Game** - With so many panic tags available, after a game or two you'll quickly have a consistent early game regardless of skill level
-   **Satisfying High Skill Volleys** - Skilled players make the game fun not only by naming obscure games, but also through creative tag choices
-   **More Consistent Pacing** - A single game usually lasts a consistent amount of time,
    with shorter games still long enough to satisfy and longer games usually being a reliable indicator of the skill of the players
    (longer games semi-reliably end soon after panic links have been exhausted)
-   **Loose Strategic Control** - Until panic links get used up, you can go from pretty much any genre to any other genre in the blink of an eye,
    which is a shame since this loses that strategic element of play
-   **Expressive** - With a greater ease to move between genres comes more opportunities to express your personal taste and experience with games
    (games against my housemate feel different to games against anyone else because every second game he picks is from the Final Fantasy series)

Overall, that's a comparison I'm pretty happy with.
I think some notable weaknesses are potential game length (more testing is needed to see if games often go so long they get boring),
losing the strategic ability to lock your opponent into a genre (since panic links make jumping between genres easy)
and - while I don't have nearly enough data to be confident on this yet -
I do worry that the fact the number of available tags is dwarfed by the number of available actors could lead to
games either having pacing issues or feeling samey once you've established a meta.

# Why Worry?

I mentioned in the above list that opening theory is minimal here,
and I like that because opening theory is one of those things I consider to provide an un-fun advantage in games.
I prefer [Fischer Chess](https://en.wikipedia.org/wiki/Fischer_random_chess) for this reason.
These kinds of advantages feel almost like cheating to me in that they feel like they're circumventing the thing you're "trying to compete over".
To me [Chess](https://store.steampowered.com/app/707140/Chess/) is a game of strategy and wits.
You play [Chess](https://store.steampowered.com/app/2965280/Chess/) to try and create and respond to clever tactics invented by you and your opponent.
Memorising a couple hundred opening positions is (to me) relatively boring but gives you a huge advantage over your opponent
without you personally having to come up with any good tactics. That defeats the whole point of [Chess!](https://store.steampowered.com/app/2373460/Chess/)
<br><br>
With that in mind, you can imagine my concern that skilled players will memorise a thousand or so games, two or three for each tag,
and essentially be able to play on autopilot, with each game feeling the same.
That's not remotely doable for Cine2Nerdle.
As discussed previously, there's far more well known actors than there are Steam tags.
My current hope is that once panic tags are used up, games will settle into a pace similar to a Cine2Nerdle game,
with features like trapping your opponent in a genre becoming viable once again.
<br><br>
That said, this is all thinking way further ahead than I need to be.
Since I now have the game in a playable offline state I can do significantly more testing to see if any of these worries are actual problems.
I'll also get much more testing done once the game is playable online with a server that I can send people a link to, so that's what's up next for me.
<br><br>
I've never set up a proper game with a server publicly available online before,
so I'm expecting that making the game multiplayer and making it publicly accessible will be two separate and immense tasks.
I may have my Steam WebAPI key on the server, which means I'll need to make sure I'm setting everything up securely,
and I suspect that ensuring I have some kind of protection against getting DDOSed will be necessary.
Looking forward to describing how I tackled these challenges in another blog post!
