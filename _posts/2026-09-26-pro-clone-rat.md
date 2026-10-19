---
layout: post
title: "Pro Clone Rat"
author: "Aloys"
categories: diy, pedal
tags: [about]
---

I recently started building small effects pedals for my synthesizers at first, then my musician friends started asking if they could have their own. I got a request for a clone of the Pro Co Rat, a famous distortion guitar pedal. We wanted to keep it cheap, so I decided to use what I had on hand.

## Schematic

The first part of designing a new circuit is the schematic. Finding a good Pro Co Rat schematic is not hard, in fact, ElectroSmash did a [full deep dive](https://electrosmash.mas-effects.com/proco-rat.html) into explaining the circuit. This is the best starting point for any mod!

![Pro Co Rat schematic by ElectroSmash](assets/img/pro-clone-rat/pro-co-rat-schematic-parts.jpg)

My idea for this mod is to replace the LM308 operational amplifier with a TL072 and the 2N5458 FET with a more common BJT like the 2SC1815. Some passive component values will also be slightly changed, again to make use of the components I already have on hand.

![LM308 compensation network](assets/img/pro-clone-rat/lm308-compensation.png)

The original LM308 uses an external compensation capacitor to control its frequency response and stability. The TL072 has internal frequency compensation, so this external compensation network is not required and can therefore be omitted.

I also added a 10 nF decoupling capacitor close to the TL072 supply pins to reduce high-frequency supply noise and provide local current decoupling. The capacitor should be placed as close as possible to the power pins. 

Finally, in the gain stage, I replaced the 560 Ω resistor with a 510 Ω one, which slightly shifts the cutoff frequency of the associated high-pass filter. As shown in the following plot, the change has little effect on the overall frequency response and the two cutoff frequencies are clearly visible around 1.5 kHz and 60 Hz.

<div style="display: flex; gap: 10px;">
  <img src="{{ '/assets/img/pro-clone-rat/gain_stage_circuit.png' | relative_url }}" style="width: 45%;">
  <img src="{{ '/assets/img/pro-clone-rat/gain_stage_bode_comparison.png' | relative_url }}" style="width: 45%;">
</div>

A [Bipolar junction transistor](https://en.wikipedia.org/wiki/Bipolar_junction_transistor) needs a base current to operate as an emitter follower. Since the circuit already provides a 4.5 V bias voltage, I can use this voltage to bias the transistor's base through a high-value resistor.

I chose to bias the transitor's base with a 1 MΩ resistor. The choice keeps tha load on the 4.5 V bus low and provides enough base current to put the transistor in linear region.

The final schematic is shown below:

![Pro Clone Rat schematic](assets/img/pro-clone-rat/Pro-Clone-Rat-Schematic.png)

## Layout

I recently came across this [website](https://stripboard-editor.com/) for creating stripboard layouts. In particular, I wanted to try its new layout generator to save me some time. I ran the solver and moved some inputs and outputs around to get the following layout.

<div style="display: flex; gap: 10px;">
  <img src="{{ '/assets/img/pro-clone-rat/layout_top.png' | relative_url }}" style="width: 45%;">
  <img src="{{ '/assets/img/pro-clone-rat/layout_bottom.png' | relative_url }}" style="width: 45%;">
</div>

## Conclusion

I hide a lot of mistake in this article that I plan to correct in future iterations of this design. Also, I would like to modify it further and remove the output transistor to use 2 opamps in the TL072. The current filter is not great and I could change it for the Bif Muff tone circuit to make it better.

Anyway, here is a picture of the finished product, hope you found this interesting !

<div style="display: flex; gap: 10px;">
  <img src="{{ '/assets/img/pro-clone-rat/finished_in.jpg' | relative_url }}" style="width: 45%;">
  <img src="{{ '/assets/img/pro-clone-rat/finished_out.jpg' | relative_url }}" style="width: 45%;">
</div>