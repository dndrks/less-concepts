# less concepts
Brevity may be the soul of wit, but specificity is the death of ambiguity.

The last thing this needs is ambiguity...

## TL;DR

*less concepts* was made using the following items:

```
monome Teletype
Mannequins Three Sisters x2
Mannequins Cold Mac
Mannequins w/ x2
Make Noise Function
Meng Qi DPLPG
M4L custom device based on Rodrigo Constanzo’s karma~
('I had depression for MONTHS' features an Arp Odyssey)
```

The master was wonderfully handled + helmed by Sage Kim at Lacquer Channel Mastering in Toronto, Ontario. I chose Sage based on her excellent treatment of folk material, which manifested nicely in this master -- she unearthed harmonic relationships I had long forgot about and put enough of her fingerprint into the project that I can listen without hearing *myself* in the work.

Extra thanks to Jonny Butler, Kyle Chamberlin, Sean Hellfritsch, Michael Hetrick, and Nick Sanborn for their guidance and feedback through the mastering process + documentation build.

The artwork is an original piece by Racquel Cable. Her work can be found on Instagram under [`@suitcasedog`](https://www.instagram.com/suitcasedog/).

When Racquel and I first moved in together, she graciously let me have the extra bedroom to set up a studio. I was primarily doing laptop stuff, but was trying to save up for the gear listed above. I stapled moving blankets onto the walls. She would work in the living room while I worked in this closed, dark space. It was terrible. Once I got some of the gear listed above, I started joining her in the living room. After a few weeks of this, I thanked her for giving me a zone of my own but ultimately, I wanted to be near her art whenever I made art. So we tore down the blankets, rearranged the stuff, and starting filling the studio with us.

Honestly, this whole thing got a lot easier once that happened.

## Specifics

*less concepts* was recorded between 5/16/2018 - 6/22/2018.

The song titles are (respectfully, if a little tastelessly) stolen from short stories + drawings made by kiddos at the Grand Rapids Art Museum.

The compositional content — rhythms, melodies, harmonies — was all decided in real time by algorithms. This was made possible by Teletype, a small computer-y device that allows a person to code *how* and *when* they want musical events to happen. Among other things, it uses lists to keep track of notes and voltage to communicate with oscillators (the raw voice of a synthesizer).

Teletype is also a platform that’s been heavily developed by the community that uses it (<https://llllllll.co>), through the curation and expansion of its musical code language.

These pieces were created using one of the operators in Teletype’s code: cellular automata. It has been a real, deep joy to explore and I didn’t know much about the science of it before, so here’s an ...

## Excited description of cellular automata!

Picture a grid of white squares. Now imagine a single black square in the top row of the middle column. Cellular automata uses a simple set of if / then conditions to determine whether or not the square directly below that single black square should be white or black, based on the color of the squares to its left and right. These are called neighborhoods.

So, the full set of (square to left / TESTED SQUARE / square to right) neighborhoods would be:

- black BLACK black
- black BLACK white
- black WHITE black
- black WHITE white
- white BLACK black
- white BLACK white
- white WHITE black
- white WHITE white

These neighborhoods (the IF part of the process) stay the same. The *results* (the THEN part of the process) are what change.

So, a rule might be: *if black BLACK black, then the square under BLACK will also be black.*

The end results can be pattern-based, like a fractal, but sometimes things can get really weird and unpredictable. It’s a science that’s been used to model growth systems used in AI, video games, and DNA sequences.

Looks like this:

![Cellular Automata image from Wolfram](http://mathworld.wolfram.com/images/eps-gif/ElementaryCA30_1000.gif)

You can read more about cellular automata in Stephen Wolfram's book: [A New Kind of Science](http://www.wolframscience.com/nks/p170--cellular-automata/)

Fuckin’ wild, right?

## CA, from Ezra
Here’s how cellular automata (hereafter CA) works in Teletype, from Ezra Buchla (@zebra). Ezra developed the CA operator.  

*nb. This is a corrected version of <https://llllllll.co/t/chaos-operators/9785/89>.*

"the behavior is defined by two things:

1. an initial state, say  

```
00100100  
```
and 2) an update rule. the rule says: to get the new value of a state, look at its old value and the value of its previous neighbors. so there are 8 possible configurations to look at, and we specify the desired result for each:

```
input:    111 110 101 100 011 010 001 000
output:    0   0   0   1   1   1   1   0
```

so the rule can be encoded as 8 bits in an integer. wolfram established a convention for doing this, by which the rule written above is equal to `0b00011110 = 0x1e = 30`. so this is referred to in the literature as *rule 30*.

when we apply the rule to the initial state, and keep applying it to subsequent states, we get a sequence

1. 00100100
2. 01111110
3. 11000001
4. 00100011
5. 11110110
6. 10000100  

and so on. (assuming i didn’t mess that up.) (*nb: this version has been corrected.*)

(by the way, in this implementation i am wrapping the edges; they could also be fixed. different behaviors; both are chaotic.)

these states likewise can be encoded as 8-bit integers. that representation is what the operator produces at its output and accepts as its input. i agree that it doesn’t make the output super intuitive; i think this structure is most useful when you can map the output bits to gates, which makes this an extremely fun sequencer."

## Egoity, from Georg

"Because man does not experience the Seeker, the Thinker, the Experiencer in his presentness, he needs property, success, self-assertion -- confirmation that he *is*. Instead of experiencing himself as a *thinker*, which is certainly possible, he seeks to convince himself of his existence from the outside, and that brings him to the habit of self-feeling. But man can only feel himself because of *something* -- everything that serves him in this way, everything important and 'necessary,' everything he clings to. Finally other men begin to serve the same purpose for him, and this determines his relationship to them. Position, power, money, and recognition form his world, on which he is dependent, and in which he has continually to make an effort to prove himself, to be certain of his own existence."

Georg's last name is Kühlewind, which translates to "cool wind."

Fuckin' wild, right?

## How to make this album at home

When I describe this process to folks -- even folks who work with this type of hardware -- it can be hard to illustrate. There's the music (the artifact) which doesn't *totally* reveal the mechanics. And then there's the maths which don't *totally* reveal the value of using algorithms to make musical decisions.

To help marry the process and the results, I've made some accompanying software for you to download along with this album. It's also called *less concepts* and it looks like this:

![less_concepts_screenshot](/doc_images/main.png?raw=true)

The core compositional process that made this album can be achieved with this device. It's a pretty close port of how I use the CA operators in Teletype, so rather than talk about some hardware you might not have, let's talk about some software that you *can* have if you want to have it!

(Even if you don't download it, I think the following visuals might be fun.)

## Won't you be my neighbor?

To begin, let's pick a **rule** (the result of the neighborhoods test) and a **seed** (an initial state).

In the **rule** box, type `30` and hit 'enter'.  
In the **seed** box, type `36` and hit 'enter'.  
(These are the examples from Ezra's explanation.)

In the **rule as binary** section, you'll see `00011110`, which is the **rule** integer `30` in binary.

Keeping the sequencer off, hit the **iterate** button to convert the **seed** integer to binary:

![iterated](/doc_images/bits1.png?raw=true)

`36` == `00100100`

Using the neighborhoods, the device scans the binary sequence in clusters of three. As Ezra explained, the scanning wraps the edges -- so the first `0` is actually *the middle* value in a cluster that begins with the rightmost `0`.

Using the neighborhoods, let's find the next iteration manually:  
`000` returns `0`  
`001` returns `1`  
`010` returns `1`  
`100` returns `1`  
`001` returns `1`  
`010` returns `1`  
`100` returns `1`  
`000` returns `0`

So, the resulting binary sequence is `01111110`, which [translates] (https://www.mathsisfun.com/binary-number-system.html) to `126`. If we hit the 'iterate' button, we see `126` in the iterated value box.


*More iterations*: `193`, `35`, `246`, `132`, `207`, `56`, `100`, `222`, `144`, `249`, `7`, `140`, `219`, `18`, `63`, `224`, `145`, `123`, `66`, `231`, `28`, `50`, `111`, `72`, `252`, `131`, `70`, `237`, `9`, `159`, `112`, `200`, `189`, `33`, `243`, `14`, `25`, `183`, `36` (that's where we started!), `126` (a repeat!!), `193` (a repeat!!!), `35` (a repeat!!!!), `246` (a repeat!!!!!)

We’ve entered a loop! Excellent.

Just for shits, open up the 'visual: rules 0 to 99' and find rule `30`. As you explore *less concepts*, you'll find that the visuals help as jumping-off points, but do not get trapped into thinking that a pattern which appears simple is not worth exploring.

## Another cool wind

"The more concentratedly an object can be thought about, and the more unimportant and uninteresting it is, then the more awake thinking becomes.

The things that seem to exist *before* our knowing them are results of a knowledge not yet conscious of itself, a process of knowing we normally sleep through.

The exercise is being performed correctly if one can forget oneself as one practices.

This point can suggest how far concentratedness is a moral question. Can a person surrender him or herself utterly to a theme, or are the ulterior motives, side thoughts? Concentratedness in this sense means improvisation at the same time, because in concentrated thinking it is impossible to work from memory or consult a notebook on what thoughts to think next. Thinking relies altogether on its present activity -- it can only improvise. *Concentration therefore means improvisation*."

## Returns

Alright, so we've got a device that spits out lists of what seem like random numbers, but what’s cool is that these numbers start to *repeat*. This means they’re not necessarily "random," but are the dependable results of iterations of 65,536 possibilities. What makes them feel "random" is that I can’t *predict* the results.

Most importantly, this means I can’t attach my ego to the result, because I don’t really know what it’s going to be. At best, I can guess and observe.

Let’s do something with the results.

## Multi-tasking

Clicking into the dropdown menu, you will see a list of scales, starting with 'ionian' (major).

If you keep it on 'ionian' and hit the 'open' button, you'll see two columns of numbers. On the right, you'll see the steps of the scale:

![scales_screenshot](/doc_images/scales.png?raw=true)

Each of these numbers occupy an index position in our Tracker, beginning with a 0th position. The *position* is the number on the left of the semicolon.
e.g.: ‘7’ is in the **4th** position, ’17’ is in the **10th** position, ‘0’ is in the **0th** position.

```
position:  0  1  2  3  4  5  6   7   8   9   10  11  12  13
note data: 0  2  4  5  7  9  11  12  14  16  18  19  21  23
```

To aid useful expressivity and exploration, we are going to limit the range of our seed growth. Instead of letting it jump around from 0 - 255, which might make for a lot of chaotic tones (which *less concepts* can do, if that's your thing!), we can scale that range down.

Note the 'lower scale limit' and 'upper scale limit' number boxes. These numbers represent range we want to limit our growth to. This is dynamic, so please experiment!

For now, let's keep our lower scale limit at 0 and our upper scale limit at 13. Translating a few iterations of the CA sequence from earlier to (scaled + rounded) Tracker positions, with a seed of `36`:  

```
CA sequence: 36 126 193 35 246 132 207 56
scaled pos.:  2   6   9  1  12   6  10  3
```

Translating these scaled down Tracker positions to actual major scale degrees...  

```
scaled pos.:  2   6   9  1  12   6  10  3
note data:    4  11  16  2  21  11  17  5
``` 

What was once a jumble of generally-unpredictable-but-eventually-repeating numbers are now a repeating sequence of notes!

*In review:*  
- we started with CA to generate "random" numbers, ranging from 0-255  
- we chose a musical scale  
- we took those CA results and scaled them down to 0-13 to seek through the Tracker positions  
- the major scale degrees in each position becomes our melody line

## Last bits...

**Choice**: It’d be rad if there were direct relationships between pitches and rhythms.  
**Solution**: Use the binary representation of each iterated value to determine whether or not the note it sequences is heard.

Binary’s most basic application is for on/off messages; 1 = on and 0 == off.  
So, basically, each iterated value is just a series of on/off messages.

To explore this, let's turn on the the **seq** in the top right + set the **ms** rate to **190**.

If you'd like, open up your DAW and select two MIDI instruments (or plug in two instruments that accept USB MIDI). If working within a DAW, tell each instrument to listen to 'less concepts 1' and 'less concepts 2'. In *less concepts*'s **midi to** section, send blue bits 'from less concepts 1' and red bits 'from less concepts 2' (or to the USB MIDI instruments you have plugged in, if you went that route).

*nb. You can also change the MIDI channel 'less concepts' sends each bit stream to in the bottom-right section of the UI.*

You should have the other parameters already set from our guided exploration, but just in case let's go with:

- scale: ionian
- lower scale limit: 0
- upper scale limit: 13
- rule: 30
- seed: 36

With the **seq** on, you should see the seed growing + eventually, looping back onto itself.

Choose a blue bit and the instrument receiving the blue **midi to** will start sounding. Same with the red.

![iterating_bits](/doc_images/iter_bits.png?raw=true)

Changing the bits will reveal new melodic phrases, harmonies and rhythms, as they are gating a master pattern. This type of subtractive composition is in line with Caterina Barbieri's [brilliant approach](https://www.soundonsound.com/news/interview-minimalist-electronic-artist-caterina-barbieri).

To hear the entire sequence through a channel, simply hit the **all** button to the left of its bit stream.

All that remains is the **global oct**ave, **global s/t** and **red oct**ave settings, which can deepen/broaden expressivity. It can be fun to offset the **red oct** to handle bass notes, with bit gates that are less active. In this way, *less concepts* offers creative workarounds to two-voice sequencing on monophonic synths.

## Removing the self, seeking the 'I'

What’s really exciting to me about this process is that it doesn't allow for the same direct ownership over melody, harmony and rhythm as when I sit down to "compose." Here, as I make structural choices, the weight ego fades. The whole process is now mostly *observation*. This shifts the traditional dynamic of this whole thing.

The link between "composer" and "being who seeks to convince himself of his existence from the outside" pivots toward a more healing "catalyst" and "observer".

I can now watch choices manifest without fear or self-consciousness.  
I’m listening and responding, not exerting control and judging (myself; the music; worthiness; imposter status; expressions of genre; how I’m seen, by whom; an audience I’ve yet to even engage that I assume an awful lot about when I’m worrying + “Writing Music”).

All of these pieces are moments where I connected emotionally to the material as listener – that’s the whole impetus for sharing them. They’re these wonderful + odd accidents that just fucked me right up on some level. Sharing them is a hope that they can be similarly heard and felt by others.

I get to be another Seeker, Thinker, Experiencer -- not Credit-Seeking Jag.

The real fun of this (which has to be the only quality that really matters) is in dialogue.

My involvement is simply to ascribe meaning to patterns. And that's really what *people* do best. So, just let the machine make the patterns. Have fun. Have less concepts.
