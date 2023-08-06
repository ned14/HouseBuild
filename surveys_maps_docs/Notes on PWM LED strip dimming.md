The house interior and site will be mainly illuminated by RGBWW LED strips which each have a five pin connector:

1. Common anode +24v
2. Red
3. Green
4. Blue
5. Warm white (3200K)

## Exterior

The exterior LED strips have already been purchased:

- 50x 5m IP67 Tube Waterproof 24v SMD 5050, 60 LEDs/metre
    - To be used edges of house fascia, edges of site.
    - Listing claimed max 12w/metre and 350-450 mcd/LED. Likely 20% worse.
    - Probably max 72w 3.0 amp on the anode.
    
- 4x 5m 1P67 Tube Waterproof 24v **double row** SMD 5050, 120 LEDs/metre
    - To be used where more brightness is needed e.g. western wall outhouse passage, inside of shipping container
    - Listing claimed 16w/metre and 18-20 lumen/LED. Empirical testing found 20w/metre (listing was 20% under this), and 2,200 lumen/metre from subjective sight seems generous.
    - Max 100w 4.2 amp on the anode, may be able to get more brightness if both ends are wired in as the common anode will limit max current. Strictly speaking only the +24v common anode needs wiring in at both ends.

## Interior

Not decided nor purchased yet (nor will be until house build completed)

## PWM dimming

### MOSFET choices

For some reason, the 5v "logic level" IRLxxx MOSFETs don't seem to come on convenient breakout breadboards, only the 10v IRFxxx MOSFETs do (note the 'L' vs 'F' difference). This is unfortunate, however what I really would want is 3.3v MOSFETs so I can skip the logic level shifter which is added cost and wiring (that said, what max frequency an affordable 3.3v MOSFET could switch at I don't know).

The two choices of MOSFET on convenient breakout boards and which are cheap are chinese clones of the IRF520N and IRF540N, both 10v saturating devices. Both allow a reasonable current for a 5v saturation, albeit considerably less than the maximum current they are capable of. I guess this is why "they'll do" for most makers.

I have a bunch of single channel IRF520N boards from my initial round of purchasing in 2021, and one of those powers the experimental LED strip cover lighting in the living room of my rented house. It works pretty well, albeit the MOSFET does run hot i.e. wastes energy.

To see if I could improve on this, I bought 10x cheap four channel IRF540N MOSFET boards to test if that single integrated board would be feasible and save me hassle wiring up individual MOSFETs. These are optically isolated apart from ground, and have a LED wired inline to the MOSFET input which roughly lops half a volt off the signal voltage. They present a common anode, and switch the cathode only which is perfect for the LED strips. The optocoupler chip limits the output voltage to 9 - 80v, as it is powered by the output voltage.

Assuming that the chinese clone MOSFETs have these characteristics:

<table>
<thead><th><th>IRF520N<th>IRF540N
<tbody>
<td align="right">R<sub>DS</sub><td>0.20<td>0.052
<td align="right">R<sub>thJA</sub><td>62<td>62
<td align="right">Max I<sub>D</sub> for<br>V<sub>GS</sub> @ 4.5v<td>2.5 A<td>20 A
<td align="right">Max I<sub>D</sub> for<br>V<sub>GS</sub> @ 5.0v<td>4 A<td>32 A
<td align="right">Max I<sub>D</sub> for<br>V<sub>GS</sub> @ 10v<td>9.7 A<td>33 A
</tbody>
</table>

Heating in watts = Current ^ 2 * R<sub>DS</sub>

Resulting temperature increase over ambient = Heating watts * R<sub>thJA</sub>

Where R<sub>DS</sub> is for a control voltage of 10v and the MOSFET's temperature is 20 C:

<table>
<thead><th>Current<th>IRF520N watts<th>IRF520N temp<th>IRF540N watts<th>IRF540N temp
<tbody>
<td>0.63 A<td>0.08 W<td>+5.0 C<td>0.02 W<td>+1.3 C
<td>1.00 A<td>0.20 W<td>+12 C<td>0.05 W<td>+3.2 C
<td>2.00 A<td>0.80 W<td>+50 C<td>0.2 W<td>+13 C
<td>2.50 A<td>1.25 W<td>+78 C<br>(needs cooling)<td>0.33 W<td>+20 C
<td>4.00 A<td>3.20 W<td>+198 C<br>(needs cooling)<td>0.82 W<td>+52 C
</tbody>
</table>

One would multiply watts and temp heating by 1.5 if the temperature were 100 C, so clearly the IRF520N runs away with waste heat past 2.0 A or so. One probably ought to also increase the heating to account for a control voltage of 4.5v vs 10v.

I have a IRF520N on the living room LED strip which I think draws about 2.2 A, and it gets really quite hot even with its heatsink. With hindsight it was the wrong choice of MOSFET for such a high current, but at the time I didn't know any better.

In any case, I reckon the four channel IRF540N boards should waste no more than 0.4 W of heat from the four MOSFETs if the LED strip is fully on for the 120 LEDs/metre strips, and 0.16 W for the 60 LEDs/metre strips. Given that each ESP32 board and its associated 60v to 24v converter will waste single digit watts, I don't think the losses from the MOSFETs will matter (and they won't need heatsinking either).

### MOSFET control option 1: Use direct PWM

The industrial ESP32 boards can PWM dim up to twelve channels, so theoretically up to three 5m LED strips can be controlled per board. In practice, most use cases will have an ESP32 board per two LED strips, as the other GPIO will be used for I2C sensors etc.

Probably a 14,648Hz PWM will be used, which gives 4,096 steps per RGBW channel. You need to make sure when introducing logic level shifters or optoisolaters etc that they are capable of switching at at least that frequency. Any bog standard FET based level shifter should be capable of 100 Khz, if you need more then a buffered level shifter such as the TXS0108E should be good up for 2 - 60 Mhz which should be enough to level shift even a SPI connection.

As inferred here, you will need a level shifter with this option, because the FET needs a 5v control signal to saturate. Whilst inexpensive, the level shifter boards each need soldering and wiring in with two sets of power and control signals and this is hassle. If one has other 5v peripherals, this might be okay, but to be honest it's rare I'd choose a peripheral without 3.3v control support, even if it a 5v powered device.

### MOSFET control option 2: Use a PCA9685 LED driver

These cost under €3 inc VAT delivered and provide sixteen i2c controlled PWM channels with 4,096 steps per channel. They can output 5v whilst being controlled by 3.3v, which saves on level shifters. ESPHome treats them as if ESP32 PWM outputs, so integration is seamless and you can of course daisy chain them as they are i2c devices. The only bad thing about them is that they probably still need soldering (though all the Aliexpress photos show them presoldered), and their maximum PWM clock is 1,526Hz which is unfortunately low (flicker).

### MOSFET control option 3: Use a TLC5947 LED driver

These cost under €7 inc VAT delivered and provide twenty-four SPI controlled PWM channels with 4,096 steps per channel. They can output up to 30v at 30mA, and work just fine with 3.3v control. They have a 4Mhz clock, which is surely sufficient, and can be daisy chained on SPI.

In case you're thinking we could have them drive a higher voltage than 5v into the MOSFETs to save heat wastage, yes you can. But we only have available 24v or 5v, and the MOSFETs won't take more than 20v into their input without burning out.

As with all the other options, these also need soldering, but the fact you can run eight LED strips from each board and with good quality dimming is attractive.
