---
layout: post
title: Operation HEAR
description: A journal of attempts to engineer an underwater hearing solution.
keywords: underwater, waterproof, hearing aid, deaf
---

Last updated: 8/29/2016

# Introduction
Since I was a kid, I've wished for a way to hear while in the water. As of 2016, there is only one [waterproof hearing aid](http://www.siemens.com/press/en/pressrelease/?press=/en/pressrelease/2012/healthcare/h20121036.htm) on the market. Someday I would like one but for now, this is my journal of trying to figure something more cost-effective :) 

# 12/29/2015
Got fitted with [Resound Enzo<sup>2</sup>](http://www.resound.com/en-US/hearing-aids/enzo2). This hearing aid has actually been life-changing. It is [Made for iPhone®](https://developer.apple.com/programs/mfi/) and routes sound from my phone directly into my hearing aid's internal microphone via Bluetooth. For the first time, I could Skype and not have to ask my friends to constantly repeat themselves because the max volume wasn't loud enough.

# 8/05/2016
Went tubing with my friends! I had taken out my hearing aids for tubing in a lake before, but this trip was a 3-hour trip down a lazy river. We would essentially be chilling and talking the entire time. I didn't want to be left out so I wore my old pair from high school. I figured that if something happened to them, I'd still have my pair from undergrad and the ReSounds. The trip turned out to be a blast, my friends tied up our tubes together and blasted music while talking. 

![River tubing](/images/river-tubing.jpg)
*Image from Trinity River Vision Authority.*

# 8/19/2016
Hatched crazy idea of using iPhone as a microphone and pairing it to waterproof bluetooth headphones. Then I simply enclose my iPhone in a waterproof case and swim with it. I had already gotten the case during tubing and discovered that I could still talk on the phone. My phone's internal microphone could pick up sound even in a watertight case. Of course, this depends on the case actually working and me not destroying my phone in the process.  

Apps that can turn the iPhone into a microphone are many! Preliminary testing using my hearing aids as bluetooth headphones reveals that the internal iPhone microphone is surprisingly good and can switch from near and far range. I turned off my hearing aid's external microphone so that the only sound came from the iPhone's internal microphone. I could hear my parents yelling my name from downstairs and hold a conversation with them in the car and at the dinner table. 

Sound quality is extremely polluted. There is a lot of ambient / background noise and it is annoyingly loud. My voice sounds disturbingly different, I can't describe it. My parents also sound different.

Overall, results are optimistic and this idea looks possible.

# 8/20/2016
Research waterproof ratings. Apparently they are on an "IPX" scale from 0 (zero protection) to 8 (fully waterproof).

| Level | Protection                                           |
|-------|------------------------------------------------------|
| 6     | Can withstand water jets at 100 liters/min for 3 min |
| 7     | Immersion up to 1 meter for 30 minutes               |
| 8     | Continuous immersion up to 3 meters                  |

Ordered a pair of [IPX7 Bluetooth earbuds](https://www.amazon.com/gp/product/B01G8JO5F2/). 

# 8/22/2016

Bluetooth headphones arrive. Comfortable and tightly snug in ear. 

The range is fine, I can hear a noise when my parents are yelling my name from downstairs. Sound quality... beyond salvageable. It sharply degrades with distance, with speech intelligibility at 3 feet, but unintelligible beyond 1 meter. It is difficult to discern changes in pitch and tone. These results are puzzling considering how well this worked when I paired my hearing aids.

Further investigation shows that the iPhone is automatically using the microphone in my bluetooth headphones instead of its own internal microphone. This seems to be the default behavior; there is no existing method to choose which microphone my phone uses. I tried several [hearing algorithms](http://petralex.pro/en/article/view?id=1): Petralax, NAL, Berger, and POGO. I generally prefer POGO, but in all cases they failed epically.

Exhaustive search for all IPX6, IPX7, and IPX8 wireless headphones without a built-in microphone. There are none. 

Since trials using my hearing aid worked well, I think this should still work if I can force my phone to use its internal microphone. To be sure, I'll repeat tests using wired earbuds.

# 8/23/2016

I borrowed my dad's Apple earbuds.

Results were even better than expected! As predicted, my iPhone used its internal microphones to pick up audio and routed it through my earbuds. The sound quality was the pleasant surprise. In tests with my hearing aid, I complained about how annoying the background noise was. Here, there was no background noise simply by virtue of the fact that I couldn't hear it. My hearing aid has a built-in amplifier that boosts all sound, but normal wired earbuds don't have such a thing. The only volume control would come from the iPhone, and it turned out that the only audio I could hear were sounds above background noise, i.e. spoken audio and people yelling. 

My thoughts were confirmed by this test: I just need to figure out a way to remove the microphone profile from my bluetooth headphones. That, or find waterproof wired earbuds which might be easier. For now I still have a couple weeks before I go anywhere but I ordered a [waterproof case](https://www.amazon.com/gp/product/B01243EJ7A/) that has an armband and a place to plug in earbuds. It also floats, so that will be useful.


# 8/24/2016

Mmm, I looked for waterproof earbuds today and found the following candidates:

[ insert table ]

I think that wired earbuds will be the easiest solution but I'm still hung up on trying to make this work with bluetooth. That brings up a new question: what is the underwater range of bluetooth?

### Preliminary Research

Bluetooth is a wireless technology standard that operates on ultra high frequency radio waves. In essence, it transmits signals through electromagnetic radiation but things get tricky when moving from air to water. Signal loss can occur through:

* transmission loss from reflection and refraction at the air/water boundary
* propagation loss due to water's high permittivity and electrical conductivity 

I think the first case shouldn't be an issue since my headphones would already be in the water. [Zeng](https://open.library.ubc.ca/cIRcle/collections/ubctheses/24/items/1.0220823) does a survey of underwater wireless communication in seawater and finds that scattering is low at long wavelengths like RF (radio frequency), so that leaves the second case. Water's high permittivity reduces any electric field around it, which is problematic since electromagnetic waves propagate via disturbances in the electric (and magnetic) fields. 

![Visualization of EM propagation](/images/em-propagation.gif)
*Image from [Physics Classroom](http://www.physicsclassroom.com/mmedia/waves/em.cfm)*

Radio frequencies like Bluetooth suffer from high attenuation - its intensity decreases sharply upon contact with water molecules. [Rhodes](http://www.hydro-international.com/content/article/underwater-electromagnetic-propagation) explains this process,

> Loss is largely due to the effect of conduction on the electric field component. Propagating waves continually cycle energy between the electric and magnetic fields; hence conduction leads to strong attenuation of electromagnetic propagating waves.

Saltwater has a high conductivity while freshwater has a relatively low conductivity. This means that it'll be more challenging to engineer a hearing solution for snorkeling in the ocean compared to swimming in a lake. 

It turns out that Bluetooth has virtually nil connectivity. [Jiang and Georgakopoulos](http://file.scirp.org/pdf/JEMAA20110700001_18390291.pdf) show that the optimum frequency for air-to-water communication is short-wave radiowaves in the 3 to 100 MHz range. In contrast, Bluetooth is almost two orders of magnitude bigger, falling under the spectrum of microwaves at 2.4 to 2.4835GHz. Anyone who's had a good middle school science teacher will remember that kitchen microwaves heats food by heating the water molecules, which absorbs the microwaves.

Wireless frequencies that do work underwater include sonar and NFC. Apple implemented NFC chips in iPhone 6 for Apple Pay, but have banned access by third party apps. Regardless, it's a moot point since NFC headphones are so few and not at all waterproof. If I hope to use my phone, then bluetooth it'll have to be.  

For my purposes, I don't really *need* a big range. If I am swimming with waterproof earbuds, then that's a max depth of one foot. [Mišković et al.](http://bib.irb.hr/datoteka/686678.Miskovic_et_al_final_paper.pdf) found thatunder calm sea conditions, bluetooth connection could be established at depths of fewer than 15cm.

It is actually REALLY hard to find published results about underwater bluetooth range. You'd think this would be a common question - and it is - but I guess since it is so ineffective that few sought to quantify it.

# 8/25/2016

Today, I spent a lot of time looking at forums for R/C submarines and... I am actually kinda appalled by how much misinformation there was. Some posters would attribute the ineffectiveness of Bluetooth to the resonant frequency of water, [which is incorrect](http://www.schoolphysics.co.uk/age16-19/Wave%2520properties/Wave%20properties/text/Microwave_ovens/index.html). I didn't know anything just a few days ago, but it is problematic when veteran posters propagate incorrect information to newbies. Luckily, this is the Internet, and there is always somebody rushing to prove people wrong.


# 8/26/2016

### Theoretical Bluetooth Underwater Range

I'm still hung up on this underwater bluetooth range question. What is it REALLY? I have about two weeks left of summer vacation and I PROMISED myself I wouldn't do any math, but here we go...

Radio frequency power is expressed in decibels. We can calculate the maximum distance using the formula for [free-space path loss](https://en.wikipedia.org/wiki/Free-space_path_loss) as:

$$ \begin{align} 
\text{FSPL}_{dB} &= 10\log_{10}\left(\left( \frac{4\pi d}{c}^2\right)\right) \\
&= 20\log_{10}(d) + 20\log_{10}(f) + 20\log_{10} \left( \frac{4\pi}{c}\right) \\
&= 20\log_{10}(d) + 20\log_{10}(f) - 147.55
\end{align} $$

(Actually, this isn't a good formula, but it was my easiest starting point.) If we measure frequency in GHz instead of Hz, the equation becomes,

$$\begin{align}
\text{FSPL}_{dB} &= 20\log_{10}(d) + 20\log_{10}(f \cdot 10^9) - 147.55 \\ 
&= 20\log_{10}(d) + 20\log_{10}(f) + 20\log_{10}(10^9) - 147.55 \\
&= 20\log_{10}(d) + 20\log_{10}(f) - 32.45
\end{align}$$

Rearranging the equation above to find distance, we get

$$d = 10^{\frac{1}{20}\left(FSPL - 20\log(f) - 32.45\right)}$$

Bluetooth frequency is a known value, but what about the path loss? [Jiang and Georgakopoulos](http://file.scirp.org/pdf/JEMAA20110700001_18390291.pdf) look at wireless signal loss in fresh water, producing the following graph of propagation loss at various depths. 

![Propagation loss of electromagnetic waves](/images/propagation-loss.png)

Bluetooth is around 2.4 GHz and I am not looking to go deep, so the solid line at 10<sup>9</sup> Hz (or 1GHz) is what I'm interested in. A depth of 0.5m is, in American, 1.6 feet. It looks like the propagation loss is about 25 dB. 

Now we can substitute the values into the equation above to get the theoretical distance: 

$$\begin{align}
d &= 10^{\frac{1}{20}\left(25 - 20\log(2.4) - 32.45\right)} \\
&= 0.1767 \text{ m}
\end{align}$$

Thus, our theoretical range in freshwater is 17.67 centimeters. [Lloret et al.](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3355409/) achieved bluetooth connectivity at average depths of 16-17 cm in a swimming pool filled with freshwater, which is pretty close to the theoretical calculations.

# 8/27/2016

Now that I have a theoretical (and empirical) distance of bluetooth range in freshwater, it seems pretty pointless to extend this result to seawater. 16 cm is about 6.3 inches, so my head would be just under the surface of the water before I lose connectivity. If I can just modify my headphones such that my phone doesn't recognize a microphone, then I should have bluetooth audio without the sound quality problem.

# 8/28/2016

### Hacking Attempts

Today, I tried to hack and reprogram my bluetooth headphones. [Senso ActivBuds](https://www.amazon.com/gp/product/B01G8JO5F2) use Bluetooth v4.1+EDR, which stands for Enhanced Data Rate. Bluetooth devices interact with each other through "profiles," and the profiles that Apple supports are [here](https://support.apple.com/en-us/HT204387). It looks like my headset might have the [HFP profile](https://developer.bluetooth.org/TechnologyOverview/Pages/HFP.aspx). Now the question is: is there an [A2DP profile](https://developer.bluetooth.org/TechnologyOverview/Pages/A2DP.aspx) as with wired headphones?

To see which profiles are on my ActivBuds, I downloaded Bluetooth Explorer (in [Hardware IO Tools for Xcode](https://developer.apple.com/download/more/)) and paired the ActivBuds to my laptop. 

![ActivBuds profiles](/images/activbuds-profiles.png)

From the picture above, we see that it supports the HFP protocol (as predicted), but also [A2DP Sink](https://developer.bluetooth.org/TechnologyOverview/pages/a2dp.aspx), which is the profile for receiving a digital-audio stream delivered from a source.

After some more digging, I suspect that it has a [CSR635](http://www.csr.com/products/csr8635) chip. According to its [technical specs](http://www.csr.com/sites/default/files/csr8635_qfn_technical_overview.pdf), it has a transmit power of 8dBm and receiver sensitivity of -89dBm. [ElectronicDesign](http://electronicdesign.com/communications/understanding-wireless-range-calculations) calculates wireless range using these two numbers but I don't feel like recalculating anymore. The author does use the FSPL formula that I used, though. 

![ActivBuds Bluetooth protocols](/images/activbuds-protocols.png)

From the picture above, we see the following protocols:

* **[AVDTP](https://en.wikipedia.org/wiki/Bluetooth#AVDTP)**: used to stream music to stereo headsets over an L2CAP channel
* **[RFCOMM](https://en.wikipedia.org/wiki/Bluetooth#RFCOMM)**: generates a serial data stream 
* **[AVCTP](https://en.wikipedia.org/wiki/Bluetooth#AVCTP)**: used by the remote control profile to transfer AV/C commands, e.g. music control buttons

This is all I've found so far for today. I don't know anything about engineering so it's taken a lot of time reading through documentation and figuring out what to look for. I haven't found a guide that tells you how profiles get put on bluetooth "modules" (chips) -- there might not even be one. I'm feeling pretty discouraged about being able to hack my ActivBuds. 

### Turn of Events

On the bright side, waterproof case showed up today! It has a line-in for plugging wireless earbuds in and they worked pretty well. Then I wondered if the iPhone would stay in A2DP profile if I plugged in my Apple earbuds while having the Senso ActivBuds paired. The answer is no.

But then all of a sudden, I heard my mom talking on the phone! While ActivBuds were in! I paid attention and realized I could distinguish what she was saying. Until now, I had only been testing these things with NPR Radio and TED Talks from my computer and those tests had failed epically. 

I was using the [Petralex](https://itunes.apple.com/us/app/petralex-hearing-aid/id816133779) amplifier. There is also the [HearYouNow](https://itunes.apple.com/us/app/hearyounow-your-personal-sound/id569522474) which performed awfully - I still couldn't hear my mom talking. However, this was the app that performed best with the Apple earbuds. Really interesting. 

Maybe I might not have to do any tweaking on the ActivBuds after all. Tomorrow morning I'm going to visit my mom's workplace and I'm going to try the ActivBuds again with the Petralex app in real-time.





