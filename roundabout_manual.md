# roundabout v1.1 manual (in progress)

<img src="https://github.com/MattKuebrich/roundabout/blob/main/images/roundabout_v1.1_board.jpg" width="500">

# explanation of circuit blocks

### VCOs
There are 3 VCOs, 1 with triangle and square outputs and 2 with saw outputs. 

The 4 CV inputs provide increasing levels of modulation, indicated by the white triangle above them. These won't track 1/V per octave. 

Each VCO has 2 sync inputs, one uses a diode and the other an LED. They behave differently (the LED is a bit wilder). Remember: If the signal that's doing the sycning is faster than the oscillator being synced, you won't hear anything. Patch hint: Try patching into both sync inputs!

The "trisq" VCO is fast by default. You can patch the 2 points labeled "medium" or "slow" together to change the speed. It’s equivalent to a 3-way "range" switch. 

## Filter
The filter section is probably the strangest part of the synth. You won't always need something plugged into the filter input, since the filter is very resonant when turned up. The potentiometers controls the resonance, while the cutoff is controlled by patching into the CV-A and CV-B inputs. These effect the 2 different stages of the filter. For the most typical filter behavior patch the same signal into both of them. There are lowpass, bandpass (2 of them), and highpass outputs. Both filters are the same except the 2nd one is tuned higher.

Patch tip: Patching the BP into the left mixer and the HP into the right mixer (from the same filter) can give you a nice stereo effect.

## Divider
There are 2 frequency divider sections. They are separated by a vertical white line that is kind of hard to see. You patch in a clock and get a division from /1 to /16. The output will always be a square wave. 

Patch tip: You can get divisions of /32, /64/, /128 and /256 by patching the /16 output of DIV1 into the clock of DIV2.

Patch tip: insert capacitors between divisions to create some swoooopy modulations. 

## Buffer
This is just an extra buffer. It can be used to overdrive a signal or just buffer a weak signal. For example, the DAC isn't buffered and in certain situations could need to be passed through this buffer.

## R2R DAC
The DAC takes 4 binary inputs and generates a stepped voltage on the output. The 2 output pins are taken from different points in the R2R ladder, so they will be different, but related. 

Patch tip: Feeding the DAC with outputs from the divider section, then using that as CV for an oscillator will generate cool arpeggios.

Patch tip 2: You can use the DAC as an attenuator. You actually patch the signal you want attenuated into the right-most DAC output, then patch out of one of the 4 inputs, which will give you decreasing amounts of attenuation. The filter CV inputs, for example, aren’t weighted like the oscillator CV inputs. This is a way to attenuate the signal before patching into the filter CV. You can also use this as a weighted mixer. Olegtron did a great writeup about the different uses of a R2R in reference to their [R2R Eurorack module](https://www.olegtron.com/olegtron-r2r-1).

## Shift Register
There are 2, 4-bit shift registers. You patch a clock and data pulse into the shift register.

On each clock pulse, if the data input is high, a 1 gets passed into the 1st register. If the data input is low, a 0 gets passed. With each successive pulse, the data gets moved down the registers.

Patch tip: you can "loop" the register by patching the 4th register back into the data input.

Patch tip 2: you can get an 8-bit register by patching the 4th register or SR1 into the data input of SR2 and uses the same clock source for both shift registers.

The shift register clock expects a clean square wave. When feeding it something else (like a triangle, saw or the output of the filter), it can behave inconsistantly, but sometimes that's *cool*. If you want it to work "properly", pass the offending signal through the /1 on the divider before going into the clock. This basically turns any signal into a square wave. 

## Mixer
Like the CV inputs, the mixer inputs provide increasing amplitude as you patch into it, left to right. Actually the 2 ones in the middle are the same amplitude (I found I used them the most), but the left one is the quietiest and the right one is the loudest.

## Ground pins
These allow you to connect multiple roundabouts together. 

# Inspiration 
I referenced, borrowed and learned from a variety of sources for this project. 

The general structure of having simple patchable circuit blocks came from the [Lorre Mille Double Knot](https://lorre-mill.com/doubleknot) and [Elliot Williams' Klangorium](https://github.com/hexagon5un/klangorium).

For the VCOs, I referenced [quite](http://evilturtle.nl/projects/fmdronesynth.htm) [a](https://electro-music.com/forum/topic-28799.html) [few](https://hackaday.com/2015/09/11/logic-noise-playing-in-tune-with-an-exponential-vco/) [different](https://www.youtube.com/watch?v=4qxgwN9aq8E) [sources](http://musicfromouterspace.com/analogsynth_new/WSG2010/wsg_page9.html#PSEUDOCV).

The logic blocks were largely inspired by the awesome ["Logic Noise" series of articles on Hackaday](https://hackaday.com/tag/logic-noise/).

# Design / Production
The circuits were breadboarded and a few things simulated in [Falstad](https://www.falstad.com/circuit/). The PCB was designed in [EasyEDA](https://easyeda.com/) and printed at [JLCPCB](https://jlcpcb.com/). 

# General Parts / Build Notes
Roundabout uses pretty common through-hole parts that can be sourced from [Tayda](https://www.taydaelectronics.com/) and [Mouser](https://www.mouser.com/). In the [BOM](https://docs.google.com/spreadsheets/d/1eRZ8_PK5HJ3nKBCjX_7MApqO0d7YXJZ0Co2NMGjRWOA/), I tried to put alternate parts when applicable. For example, the potentiometers can be any Alpha-style 9mm pot, although I prefer the long Song Huei pots. 

When soldering, I usually starts with components that sit closest to the board first, so the resistors, diodes and capacitors. Then move on to the caps, transistors, LED, and headers. Then do the pots and jacks last. Tip: I like to use sticky tack to keep the headers in place when soldering.

I've been using [recharchable 9v batteries](https://www.amazon.com/Tenergy-Charger-Premium-Rechargeable-Batteries/dp/B00461E85M) for power and they work great, just make sure they are the NiMH ones and NOT the LI-ON ones (they cause the circuit to make an annoying high pitched noise).

# DIY modifications
Todo...
