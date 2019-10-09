---
title: Devlog Three
summary: Mechanics
date: "2019-10-09"

reading_time: false # Show estimated reading time?
share: false # Show social media stuff?
profile: false # Show author profile?
comments: false # Show comments?

# Optional header image (relative to 'static/img/' folder).
header:
  caption: ""
  image: ""
 
---  
 
# Preceding Thoughts

Before I start working on the game in earnest, there are a few things I've needed to consider relating to how the game will function both mechanically and thematically. I also have to consider the societal implications of my work. Do I think the conditions of Irish immigrants in the 19th century is a controversial, hot-button issue? No. But I do think a lot of the questions I intend to address _are_ - such as race, class, immigration, revolution, and violence. I don’t intend to make a didactic experience that beats its participants over the head with any overt message, and while I don’t intend to condone the Shiner’s historical actions I do think that the experience is going to be at least sympathetic towards them.

## Foundations

I'm intending to make a text game, which leaves me a lot of options. I've chosen Twine. It's software I'm familiar with, and the fact it exports as raw HTML means that it's both compatible with all sorts of devices and is not reliant on a service provider for upkeep. Furthermore, it can be saved and downloaded as a local file, which makes it extremely easy to disseminate and maintain.

The course requires some sort of focus on the interconnectivity of physical and digital space, and after some trial-and-error this has left me with a couple options: either implement geolocation into the game, or implement visual cues that need to be obtained from the real-world environment in the style of a scavenger hunt. For example, to be able to perform a certain action, they could either physically place themselves inside the space which was once Corktown and use geolocation to confirm their presence, or they could input textual cues (such as a street name or the last words of a memorial plaque) to confirm their presence. The latter is more 'fun', and opens up options for people without data plans and who may be living outside Ottawa, and avoids the use of Twine's geolocation, which is reportedly lacking in percision.

## Mechanics

I already have a pretty solid idea for how I want the game to play out. The player is going to start as an Irish immigrant in Bytown, 1830, as work is finishing on the Rideau Canal. I find myself quickly running up against the issue of gender. From my research the Shiners were overwhelmingly male - and while they may have had support and encouragement from the Irish community's women, there are no reports of them taking any into their ranks. In order to ensure that the players can directly participate in the escalating acts of violence committed by the Shiners, it makes most sense to allow the player to exclusively play a man - due to the strict social conventions at the time, choosing to play as a woman would likely delegate the player to being an outside observer of this violence rather than an active participant. Of course, that's only if I honestly portray the strict gender roles of the past - I could always play a little fast and loose with history. I'm going to bring this up in class and perhaps seek some outside input.

The player is going to have several needs that influence their overall mood, or stress: Wealth, Health, Family, Social, Fervor. As these stats deteriorate, so will the player's overall state. When all these needs are well-maintained, the player character will be in a good mindset, and will generally prefer kinder, less violent solutions to their problems. However, as these needs deteriorate, the player character's mood state will decrease. They will become progressively more desperate, which will result in their actions becoming increasingly drastic and violent. Traditional text adventures allow players to choose for their characters - but in this case, I'm only going to let players choose what the character does in their off time - how they manage their needs. When it comes to the hard decisions - whether to join a riot or stay home with the kids - the character is going to make the choice for the _player_, depending on their stress levels. I think this is an interesting twist on the traditional mechanics of a choose-your-own-adventure, and helps develop my theme of what drives communities to violence.
