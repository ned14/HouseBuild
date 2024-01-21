The house exterior and site will be mainly illuminated by RGBWW LED strips which each have a five pin connector:

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

- 5x 5m 3500K CRI95 LED strip 11w/metre.

    - 3x for roof of living area above TV.
    - 1x for end of hallway.
    - 1x for back of games room.

All likely using the recessed LED channels below.

- 1x 5m 4000K CRI95 waterproof LED strip 28.8w/metre.

    - Upstairs bathroom where we needed an ultra bright
strip to uplight. Had wanted 3500K but couldn't get
that in waterproof. Couldn't get 3000K either, only 2800K,
so ended up going for 4000K which is disappointing but water
under the bridge now.

- 1x 5m 3000K CRI95 ultra bright LED strip 38.4w/metre.

    - Top of stairs around grandfather clock. This is beyond
ultra bright, more like insanely bright. Idea here is to uplight
from below so it will be reflecting back down.

- 1x 5m 3000K RA90 RGBWW COB LED strip.

    - Sauna.

- 2x 5m 3700K COB LED strip 15w/metre.

    - Additional lighting around both ground floor showers.
Not waterproof, but it'll be inside recessed channels and
it's COB so it should be fine.

- 1x 5m 4000K RA95 COB LED strip 10w/metre.

    - Ground floor bathroom mirrors MISSING STRIP FOR ONE
MAYBE TWO.

- 24x 3000K CRI90 MR16 bulb 120 degree 7w.

    - Accidentally got ten too many. Anywhere needing a
wide cosy throw where people are standing e.g. hallways,
utility, bathrooms.

    - These were very cheap (under €1 delivered), and appear to
have no heatsink at all. They get hot quickly at full power,
and will need PWM dimming to get much lifespan from them. They are
marked 'Gatetop' but that's the Aliexpress shop front name, most
of the MR16 bulbs on Aliexpress are likely from the same manufacturer.

- 8x 3000K CRI90 MR16 bulb 38 degree 7w.

    - Mainly bedrooms, the warmest colour we use.

    - These were very cheap (under €1 delivered), and appear to
have no heatsink at all. They get hot quickly at full power,
and will need PWM dimming to get much lifespan from them. They are
marked 'Gatetop' but that's the Aliexpress shop front name, most
of the MR16 bulbs on Aliexpress are likely from the same manufacturer.

- 15x 3500K CRI90 MR16 bulb 40 degree 8w.

    - Living spaces where high CRI matters.

    - These are called "expensive Satco" below. They were about US$12
each. They dim very smoothly over a large range, have clearly superior
heatsinking, and their power regulator doesn't care about input voltage
which suggests a fully switched power converter. These are clearly the
best bulbs I bought on all measured metrics, but at 15x the cost of
the very cheap Aliexpress ones I'd wonder if there is cost benefit.

- 12x 3500K CRI80 MR16 bulb 40 degree 6w.

    - Living spaces where lower CRI can be tolerated.

    - These are called "cheap Satco" below. They were about US$9
each, three quarters the price of the expensive Satco. They have at least
some heatsinking compared to the very cheap Chinese bulbs resulting
in temperatures a few degrees lower, but otherwise seem very similar
i.e. they get hot fast, and may even have an inferior driver IC to those
very cheap bulbs (see below).

- 16x 4000K CRI90 MR16 bulb 38 degree 7w.

    - Anywhere needing focus and concentration i.e. kitchen
countertops, home office.

    - These were very cheap (under €1 delivered), and appear to
have no heatsink at all. They get hot quickly at full power,
and will need PWM dimming to get much lifespan from them. They are
marked 'Gatetop' but that's the Aliexpress shop front name, most
of the MR16 bulbs on Aliexpress are likely from the same manufacturer.

- 24x fixed 3cm recessed downlight fixtures.

    - Hallways, kitchen countertops.

- 36x tiltable 3cm recessed downlight fixtures.

    - Everywhere else.

- 27x 0.5m recessed aluminium LED strip channel for 8mm wide tape.

- 30x 0.5m recessed aluminium LED strip channel for 12mm wide tape.

- 10x 0.5m double sided aluminium LED strip coving.

- 10x 0.5m brushed black skirting channel for LED strip.

- 10x 0.5m brushed rose gold skirting channel for LED strip.

- 10x 6 amp two pole DC circuit breakers.

- 10x 6 amp one pole DC circuit breakers.

- 28x 12 AWG mini car fuse leads.

- 25x 8 kHz DC PWM wall dimmer switches.

    - Verified with oscilloscope these genuinely do run an 8 kHz
PWM. They're actually configurable between 500 Hz, 1 kHz, 2 kHz,
4 kHz and 8 kHz. This turns out to be super useful when paired
with the MR16 bulbs, which expect clipped AC to tell them when
to dim.

- 2x 4 Khz DC PWM wall dimmer switches.

    - Bought in case the 8 kHz switches didn't work out as samples.
Turns out the 8 kHz switches work great.

- 4x touchpanel RGBW wall dimmer switches.

    - Only need one, but bought spares as they were very cheap
and I don't trust the touch interface at all to be reliable.

## PWM dimming

### MOSFET choices

For some reason, the 5v "logic level" IRLxxx MOSFETs don't seem to come on convenient breakout breadboards, only the 10v IRFxxx MOSFETs do (note the 'L' vs 'F' difference). This is unfortunate, however what I really would want is 3.3v MOSFETs so I can skip the logic level shifter which is added cost and wiring (that said, what max frequency an affordable 3.3v MOSFET could switch at I don't know).

The two choices of MOSFET on convenient breakout boards and which are cheap are chinese clones of the IRF520N and IRF540N, both 10v saturating devices. Both allow a reasonable current for a 5v saturation, albeit considerably less than the maximum current they are capable of. I guess this is why "they'll do" for most makers.

I have a bunch of single channel IRF520N boards from my initial round of purchasing in 2021, and one of those powers the experimental LED strip cover lighting in the living room of my rented house. It works pretty well, albeit the MOSFET does run hot i.e. wastes energy.

To see if I could improve on this, I bought 10x cheap four channel IRF540N MOSFET boards to test if that single integrated board would be feasible and save me hassle wiring up individual MOSFETs. These are optically isolated apart from ground, and have a LED wired inline to the MOSFET input which roughly lops half a volt off the signal voltage. They present a common anode, and switch the cathode only which is perfect for the LED strips. The optocoupler chip (PS2801-4) limits the output voltage to 9 - 80v, as it is powered by the output voltage.

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

### MOSFET control option 4: Use a 24v PWM dimming rotary wall switch

This is the most expensive option, costing €17.20 inc VAT delivered each. Though it also saves on the cost of a wall switch, its single most attractive feature is saving me time. This is actually the one I ended up choosing, despite its expense, as my time is so very limited. I can later upgrade lighting control with ESP32 as needed.

The unit I bought claimed it could work with 12v (the listing claimed 5v) to 24v at up to 6 amps, with 180 watts specified as maximum (that doesn't make sense to me either). It claims to support five output frequencies: (i) 500 Hz (ii) 1000 Hz (iii) 2000 Hz (iv) 4000 Hz (v) 8000 Hz. This will be useful for working with MR16 bulbs, that expect an AC dimming signal. I couldn't tell from the Aliexpress description if they meant dimming levels, or PWM frequency (later I used an oscilloscope to check, and they did mean PWM frequency, these switches do use a 8000 Hz PWM frequency when so configured).

Having received them and cracked one open, they are based on two 60N03 MOSFETs. The MOSFETs can cope with up to 30v and their control signal is TTL, and the datasheet reckons they can push up to 320 watts. There is a TM1651 LED driver control IC, but it is for the eight segment number display only. An unmarked IC appears to do all the real work. A 78L05 voltage regulator takes in 0 - 30v and outputs 5v, its datasheet says it needs a minimum 7.5v to produce 5v. With 5v input it produces 3.5v, which is above TTL so a lot of ICs should still work. All the ICs with identifiers I could see their datasheets all say they're happy at 3.3v, so only the unmarked IC will be the question. I ended up putting it onto my variable voltage power supply, it appears (just about) happy at 5.0v albeit with the numbers display rather dim, but 4.8v is too little and it hangs. The numbers display appears to reach full brightness at around 8v, so I suspect its needs 5v from that voltage regulator for full brightness but is happy down to TTL.

After empirical testing, I have found:

- The very cheap Chinese MR16 bulbs have no issue being put into series, which to be honest was rather the surprise. Each claims 10v for itself minimum, one of the other bulbs takes the balance, it all 'just works'.
- The Satco bulbs don't like being put into series at all. One goes out, the other gets full voltage.

The dimmer switch PWMs the cathode, so you get a series of pulses connecting to ground. Unfortunately the MOSFET boards above are anode switched, with a pull up resistor you can invert the dimming setting, but that's hardly ideal.

I could install special 54v => 12v converters throughout the house and put the Satco bulbs in parallel, however I already have lots of 54v => 24v converters in stock and they're more efficient in any case. It seemed above that the Satco bulbs don't mind 24v input:

- The AMC7105 MR16 driver IC will accept between 4.0v and 40v.
- The iW3662 MR16 driver IC will accept between 10.0v and 24v.
- The MAX16840 MR16 driver IC will accept between 5.6v and 46v.
- The MAX31840 MR16 driver IC will accept between 6.5v and 26v.
- The TPS92560 MR16 driver IC will accept between 6.5v and 42v.

These seem to be the most common MR16 LED driver ICs, and they all accept 24v.

**Unfortunately** from thermal camera testing of the very cheap Chinese MR16 bulbs it would seem the higher the input voltage, the much more heat gets output which means bulb lifetime will be impacted, so using 24v throughout for those is probably unwise. Whatever IC they use it appears to treat 10v as 100% brightness, and it performs a dim down to about 4v -- anything above 10v appears as increased heat dissipation (even 12v), so they might even have a linear regulator in there to save costs. I saw a max temp of 60 C on 10v with it going to 72 C on 12v, it went to 80 C before I pulled the plug on 24v. Unfortunate.

For the cheap Satco, it was a similar story to very cheap Chinese bulbs: more voltage equals more heat, but the heatsinking is slightly better. The 24v bulb went to 90 C within a few minutes, the 12v bulb got to 58 C. Dimming is smooth between 3.6v and 10v, I couldn't see brightness change 10v to 12v.

For the expensive Satco, they are completely idempotent to input voltage. On both 12v and 24v they reach 46 C and stay there. Identical. They turn on quite brightly at 3.6v which is the lowest my variable power supply can go, and have a smooth dim from there right up to 12v which appears to mean 100% for them. In PWM dimming testing these bulbs had by far the widest dimming range, going from just above off smoothly to full brightness. I very much like the colour of the light from the bulbs, they're generally just lovely. I guess you get what you pay for, and the cheap Satco are actually lousy value for money considering they're barely better than the 'Gatetop' Aliexpress bulbs at one tenth their price.

I guess what all this means is I'm going to need a bunch more ~60v DC to 10v DC converters (more likely it'll be 12v). Let's hope the January sales have hefty discounts.

For sizing:

- Very cheap Chinese use ~0.44 amps at 12v. As you drop the voltage below 10v, amps also drops with voltage as they dim. They claim to be a 7w bulb, that clearly is usual Aliexpress 'listing claims 25% over reality' at 5.3w at most.
- Cheap Satco use ~0.56 amps at 12v. As you drop the voltage to 8v they will ramp up amps to 1 amp, after which they dim whilst holding current constant. They claim to be a 6.5w bulb, however they actually consume as much as 8w and run at 6.72w normally. These really are poor bulbs, consuming up to 8w when their box claims 6.5v is unacceptable.
- Expensive Satco use ~0.60 amps at 12v. As you drop the voltage to 10.6v they will ramp up amps to 0.73 amp, after which they dim whilst holding current constant. They claim to be an 8w bulb, however they never exceed 7.7w and run at 7.2w normally.
- I didn't mention it above as I only have a couple of them so not worth the testing time: a 'Goodlite' 3500K 7w MR16 bulb uses 0.61 amps at 12v, which is 7.3w. These are different again, as you drop the voltage they keep ramping current upwards to compensate, with an apparent constant current cap at 1.15 amps, after which they dim.

So tl;dr; you need to budget one amp per bulb worst case if they're connected in parallel. So five bulbs could draw 5 amps of 12v.
