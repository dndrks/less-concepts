Brevity may be the soul of wit, but specificity is the death of ambiguity.

The last thing this needs is ambiguity...

## Specifics

The five pieces were recorded from 5/16/2018 - 6/22/2018.

The tonal content — rhythms, melodies, harmonies — were all decided in real time by Teletype, a small computer-y device that allows a person to code how and when they want musical events to happen using synthesizers. It uses lists to keep track of notes. It uses voltage to communicate with oscillators (the raw voice of a synthesizer). Teletype is also a platform that’s been heavily developed by the community that uses it, through the addition and expansion of its musical code language.

The five pieces were created using one of the operators in Teletype’s code: cellular automata. It has been a real, deep joy to explore and I didn’t know much about the science of it before, so here’s an overly excited visual description:

Picture a grid of white squares. Now imagine a single black square in the top row of the middle column. Cellular automata uses a simple set of rules to determine whether or not the squares around + below that single black square should be white or black, based on how many squares around it are white or black. The same rules are applied to the squares around + below, and again and again, down all the rows. The end results can be pattern-based, like a fractal, but sometimes things can get really weird and unpredictable. It’s a science that’s been used to model growth systems used in AI, video games, and DNA sequences.

Fuckin’ wild, right?

## CA, from EMB
*Here’s how cellular automata (hereafter CA) works in Teletype, from EMB.  
I corrected a small error, in case you look this up on llllllll.co*

the behavior is defined by two things:

an initial state, say
00100100
and 2) an update rule. the rule says: to get the new value of a state, look at its old value and the value of its previous neighbors. so there are 8 possible configurations to look at, and we specify the desired result for each:

```
input:    111 110 101 100 011 010 001 000
output:    0   0   0   1   1   1   1   0
```

so the rule can be encoded as 8 bits in an integer. wolfram established a convention for doing this, by which the rule written above is equal to 0b00011110 = 0x1e = 30. so this is referred to in the literature as rule 30.

when we apply the rule to the initial state, and keep applying it to subsequent states, we get a sequence

1. 00100100
2. 01111110
3. 11000001
4. 00100011
5. 11110110
6. 10000100  

and so on. (assuming i didn’t mess that up.) (*nb: this version has been corrected.*)

(by the way, in this implementation i am wrapping the edges; they could also be fixed. different behaviors; both are chaotic.)

these states likewise can be encoded as 8-bit integers. that representation is what the operator produces at its output and accepts as its input. i agree that it doesn’t make the output super intuitive; i think this structure is most useful when you can map the output bits to gates, which makes this an extremely fun sequencer.

## How to make this album at home
The way that cellular automata has been implemented in Teletype, you begin by choosing a rule and an initial state (seed). Then, call the function to run the rule through subsequent states. The timing of this is determined by you, using the metronome / clock in Teletype.

Let’s say we choose a seed of `36` (00100100) and iterate with rule 30 (basically, EMB’s above example).  
*One iteration*: `126` (which is the integer translation of 01111110)  
*More iterations*: `193`, `35`, `246`, `132`, `207`, `56`, `100`, `222`, `144`, `249`, `7`, `140`, `219`, `18`, `63`, `224`, `145`, `123`, `66`, `231`, `28`, `50`, `111`, `72`, `252`, `131`, `70`, `237`, `9`, `159`, `112`, `200`, `189`, `33`, `243`, `14`, `25`, `183`, `36` (where we started!), `126` (a repeat!!), `193` (a repeat!!!), `35` (a repeat!!!!), `246` (a repeat!!!!!)

We’ve entered a loop! Excellent.

So we got a list of what seemed like random numbers, but what’s cool is that these numbers started to *repeat*. Which means they’re not necessarily “random.” They are the expected results of definitive iterations of 65,536 possibilities. What makes them feel “random” is that I can’t *predict* the results.

Most importantly, I can’t attach my ego to the result, because I don’t really know what it’s going to be. At best, I can guess and observe.

Let’s do something with the results.

## Multi-tasking

While Teletype performs this active CA process, it can also store lists of numbers in a Tracker which can be read on demand and sent as note data to an oscillator.

Let’s say I put the steps of a major scale in the Tracker:
`[0,2,4,5,7,9,11]`  
Actually, let’s have it span two octaves:
`[0,2,4,5,7,9,11,12,14,16,17,19,21,23]`

Each of these numbers occupy an index position in the Tracker, beginning with a 0th position.
e.g.: ‘7’ is in the **4th** position, ’17’ is in the **10th** position, ‘0’ is in the **0th** position.

**Choice**: I want to use CA to crawl these Tracker positions.  
**Barrier**: Teletype’s CA operator naturally returns values between 0 and 255 and I only have 14 positions, 0 through 13.  
**Solution**: I can compress the range of 0 through 255 to 0 through 13, to make it easier for the CA to return useful results when it crawls the Tracker positions.

Teletype’s math operators allow me to scale these results. So, if the CA returns its max of 255, Teletype will scale it to the new max of 13. It will also round decimals.

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

**Choice**: I want to remove the dumb, thinking part of my self from the sequencing of pitches.  
**Solution**: Use the major scale degrees in each CA-chosen Tracker positions (above) to sequence an oscillator.

Iterating these results from Tracker position to actual major scale degrees...  
note data:`[0,2,4,5,7,9,11,12,14,16,17,19,21,23]`  

```
(position -> note data)  

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

*For review:*  
- we started with CA to generate “random” numbers, ranging from 0-255  
- we entered the notes we wanted to play in Teletype’s Tracker, positions 0-13  
- we took those CA results and scaled them down to 0-13 to seek through the Tracker positions  
- the major scale degrees in each position becomes our melody line

What’s really exciting here is I didn’t *make* the pattern of notes. I made some structural choices, but I did not sit down to write the sequence that emerges. This removes direct ownership over the results, which shifts the traditional dynamic of my role in this whole thing. The weight of ‘statement’ and ego fade. The whole process is now mostly observation.

The duality of “composer” and “being who seeks validation” (which are too deeply linked in me) pivots toward a more scientific “catalyst” and “observer”.

I can now watch choices manifest without fear or self-consciousness.  
I set the initial conditions and I can affect the aesthetic, but *I* am not responsible for melodic expression or harmonic progression.  
I’m listening and responding, not exerting control and judging (myself; the music; worthiness; imposter status; expressions of genre; how I’m seen, by whom; an audience I’ve yet to even engage that I assume an awful lot about when I’m worrying + “Writing Music”).

If I feel good about any results, it’s because I simply appreciate the outcome of the experiment.

I show up to guide the presentation of the results. I don’t get to own the good shit. I’m only here as presence, not as credit-seeking jag.

And if the results are “bad”, then I move onto the next seed or maybe adjust the scale / note pool or change tempo or... whatever, you know?  
The important thing here is that the element that caused me the most stress, that I hung most of my need for validation on, was offloaded.  
To me, that’s the fuckin’ beauty of these tools — they can free the person to make person choices.

I’m not going to fret and wrestle my way through traditional composition and write anything that feels good to have written.  
That process hasn’t really paid off, in the last few years I’ve been learning these tools.  
And if it does, the high doesn’t last.

The real fun of this (which has to be the only quality that really matters) is in dialogue.

## Last bit...

**Choice**: It’d be rad if there were direct relationships between pitches and rhythms.  
**Barrier**: Determining *when* notes happen is the other most stressful part for me.

Let’s revisit those binary conversions.

Translating the position sequence into binary:  

```
(position -> binary)

2 -> 10  
6 -> 110  
9 -> 1001  
1 -> 1  
12 -> 1100  
6 -> 110  
10 -> 1010  
3 -> 11  
5 -> 101  
11 -> 1011  
7 -> 111  
13 -> 1101  
```

Binary’s most basic application is for on/off messages; 1 = on and 0 == off.  
So, basically, each piece of pitch data is just a series of on/off messages.

One of the weirdest lessons to learn when I began working with modular synthesizers is that most instruments operate off -> on.  
Their elements (the strings, the pipes, the drum’s skin) are dormant (off) until they are excited or struck (on).  
Synthesizers operate on -> off. Sound is *always* flowing from an oscillator and requires a gate to orient itself to off -> on.

Gates can be opened with voltage.  
This lets sound through.  
When voltage is no longer supplied, the sound is silenced.

**Choice**: It’d be rad if there were direct relationships between pitches and rhythms.  
**Solution**: Use the binary representation of each note to determine whether or not that note is heard.

I like using a raw sine wave and a processed copy of that same sine wave, so I’m getting two variants of the same source.

So, if each note provides its own string of 1’s and 0’s (or ons/offs)...

**Choice**: If the rightmost bit in a note’s binary representation is 1, then open the raw sine wave’s gate. If the second rightmost bit in a note’s binary representation is 1, then open the processed copy’s gate.

Which gets us...  

```
Pos.: 2  6  9  1  12   6  10  3  5  11   7  13 
Note: 4 11 16  2  21  11  17  5  9  19  12  23
Raw : 0  0  1  1   0   0   0  1  1   1   1   1  
Copy: 1  1  0  0   0   1   1  1  0   1   1   0  
```

So now, I have a holistic system of choices I made to *explore* outcomes rather than determine them:  
- CA rule chosen  
- CA seed chosen  
- note pool chosen  
- CA progress at a chosen rate  
- CA’s returned values are scaled to pick one of the notes in chosen pool  
- the selected note is played through a chosen oscillator  
- processing of the oscillator is chosen  
- the oscillator, raw, is gated  
- the oscillator, processed, is also gated  
- listen  
- make new choices

This maintains a relationship of play between me and the material generated. Time is spent making choices rather than crafting expressions.

(**IC**: Damn dude, it sounds like the whole process of Writing Music is stressful for you.  
**ICC**: It for sure is.  
**IC**:  It’s just pitches, durations and rhythm.  
**ICC**: Yeah, but pitches, durations and rhythm are too trusting. It’s too easy to impose personal meaning + validation onto those vessels. But they exist, without me. They are invisible and free. I expose and exert control over them to use them to Write Music. I can ruin them, if I’m too involved.  
That’s why I don’t like Writing Music.  
That’s why I like playing music.  
This process helps me play music without Writing it.  
**IC**: Is that even Your Music, then?  
**ICC**: No, thank god.)

## a note on *the stuff*

The five pieces were made using the following items:

```
monome Teletype
Mannequins Three Sisters x2
Mannequins Cold Mac
Mannequins w/ x2
Make Noise Function
Max/MSP custom device based on Rodrigo Constanzo’s karma~
```

**The gear doesn’t matter**. Get shit done on what makes sense and is most fun. Things can get out of control and you can get trapped into collecting, otherwise.

These tools are just the stuff that makes sense and is most fun for me.
