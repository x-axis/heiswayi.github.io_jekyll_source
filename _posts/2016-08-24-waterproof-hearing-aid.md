---
layout: post
title: Operation HEAR
description: A journal of attempts to engineer an underwater hearing solution.
keywords: underwater, waterproof, hearing aid, deaf
---

Last updated: 8/26/2016

## Introduction
Since I was a kid, I've wished for a way to hear while in the water. As of 2016, there is only one [waterproof hearing aid](http://www.siemens.com/press/en/pressrelease/?press=/en/pressrelease/2012/healthcare/h20121036.htm) on the market. Someday I would like one but for now, this is my journal of trying to figure something more cost-effective :) 

## 12/29/2015
Got fitted with [Resound Enzo<sup>2</sup>](http://www.resound.com/en-US/hearing-aids/enzo2). This hearing aid has actually been life-changing. It is [Made for iPhone®](https://developer.apple.com/programs/mfi/) and routes sound from my phone directly into my hearing aid's internal microphone via Bluetooth. For the first time, I could Skype and not have to ask my friends to constantly repeat themselves because the max volume wasn't loud enough.

## 8/05/2016
Went tubing with my friends! I had taken out my hearing aids for tubing in a lake before, but this trip was a 3-hour trip down a lazy river. We would essentially be chilling and talking the entire time. I didn't want to be left out so I wore my old pair from high school. I figured that if something happened to them, I'd still have my pair from undergrad and the ReSounds. The trip turned out to be a blast, my friends tied up our tubes together and blasted music while talking. 

<center>
![River tubing photo](/images/river-tubing.jpg)
*Image from Trinity River Vision Authority.*

</center>

## 8/19/2016
Hatched crazy idea of using iPhone as a microphone and pairing it to waterproof bluetooth headphones. Then I simply enclose my iPhone in a waterproof case and swim with it. I had already gotten the case during tubing and discovered that I could still talk on the phone. My phone's internal microphone could pick up sound even in a watertight case. Of course, this depends on the case actually working and me not destroying my phone in the process.  

### Preliminary Testing

Apps that can turn the iPhone into a microphone are many! Preliminary testing using my hearing aids as bluetooth headphones reveals that the internal iPhone microphone is surprisingly good and can switch from near and far range. I turned off my hearing aid's external microphone so that the only sound came from the iPhone's internal microphone. I could hear my parents yelling my name from downstairs and hold a conversation with them in the car and at the dinner table. 

Sound quality is extremely polluted. There is a lot of ambient / background noise and it is annoyingly loud. My voice sounds disturbingly different, I can't describe it. My parents also sound different.

Overall, results are optimistic and this idea looks possible.

## 8/20/2016
Research waterproof ratings. Apparently they are on an "IPX" scale from 0 (zero protection) to 8 (fully waterproof).

| Level | Protection                                           |
|-------|------------------------------------------------------|
| 6     | Can withstand water jets at 100 liters/min for 3 min |
| 7     | Immersion up to 1 meter for 30 minutes               |
| 8     | Continuous immersion up to 3 meters                  |

t ### Preliminary Research

Bluetooth is a wireless technology standard that operates on ultra high frequency radio waves. In essence, it transmits signals through electromagnetic radiation but things get tricky when moving from air to water. Signal loss can occur throughs:

* transmission loss from reflection and refraction at the air/water boundary
* propagation loss due to water's high permittivity and electrical conductivity 

I think the first case shouldn't be an issue since my headphones would already be in the water. That leaves the second case. Water's high permittivity reduces any electric field around it, which is problematic since electromagnetic waves propagate via disturbances in the electric (and magnetic) fields. 

<center>
![Visual representation of electromagnetic propagation](/images/em-propagation.gif)
*Image from [Physics Classroom](http://www.physicsclassroom.com/mmedia/waves/em.cfm)* 
</center>

Radio frequencies like Bluetooth suffer from high attenuation - its intensity decreases sharply upon contact with water molecules. [Rhodes](http://www.hydro-international.com/content/article/underwater-electromagnetic-propagation) explains this process,

> Loss is largely due to the effect of conduction on the electric field component. Propagating waves continually cycle energy between the electric and magnetic fields; hence conduction leads to strong attenuation of electromagnetic propagating waves.

Saltwater has a high conductivity while freshwater has a relatively low conductivity. This means that it'll be more challenging to engineer a hearing solution for snorkeling in the ocean compared to swimming in a lake. 

It turns out that Bluetooth has virtually nil connectivity. [Jiang and Georgakopoulos](http://file.scirp.org/pdf/JEMAA20110700001_18390291.pdf) show that the optimum frequency for air-to-water communication is short-wave radiowaves in the 3 to 100 MHz range. In contrast, Bluetooth is almost two orders of magnitude bigger, falling under the spectrum of microwaves at 2.4 to 2.4835GHz. Anyone who's had a good middle school science teacher will remember that kitchen microwaves heats food by heating the water molecules, which absorbs the microwaves.

Wireless frequencies that do work underwater include sonar and NFC. Apple implemented NFC chips in iPhone 6 for Apple Pay, but have banned access by third party apps. Regardless, it's a moot point since NFC headphones are so few and not at all waterproof. If I hope to use my phone, then bluetooth it'll have to be.  

For my purposes, I don't really *need* a big range. If I am swimming with waterproof earbuds, then that's a max depth of one foot. [Mišković et al.](http://bib.irb.hr/datoteka/686678.Miskovic_et_al_final_paper.pdf) found thatunder calm sea conditions, bluetooth connection could be established at depths of fewer than 15cm.


It was actually REALLY hard to find published results about underwater bluetooth range. You'd think this would be a common question - and it is - but I guess since it is so ineffective that few sought to quantify it.  

### 8/23/2016

Today, I spent a lot of time looking at forums for R/C submarines and... I am actually kinda appalled by how much misinformation there was. Some posters would attribute the ineffectiveness of Bluetooth to the resonant frequency of water, [which is incorrect](http://www.schoolphysics.co.uk/age16-19/Wave%2520properties/Wave%20properties/text/Microwave_ovens/index.html). I didn't know anything just a few days ago, but it is problematic when veteran posters propagate incorrect information to newbies. Luckily, this is the Internet, and there is always somebody rushing to prove people wrong.


### 8/25/2016

I'm still hung up on this underwater bluetooth range question. What is it REALLY? I have about two weeks left of summer vacation and I PROMISED myself I wouldn't do any math, but here we go...

Radio frequency power is expressed in decibels. We can [calculate the maximum distance](https://en.wikipedia.org/wiki/Free-space_path_loss) as:

$$ \begin{align} 
\text{FSPL}_{dB} &= 10\log_{10}\left(\left( \frac{4\pi d}{c}^2\right)\right) \\
&= 20\log_{10}(d) + 20\log_{10}(f) + 20\log_{10} \left( \frac{4\pi}{c}\right) \\
&= 20\log_{10}(d) + 20\log_{10}(f) - 147.55
\end{align} $$

If we measure frequency in GHz instead of Hz, the equation becomes,

$$\begin{align}
\text{FSPL}_{dB} &= 20\log_{10}(d) + 20\log_{10}(f \cdot 10^9) - 147.55 \\ 
&= 20\log_{10}(d) + 20\log_{10}(f) + 20\log_{10}(10^9) - 147.55 \\
&= 20\log_{10}(d) + 20\log_{10}(f) - 32.45
\end{align}$$

Rearranging the equation above to find distance, we get

$$d = 10^{\frac{1}{20}\left(FSPL - 20\log(f) - 32.45\right)}$$


[Jiang and Georgakopoulos](http://file.scirp.org/pdf/JEMAA20110700001_18390291.pdf) look at electromagnetic wave propagation in fresh water. The graphs below shows the propagation and transmission loss at varying depths as frequency increases. 
![Figure of propagation loss in water](/images/propagation-loss.png)
*Figures from [Jiang and Georgakopoulos](http://file.scirp.org/pdf/JEMAA20110700001_18390291.pdf), page 263*

Bluetooth is around 2.4 GHz, which is 
The solid line at 10<sup>9</sup> Hz (or 1GHz) is what I'm interested in. A depth of 0.5m is, in American, 1.6 feet. It looks like the propagation loss is about 25 dB. 




