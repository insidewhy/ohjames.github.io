---
layout: post
title:  moving from MonoGame to Unity
date:   2019-02-10 15:20:00
categories: MonoGame Unity SuperFightingTeam
---

I love MonoGame, but I'd love it even more if there was a good library (or few libraries) that provided these things for it:
- Ray-casting of polygon shapes into a scene of components, including spatial division (e.g. quad trees) to reduce the number of collision tests.
- A Component/Object/Scene system for structuring code.
- A dependency injection system to allow data that can possibly live across many scenes to be injected into Objects/Components.
- A tilemap editor.

It would be fun (and also a little painful) to work on those things but I'm a little tired of reinventing wheels so, for now, I've switched from MonoGame to Unity.

Unity can be annoying. It crashes about ten to twenty times per day. I've falls over itself without crashing leading to many restarts. Sometimes I feel like I do the same thing five times in a row and get different results. Earlier today I was importing a sprite-sheet into a tile-palette and the tiles within the sheet kept getting reordered. It worked the first three times and from then on kept giving me different versions of what I'd pasted, often containing gaps. Wasted hours getting nowhere. Today I wake up, and try the same thing again and it's worked ten times in a row. I'm not really sure if the bug will come back or not, if it does that'll mean a lot of manual work in the future. Manually reordering a messed up tile-palette is no fun, a lot of mouse clicks, and this is basically of the most annoying things about Unity. Most stuff you have to do it menus with mouse clicks, maybe you'll have to do the same series of forty repetitive mouse clicks in a row. I'm more use to writing a vim macro to get tasks like this done in 10 seconds. The yaml files it generates absoultely everywhere are stupidly huge, specifying every single default. This makes version control of said files very challenging. The merge conflicts can be impossible to deal with and lead to someone having to redo some work. Why can't each yaml file contain a single "version" flag which is associated with a set of default values, and then just leave all those defaults values out of the yaml? It would be more readable and less prone to version conflicts.

The user-interface and yaml files may suck but when it comes to the coding, I really like how everything is structured. I love that you write C#, it's a really great language, the API overall is really good, especially when it comes to collision detection and implementing custom physics. If the user-interface was even a third as good as the coding side then Unity as an overall would be twice as good.

I foresee having a hundred hours wasted by Unity being annoying, but that will still be less time than it'll take to write the four items I described above. I'm still not sure which will be more fun, or less painful. If I give up on Unity I will have just spent time learning a technology that is basically useless to me if I don't like it. I'm only 60% sure going with Unity is the right option and I wish it were better.

We've also decided to call this game Super Fighting Team for now but that will almost definitely change. Our name `chilon.net` works okay for a web development studio but it's not great for a game development company, so we're naming our game development section: Super Frolic Team.
