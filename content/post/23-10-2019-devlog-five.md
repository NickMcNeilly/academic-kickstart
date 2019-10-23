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

Here's an example of the code in the 'Sleep' Passage
 	

~~~~
<<if $health gt 0>>\
<<nobr>>
You lay your head down and go to sleep, <<if $wAlive is true and $fr gte 3>> with your wife curled up next to you. <<else>> alone. <</if>>

<<if $wAlive is true and $wHealth is 0 or $wAlive is true and $wNeeds is 0>>
<<set $deathFlag to true>> <</if>>
<<if $sAlive is true and $sHealth is 0 or $sAlive is true and $sNeeds is 0>>
<<set $deathFlag to true>> <</if>>
<<if $dAlive is true and $dHealth is 0 or $dAlive is true and $dNeeds is 0>>
<<set $deathFlag to true>> <</if>>
<</nobr>>

After a night's rest, you awaken to start the new day.

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
<</nobr>>
MEDPOWER: (_medPower))
You rolled a: (_pDiseaseHit)
$wife rolled a: (_wDiseaseHit)
$son rolled a: (_sDiseaseHit)
$daughter rolled a: (_dDiseaseHit)
<<nobr>>
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

<</nobr>>

<<if $deathFlag>>[[Something's wrong...|Family Death]]<<else>>[[Get ready for work.|Corktown Hub]]<</if>>

<<set $daytime to true>>
<<set $week += 1>>
<<set $weekFoodBuy to false>>
<<set $weekMedBuy to false>>
<<set $weekPrayed to false>>
<<set $medQuality to 1>>
<<else>>\
<<nobr>>
You lay your head down and go to sleep, <<if $wAlive is true and $fr gte 3>> with your wife curled up next to you. <<else>> alone. <</if>><</nobr>>

[[You don't wake up.|Player Death]]<</if>>
~~~~
