---
layout: blog_post
title: "New Game Idea: Tag Team"
category: game-development
subcategory: tag-team
---

Making a game for a friend who has never watched a movie.

<!--more-->

You might think this is hyperbole, and it is, but not by a lot.
<br><br>
To give some background, I really like [Cine2Nerdle's Battle Mode](https://www.cinenerdle2.app/battle).
It's a competitive 1v1 game where you're given a movie, asked to name another movie that shares a cast member,
then play is passed to your opponent to do the same.
When you successfully pick a film it reveals the 'links' (shared cast) between those films, and you can't use the same link more than 3 times
(each use puts a 'strike' next to that link, three strikes and it can't be used any longer).
<br><br>
I really like this game, especially because my brain doesn't really organise information this way.
I've always had trouble recognising actors, and when I've recognised them I haven't known their names,
and even if I'm told their name I might not be able to name a single film they're in even if I've seen a dozen of them.
This game motivates me to form those links, which in turn gives me a stronger idea of the careers of various actors and directors.
<br><br>
Another great thing about this game is it's really easy to play with friends.
The format lends itself a lot to being in a team (people tend to have different film tastes, so everyone can contribute something a little different)
and pretty much everyone has seen plenty of movies in their life (although recent trends suggest shrinking attention spans are slowly eroding that reality).
<br><br>
The story of this game starts with a friend who has seen no movies.
<br><br>
When I suggest this game to people they often say "I dunno, I haven't seen a lot of movies..." and then proceed to thrash me.
Turns out most people have seen a lot more movies than they think.
And even if they don't know the names of the actors in those films, they can picture them in their head and find another movie they're in.
<br><br>
So when a friend of mine said they hadn't really seen any movies, I was optimistic that they were underestimating themselves.
I set the starting movies to Avengers: Endgame.
<br><br>
For those unaware, Avengers: Endgame is a common (and poetically appropriate) movie people will randomly guess if they feel stuck.
This is because the movie contains pretty much every actor.
Even if you haven't seen it (like me, funnily enough)
you know Robert Downey Jr. is in it as Iron Man (the Sherlock Holmes movies, Dolittle, Tropic Thunder, Oppenheimer),
Samuel L Jackson of course makes an appearance (Django Unchained, Pulp Fiction, the Star Wars Prequels),
there's Mark Ruffalo (Now You See Me 1 and 2),
Scarlett Johansson (Lost in Translation),
Benedict Cumberbatch (every movie released after 2012)
and Chris Pratt (The Super Mario Bros Movie).
And I'm only naming non-MCU roles here.
You could just shrug and put "Iron Man 3", "Guardians of the Galaxy" or even "Avengers: Infinity War" if you really had no clue.
<br><br>
My friend had 40 seconds to name a single movie that shared an actor with Endgame, and couldn't do it.
<br><br>
This is not a dig at him. If anything, I envy his zen-like unawareness of the MCU and every other property acquired by Disney.
But since he clearly couldn't play this game I tried to think of an alternative,
and it just so happens that this friend of mine is one of the only people I know to beat me at "number of distinct games played" on Steam.
<br><br>
So: an idea. What if we played the same game, but with videogames as the subject, rather than films?
<br><br>
The immediate issue is that videogames generally don't have a cast, and when they do it's Troy Baker and Nolan North.
They do have developers and publishers, but they don't overlap much.
Games tend to be either developed and published by the same entity (AAA games come to mind)
or developed by someone whose life's work is two games and published by a publisher whose published hundreds of games by devs in a similar situation
(indie games).
<br><br>
Neither of those are particularly fun to play, so the question remains "What could you use as links?".
Ideally a game should have around a dozen links - some well known or obvious, others more obscure -
and there should be a spectrum of how much these links overlap.
What I mean by that last point is that two games could have no link, one link, a few links or many links (one of those categories shouldn't dominate).
<br><br>
What we decided upon was Steam Tags.
You can view these on the store page (currently displayed beneath the developer and publisher) and they fulfil most of these requirements pretty well.
The main issue is that if two games share a tag, they usually share many tags.
This is an issue with a few solutions, but they each have their own pros and cons.
As such, I figured I'd implement all of them and see which ones stuck.
<br><br>

# Solution 1 - Top 5 Steam Tags

This is what we went with when playing the game casually the first time without any kind of system in place to keep track of everything.
Steam shows you around 5 tags for a game on the store page for it, and they're the most popular ones.
So you essentially pretend every game has only five tags, and this makes everything a lot less of an issue.
Games are usually linked by 1-3 tags, but rarely all of them. Even sequels tend to diverge.
<br><br>
The biggest issue for me is that a lot of interesting tags get hidden by this method.
'Silent Protagonist' is a fun tag which links otherwise unrelated games, but it's basically never one of the top 5.
Eliminating so many tags is especially an issue given that there's a lot more actors than there are Steam tags.
This means the game feels a lot more restrictive than a Cine2Nerdle game, with a lot less to learn.
<br><br>
Finally, it can be unintuitive what tags are going to be in the top 5 tags for a game.
In a test game, someone went from Binding of Isaac to The Legend of Bum-Bo via Edmund McMillen
(we allow linking by developers and publishers in addition to tags).
I thought it'd be hilarious to go from The Legend of Bum-Bo to HuniePop via the tag 'Match 3'.
That's basically the central gameplay mechanic of both games, so surely it's in the top 5 steam tags for both, right?
It turns out that it's actually in the top 5 for _neither_ (although they do share 'Puzzle').
<br><br>
This really cemented the idea that this technique was insufficient,
so I tried thinking of alternatives that might achieve similar goals.

# Solution 2 - Called Tags

In Cine2Nerdle you don't have to name the actor you're using to link films.
This works well, because some people recognise an actor's face but can't remember (or spell) their name.
It also means that movies which share a huge portion of their cast (Wes Anderson or Edgar Wright films come to mind)
will suddenly spring all of them as links if you go between them,
but this is fine because there's a huge number of actors.
<br><br>
I keep saying that there's "a huge number of actors" to use as links compared to the tags we've got to work with,
so let me give you a feel for how large that disparity is.
At time of writing there's 449 official Steam tags (according to SteamDB) and two similar Steam games
could link on 4-8 tags. Endgame and Infinity War (possibly the films with the biggest overlap in cast) share a few dozen actors,
but there's thousands of them (getting stats on this is hard but a list of the Top 1000 Actors and Actresses on IMDb still ends on well known
names, so I'd estimate there's a few thousand well-known actors and hundreds of thousands of obscure ones you could still use in a game).
As such, two run-of-the-mill games can put a comparable dent in the pool of links to the biggest crossover event in cinema history.
<br><br>
Previously we fixed that by only using the top five tags, which limits the number of links and also means there's essentially a random chance
certain obvious links won't get used (because they just happen to not be in the top 5 for one of the games), preserving them for later.
Instead, we can say you need to specify the tag you're using to connect two games.
<br><br>
Unlike actors, tags are usually easy to intuit and name, so asking the user to explicitly state what they're using isn't a big drawback.
This also encourages using more obscure tags to link between seemingly unrelated games, which I think is fun.
However, this significant deviation from Cine2Nerdle raises a notable question:
If two games share a link with three strikes (eg. Puzzle) but you state you're linking them via a different tag (eg. Match 3) is that allowed?
<br><br>
In my opinion the answer is 'yes'.
As stated earlier, Bum-Bo and HuniePop share 'Match 3' (a cool and interesting tag to link from), but also share 'Puzzle'.
Since most games with Match 3 will also have Puzzle (another unfortunate property of tags as links), you'll rarely get to link off of these tags and nothing else.
In particular, I hate the idea of getting cornered in Bum-Bo, with three strikes on Puzzle, then trying to escape through Match 3 and getting blocked.
<br><br>
So in this system you can link off of developers/publishers without needing to name them (like in Cine2Nerdle)
but if you want to link off of a tag you need to specify which one.
Personally, I think this mode will see the most success.
But it's worth implementing all my options so I can experiment with them.

# Solution 3 - Allow Overlap

In Cine2Nerdle, if Robert Downey Jr. has three strikes you cannot link between two Robert Downey Jr. movies, _even if there are other links between them_.
This helps with a few things, an obvious one being you can't exhaust every Harry Potter or Stan Lee movie before moving on.
You can rarely play movies from the same series more than four times in a row because they usually share at least one cast member.
<br><br>
But in this game, maybe allowing this isn't so bad?
If 'Puzzle' has already been exhausted, no problem, we're not going to block you from traveling between Puzzle games as long as there's at least one more link.
This has a lot of similar advantages to the previous solution, but it feels less deliberate to me.
If you type the names of three random Steam games you'll probably find one with at least one link to your current game,
so it encourages rapid guessing a lot more than deliberate demonstrations of knowledge.
Not only that, it still ends up churning through tags like nothing else.
It limits the impact of churning through tags, but you will still end up unable to use common tags to link between games relatively quickly,
and I think that makes the game less accessible.
It also means that cool moves like the 'Match 3' link I keep lauding end up also causing unintended strikes on common tags like 'Puzzle', so in some cases
you won't gain a lot by being stylish.
<br><br>
Overall I'm not super satisfied with this technique. But it's worth considering.
<br><br>

# Conclusion

With all of that out of the way it's time to start developing the game.
There's only so much you can theorise about without just testing the ideas you're playing around with.
I'm going to get a local 'couch co-op' version going first, and move on from there.
