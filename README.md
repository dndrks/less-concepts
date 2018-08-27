# less_concepts
Brevity may be the soul of wit, but specificity is the death of ambiguity.

The last thing this needs is ambiguity...

## Specifics

These five pieces were recorded from 5/16/2018 - 6/22/2018.

Their titles are respectfully stolen from short stories + drawings made by kiddos at the Grand Rapids Art Museum.

Their compositional content — rhythms, melodies, harmonies — were all decided in real time by algortihms. This was made possible by Teletype, a small computer-y device that allows a person to code how and when they want musical events to happen. Among other things, it uses lists to keep track of notes and voltage to communicate with oscillators (the raw voice of a synthesizer).

Teletype is also a platform that’s been heavily developed by the community that uses it (<https://llllllll.co>), through the curation and expansion of its musical code language.

These pieces were created using one of the operators in Teletype’s code: cellular automata. It has been a real, deep joy to explore and I didn’t know much about the science of it before, so here’s an **overly excited description**:

Picture a grid of white squares. Now imagine a single black square in the top row of the middle column. Cellular automata uses a simple set of rules to determine whether or not the squares around + below that single black square should be white or black, based on how many squares around it are white or black. The same rules are applied to the squares around + below, and again and again, down all the rows. The end results can be pattern-based, like a fractal, but sometimes things can get really weird and unpredictable. It’s a science that’s been used to model growth systems used in AI, video games, and DNA sequences.

Looks like this:

![Cellular Automata image from Wolfram](http://mathworld.wolfram.com/images/eps-gif/ElementaryCA30_1000.gif)

You can read more about cellular automata in Stephen Wolfram's book: [A New Kind of Science] (https://www.wolframscience.com/nks/)

Fuckin’ wild, right?

## CA, from Ezra
*Here’s how cellular automata (hereafter CA) works in Teletype, from Ezra Buchla (@zebra). Ezra developed the CA operator.  
This is a corrected version of <https://llllllll.co/t/chaos-operators/9785/89>.*

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

Georg's last name is Kühlewind, which means "cool wind."

Fuckin' wild, right?

## How to make this album at home

The way that cellular automata has been implemented in Teletype, you begin by choosing a rule and an initial state (seed). Then, call the function to run the rule through subsequent states. The timing of this is determined by you, using the metronome / clock in Teletype.

To demonstrate this process, I've made some accompanying software for you to download along with this album. It looks like this:

![less_concepts_screenshot](https://github.com/dndrks/less_concepts/blob/master/doc_images/whole.png)

The core compositional process that made this album can be acheived with this device. It's a pretty close port of how I use the CA operators in Teletype, so rather than talk about some hardware you might not have, let's talk about some software that you *can* have if you wanna!

## Won't you be my neighbor?

In the **rule** box, enter `30`.  
In the **seed** box, enter `36`.  
(These are the examples from Ezra's explanation.)

You should see the **rule as binary** change as the function converts the **rule** integer to binary:

![rule_seed](https://github.com/dndrks/less_concepts/blob/master/doc_images/seed.png)

`30` == `00011110`

Keeping the sequencer off, hit the **iterate** button to convert the **seed** integer to binary:

![iterated](https://github.com/dndrks/less_concepts/blob/master/doc_images/bits.png)

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

## Another cool breeze

"The more concentratedly an object can be thought about, and the more unimportant and uninteresting it is, then the more awake thinking becomes.

The things that seem to exist *before* our knowing them are results of a knowledge not yet conscious of itself, a process of knowing we normally sleep through.

The exercise is being performed correctly if one can forget oneself as one practices.

This point can suggest how far concentratedness is a moral question. Can a person surrender him or herself utterly to a theme, or are the ulterior motives, side thoughts? Concentratedness in this sense means improvisation at the same time, because in concentrated thinking it is impossible to work from memory or consult a notebook on what thoughts to think next. Thinking relies altogether on its present activity -- it can only improvise. *Concentration therefore means improvisation*."

## Returns

Alright, so we've got a device that spits out lists of what seem like random numbers, but what’s cool is that these numbers start to *repeat*. This means they’re not necessarily "random," but are the dependable results of iterations of 65,536 possibilities. What makes them feel "random" is that I can’t *predict* the results.

Most importantly, this means I can’t attach my ego to the result, because I don’t really know what it’s going to be. At best, I can guess and observe.

Let’s do something with the results.

## Multi-tasking

While Teletype performs the CA process, it can also store lists of numbers in a Tracker which can be read on demand and sent as note data to an oscillator.

These are in our device in a dropdown menu, starting with the ionian/major scale:

![scale_stuff](https://github.com/dndrks/less_concepts/blob/master/doc_images/scale.png)

If you hit the 'open' button, you'll see two columns of numbers. On the right, you'll see the steps of the scale:
`[0,2,4,5,7,9,11,12,14,16,17,19,21,23]`

Each of these numbers occupy an index position in the Tracker, beginning with a 0th position. These are the leftmost number.  
e.g.: ‘7’ is in the **4th** position, ’17’ is in the **10th** position, ‘0’ is in the **0th** position.

**Choice**: I want to use CA to crawl these Tracker positions.  
**Barrier**: Teletype’s CA operator naturally returns values between 0 and 255 and I only have 14 positions, 0 through 13.  
**Solution**: I can compress the range of 0 through 255 to 0 through 13, to make it easier for the CA to return useful results when it crawls the Tracker positions.

That's the 'lower limit' and 'upper limit' number boxes -- the range we want to compress down to. This is dynamic, so please experiment!

Translating a few of the CA sequence from earlier to (rounded) Tracker positions, with a seed of `36`:  

```
(CA -> Tracker position)
 
36 -> 2  
126 -> 6  
193 -> 9  
35 -> 1  
246 -> 12  
132 -> 6  
207 -> 10  
56 -> 3  
100 -> 5  
222 -> 11  
144 -> 7  
249 -> 13  
```

Iterating these results from Tracker position to actual major scale degrees...  

```
position:  0   1   2   3   4   5   6   7   8   9   10   11   12   13
note data: 0   2   4   5   7   9   11  12  14  16  18   19   21   23
```


```
(Tracker position -> note data)  

2 -> 4  
6 -> 11  
9 -> 16  
1 -> 2  
12 -> 21  
6 -> 11  
10 -> 17  
3 -> 5  
5 -> 9  
11 -> 19  
7 -> 12  
13 -> 23 
``` 

What was once a jumble of generally-unpredictable-but-eventually-repeating numbers are now a repeating sequence of notes!

*In review:*  
- we started with CA to generate "random" numbers, ranging from 0-255  
- we entered the notes we wanted to play in Teletype’s Tracker, positions 0-13  
- we took those CA results and scaled them down to 0-13 to seek through the Tracker positions  
- the major scale degrees in each position becomes our melody line

## Removing the self, seeking the 'I'

What’s really exciting to me about this process is that it doesn't allow for the same direct ownership over melody, harmony and rhythm as when I sit down to "compose". Here, I make structural choices, but the weight of 'statement' and ego fade. The whole process is now mostly *observation*. This shifts the traditional dynamic of this whole thing. 

The link between "composer" and "being who seeks to convince himself of his existence from the outside" pivots toward a more healing "catalyst" and "observer".

I can now watch choices manifest without fear or self-consciousness.  
I’m listening and responding, not exerting control and judging (myself; the music; worthiness; imposter status; expressions of genre; how I’m seen, by whom; an audience I’ve yet to even engage that I assume an awful lot about when I’m worrying + “Writing Music”).

All of these pieces are moments where I connected emotionally to the material as listener – that’s the whole impetus for sharing them. They’re these wonderful + odd accidents that just fucked me right up on some level. Sharing them is a hope that they can be similarly heard and felt by others.

I get to be another Seeker, Thinker, Experiencer -- not Credit-Seeking Jag.

The real fun of this (which has to be the only quality that really matters) is in dialogue.

## Last bits...

**Choice**: It’d be rad if there were direct relationships between pitches and rhythms.  
**Solution**: Use the binary representation of each iterated value to determine whether or not the note it sequences is heard.

![iterated](https://github.com/dndrks/less_concepts/blob/master/doc_images/bits.png)

Binary’s most basic application is for on/off messages; 1 = on and 0 == off.  
So, basically, each iterated value is just a series of on/off messages.

Most instruments operate off -> on.  
Their elements (the strings, the pipes, the drum’s skin) are dormant (off) until they are excited or struck (on).  

But synthesizers operate on -> off. Sound is *always* flowing from an oscillator and requires a **gate** to re-orient itself as an off -> on instrument.

(Fuckin' wild, right?)

To turn on the two oscillators in the device, *turn on the DSP* and click each **osc** button:

![osc](https://github.com/dndrks/less_concepts/blob/master/doc_images/osc.png)

These two **osc**illators are gated, so you won't hear any sound.  
Gates can be opened with voltage, which lets sound through.  
When voltage is no longer supplied, the sound is silenced.

To supply "voltage" to the gates, use the **bits to gates** number boxes for each **osc**illator.

We can now use one of the bits in the iterated value's binary to open its own gate!

To hear it all come together, toggle on the **seq**uencer, play around with the **rate**, and adjust the filter to taste!

## end notes

The five pieces of *less_concepts* were made using the following items:

```
monome Teletype
Mannequins Three Sisters x2
Mannequins Cold Mac
Mannequins w/ x2
Make Noise Function
Meng Qi DPLPG
M4L custom device based on Rodrigo Constanzo’s karma~
```

The master was wonderfully handled + hemled by Sage Kim, from Lacquer Channel Mastering in Toronto, Ontario. I chose Sage based on her excellent treatment of folk material, which manifested nicely in her master -- she unearthed harmonic relationships I had long forgot about and put enough of her fingerprint into the project that I can listen without hearing *myself* in the work.

The artwork is an original piece by my partner Racquel Cable. Her work can be found on Instagram under [`@suitcasedog`](https://www.instagram.com/suitcasedog/).

When we first moved in together, she let me have the extra bedroom to set up a studio – I was primarily doing laptop stuff, but was trying to save up for the gear listed above. She would work in the living room while I worked in this closed space and once I got a small skiff together, I started joining her in the living room. It felt so good for us to work in the same space, so I thanked her for wanting to give me a zone of my own but ultimately, I wanted it to be filled with us.

Honestly, this whole thing got a lot easier once that happened.
