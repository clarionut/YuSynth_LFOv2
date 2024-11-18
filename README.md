# YuSynth_LFOv2

My modifications to the [YuSynth LFO version #2](http://yusynth.net/Modular/EN/LFO/VC-LFO2.html).

Alterations include
- changes to some component values to reduce current draw
- an increase in the pulse width range to allow very short (or long) pulses
- a fix for glitches in the pulse wave output at low (< 1-2Hz) frequencies
- a modification of the [fix by Gabbagabi](https://electro-music.com/forum/viewtopic.php?t=69587) for problems adjusting the triangle and sine wave symmetry at both high and low frequency settings
- elimination of the 741 op-amp, replaced by the 'spare' TL074

I recently built a second YuSynth LFOv2 for my DIY modular synthesiser. Having installed ammeters in the synth power supply I've become increasingly conscious of high current draw from some modules, and so modified some of the component values to help reduce this, possibly at the expense of some loss of linearity in the control potentiometers (though I haven't noticed this). I also wanted to be able to produce much shorter pulses than the 20-80% duty cycle range of the original. In both of these modules I eliminated the 741 in the rate/modulation input circuitry, instead using the spare op-amp in one of the TL074s (IC3a in the original circuit).

I found that both modules suffered the problem that it was impossible to set the sine and triangle wave symmetry for both the fast and slow speed settings (selected by switching between two different capacitor values). I eventually found the very clever solution by Gabbagabi on the electro-music.com forum (link above). This allows the gain of the fast and slow settings to be adjusted independently, allowing the symmetry to be adjusted for both speed settings. I fixed both my LFOs using a small daughter board for the extra components. The schematic and proposed PCB layout include these in the design, but do note that I have NOT built an LFO using this exact board layout - please check it carefully if you decide to use it!

An additional issue encountered using the pulse wave output as a sequencer clock was that at low frequencies (less that 1-2Hz) the sequencer would occasionally skip steps. Checking the output on a 'scope showed noise pulses at the start of the high phase of the pulse as the comparator (IC2c in the YuSynth original, U2D in my schematic) switched. Adding a high value positive feedback resistor on this comparator gave very clean switching and no more skipped steps from the sequencer.

The original YuSynth schematic includes a ramp (inverted sawtooth) output via R18. I included this output on my PCB design, but didn't connect it to the panel. It is available if required though.

This is the new procedure for trimming the triangle/sine wave outputs:
- switch the LFO to the FAST (x1) setting
- monitor the TRIANGLE output with a 'scope
- adjust the FAST SAW BIAS trimmer to get a good symmetrical triangle wave
- adjust the SINE/TRI SYM trimmer to remove any DC offset
- check the SINE output is also symmetrical at this point
- switch the LFO to the SLOW (x10) setting and monitor the triangle output
- iteratively adjust the SLOW SAW BIAS and SLOW GAIN trimmers to get a good triangle wave with no DC offset. These trimmers interact with each other, so make small adjustments to be sure you're going the right way. Do NOT touch the SINE/TRI SYM trimmer during this process.

If there's an extreme imbalance between the FAST and SLOW settings you may need to adjust the value of R18 as well.

The kiCad schematic and PCB design use some custom symbols and footprints, so you may need to include the contents of my [kiCad_libraries repository](https://github.com/clarionut/kiCad_libraries).
