---
layout: post
title:  Taming Unity
date:   2019-03-03 19:30:00
categories: C# Unity SuperFightingTeam
---

Three weeks later, I'm pretty happy we switched to Unity for this project. There are several parts of Unity that I don't use but thankfully Unity itself can be modified with code and you can substitute most components out with your own code.

## Animation
Unity provides a pretty nice visual method of building animations but it involves much mouse clicking and waving around of the mouse. While it provides a lot of power to non-coders, it is also fiddly and time-consuming to use.

I built a custom animator driven by `ScriptableObject`s that describe each character's animations and then I use an editor script to generate those `ScriptableObject` instances from a `yaml` file. The animator code uses a co-routine which yields the next animation for each `Update()` allowing a declarative style of describing animations that provides the same benefits of Unity's animator work-flow only via code.

Here is what one of the animations in the project looks like:
```yaml
  animation: 0-5,0-5,0-3,6-8@6
```

That shows sprites 0 through 5, then sprites 0 through 5 again, then sprites 0 through 3, followed by sprites 6 through 8, with each sprite being shown for 6 frames. On unity this would involve 38 input boxes, 19 of which need you to drag a sprite into them and 19 which `6` must be entered into. To fill it out for one animation takes a few minutes, to fill it out for a thousand animations would take several days.

Here's another:
```yaml
  animation: 0,1,0@2 l,2-7@4
```

This shows sprite 0, then sprite 1, then sprite 2, each for 2 frames. Then it shows sprites 2-7 for 4 frames each in a loop until the animation is stopped.

## Building sprites
Unity has a pretty great spritesheet editor but it also involves much waving around of the mouse and much clicking which felt like a waste of time.

To get around this I also use `yaml` and an editor script:
```yaml
- name: anna
  sprites:
    - name: standing
      animation: 0-5,0-5,0-3,6-8@6
    - name: dashing
      pivots:
        - range: 0-1
          x-offset: 7
      animation: 0,1,0@2 l,2-7@4
```

The names in the `yaml` pertain to two spritesheets, `anna-standing.png` and `anna-dashing.png`. The pivot for each sprite within the sheet is assumed to be the center but the `overrides` section above can be used to adjust the offset for specific sprites. The script that builds the sprites scans the images and automatically determines how to split it up into several sprites based on the standard character sprite size.

## Moving on

Now I never have to touch Unity's animator or spritesheet editor UI I'm much happier, I'm tackling problems with code instead of the mouse. I've got the basics of my custom physics sorted out and have a fully animated character running around a tile-based platforming level. Next I need to work on improving the animations, some basic combat, platforms characters can "jump up through", platforms that can push/carry characters and jumping off of platforms.
