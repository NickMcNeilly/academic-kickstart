---
title: Devlog Five
summary: More Progress
date: "2019-10-23"

reading_time: false # Show estimated reading time?
share: false # Show social media stuff?
profile: false # Show author profile?
comments: false # Show comments?

# Optional header image (relative to 'static/img/' folder).
header:
  caption: ""
  image: ""
 
---  
 
## Busywork


It's been a productive week. I've been focusing on getting the core gameplay loop implemented, as well as all the required features. You can see the overall gametree below:

![Overview](/static/img/DevlogFive.PNG)

Currently I've implemented: Player stats (wealth, health, family, social, state), family stats (hunger, health), a day/night cycle, working for money, a store where you can buy food and medicine, custom names for yourself and your family, a player home, disease & medicine, a church where you can pray against disease, family death, and player death.

To get a sense of what the code within these passages looks like, here's the current code in the 'Sleep' passage that handles disease: 	

~~~~
<<nobr>>
/* Disease */
<<set _pDiseaseHit to random(100)>> <<set _wDiseaseHit to random(100)>> <<set _sDiseaseHit to random(100)>> <<set _dDiseaseHit to random(100)>>

<<switch $medQuality>>
<<case 8>>
<<set _medPower to 45>>
<<case 7>>
<<set _medPower to 40>>
<<case 5>>
<<set _medPower to 25>>
<<case 4>>
<<set _medPower to 20>>
<<case 2>>
<<set _medPower to 5>>
<<case 1>>
<<set _medPower to 0>>
<</switch>>

/* PLAYER ILLNESS */

<<if _pDiseaseHit <= 50 and $illness is false>> 
You have fallen ill.  <<set $famSick += 1>> <<set $illness to true>> 

<<elseif _pDiseaseHit >= (95 - (_medPower / 2)) and $illness is true>> <<set $illness to false>> You are no longer sick. <<set $famSick -= 1>><</if>>

/* WIFE ILLNESS */

<<if $wAlive and _wDiseaseHit <= 10 and $wHealth is 3>> 
$wife has fallen ill.  <<set $famSick += 1>> <<set $wHealthDis -= 10>> 

<<elseif $wAlive and _wDiseaseHit <= (10 - (_medPower / 5))>> $wife's condition worsens. <<set $wHealthDis -= 5>>

<<elseif $wAlive and _wDiseaseHit >= (95 - _medPower) and $wHealth isnot 3>> <<set $wHealthDis += 10>> <<if $wHealthDis > 20>> $wife is no longer sick. <<set $famSick -= 1>> <<else>> $wife's condition improves. <</if>> <</if>>

/* SON ILLNESS */

<<if $sAlive and _sDiseaseHit <= 10 and $sHealth is 3>> 
$son has fallen ill.  <<set $famSick += 1>> <<set $sHealthDis -= 10>> 

<<elseif $sAlive and _sDiseaseHit <= (10 - (_medPower / 5))>> $son's condition worsens. <<set $sHealthDis -= 5>>

<<elseif $sAlive and _sDiseaseHit >= (95 - _medPower) and $sHealth isnot 3>> <<set $sHealthDis += 10>> <<if $sHealthDis > 20>> $son is no longer sick. <<set $famSick -= 1>> <<else>> $son's condition improves. <</if>> <</if>>

/* DAUGHTER ILLNESS */

<<if $dAlive and _dDiseaseHit <= 10 and $dHealth is 3>> 
$daughter has fallen ill.  <<set $famSick += 1>> <<set $dHealthDis -= 10>> 

<<elseif $dAlive and _dDiseaseHit <= (10 - (_medPower / 5))>> $daughter's condition worsens. <<set $dHealthDis -= 5>>

<<elseif $dAlive and _dDiseaseHit >= (95 - _medPower) and $dHealth isnot 3>> <<set $dHealthDis += 10>> <<if $dHealthDis > 20>> $daughter is no longer sick. <<set $famSick -= 1>> <<else>> $daughter's condition improves. <</if>> <</if>>

<<if $famSick is 0>> Everyone's health remains stable. <<elseif $famSick is 1>> $famSick of you is sick. <<else>> $famSick of you are sick. <</if>>

<<if $illness>> <<set $health -= 10>> <</if>>
~~~~

I'm not a coder by trade, so I apologize to any programmers out there who find themselves in dire need of a barf bag after reading that mess. Simplifying the code above into layman's terms, I can describe what is happening here roughly as follows:

~~~
Recovery power (called _medPower) is determined by the quality of purchased medicine as well as if they player has prayed for health that week.
Prayer gives a much smaller bonus to recovery power than both low-quality and high-quality medicine.

Then, each family member rolls a number from 0 - 100.

Several things can happen, here:
- If they are healthy and roll 10 or higher, they stay healthy.
- If they are healthy and roll under 10, they become sick.
- If the player is sick and rolls above 95*, they are cured.
- If non-player family members are sick and roll under 10*, their health gets even worse.
- If non-player family members are sick and roll over 95*, their condition improves. If this improvement results in their health rising above a certain point, they are cured.

Finally, if the player is sick, after all these calculations are applied their health stat degrades.

* These values are reduced to varying degrees by recovery power. A higher recovery power makes it easier to recover from disease and harder for a disease to worsen.
~~~

These values are still being tweaked for difficulty, but what this essentially results in is a functioning health system. As you and your family become ill, you are encouraged to buy medicine - which is expensive - to help them recover. Failure to do this is likely to result in their illnesses getting worse, leading up to their death. It's rough and unforgiving, as intended.


