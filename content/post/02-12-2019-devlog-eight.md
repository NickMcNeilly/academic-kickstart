---
title: Devlog Eight
summary: Nearing Completion
date: "2019-11-01"

reading_time: false # Show estimated reading time?
share: false # Show social media stuff?
profile: false # Show author profile?
comments: false # Show comments?

# Optional header image (relative to 'static/img/' folder).
header:
  caption: ""
  image: ""
 
---  
 
## Finale

![Overview](/img/Devlog8.PNG)

The game is done. Well, the first pass, at least - it still needs to be playtested. There are currently three acts to progress through: Act 1 for the Rideau Canal construction phase, Act 2 for when the player is out of work and lacks a reliable source of income, and Act 3 is when the Bytown Shiners come into fruition as a gang - which the player may or may not align themselves with. Now it's just a matter of playtesting and getting a few more eyes on the project. I'm too close to the project deadline to make any broad, sweeping changes - but tweaks are still very much possible. Bugs are going to be inevitable, unfortunately, but that's the case with any digital project.

The game now has both a win state and a lose state. You lose the game if you die - simple enough. You win the game if you make it all the way to the end without dying. Also very simple. There's a slight scoring system included, but I tried to avoid making it overtly 'gamey'. Instead of mention of numerical scores or the like, I tried to focus on giving descriptive responses to player performance. I'm not particularly sure why this is - I haven't shied away from describing it as a game, or using gameplay elements like player stats. It simply felt more natural to have a less gamified ending. I've also gotten rid of the numerical identifiers in the stats screen to make it less obvious how well the player is doing, and make the algorithm of the game loop less easy to figure out.

Though I haven't talked about much in this devlog, that's mostly because things have gone according to plan. I've added a whole new chapter, which is also the densest of the three. In all, I'd say this step of progress is second only next to the initial mechanical setup phase of Devlog 5, which involved constructing the foundation for everything that lay ahead.
