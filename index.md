# Semimak
The Semimak layout is designed to have low finger movement rate -
decreasing the overall speed at which your fingers must travel to type
on average. This doesn't only mean to optimize for reducing
same-finger bigrams (e.g "ed" on QWERTY), but disjointeds as well (eg.
the "m_y" in "may" on QWERTY). It is not certain if a layout can
change maximum potential speed, but Semimak should be near the best
possible in that regards.

A picture of the layout will be here on July 1st.

# Development
Most layout analyzers at the moment report an SFB percentage - how
many times you use the same finger to hit two keys in a row. But I
found this somewhat superficial - not all SFBs are equally bad. They
can be heavily influenced by what finger is being used and how much
distance is traveled in the SFB. In addition, the statistic can be
generalized more. Why do the two keys in the bigram need to be
concurrent to be significant? 

## Skipgrams
Instead of only punishing same-finger bigrams weighted by finger and
distance, I had the idea to also punish same-finger skipgrams. You can
weight this exponentially - separated by 0 keys (normal bigram) is a
weight of 1, separated by 1 is 0.5, separated by 2 is 0.25, and so on.
These weights are arbitrary, but they were inspired both by my own
experiences and what great typists much faster than me have said. 

## Distance weighting
This is pretty simple. I square the distance to punish distance
exponentially. A distance of 1u is treated as 1, whereas a distance of
2u is treated as 4. In addition, lateral/horizontal movement is
treated as 1.6x the amount. This is because a reasonable amount of
people find this movement to be more uncomfortable.

## Finger weighting
I used a script that NotGate wrote to test how quickly I can move each
of my fingers. For example, to see how dexterous my middle finger is,
I would type `eded` over and over on QWERTY, and see how fast my keys
per second was. This data was then used to weight how bad fast
distance is on each finger.

## Scoring
As of the most recent iteration, I score largely on the finger
movement rate metric, a little bit with rolls, and some encouragement
of having balanced index finger usage.

## Generation and analysis
I wrote an analyzer/generator for this project on
[my Github](https://github.com/semilin/genkey). It was initially intended to
be a quick hack-up but it ended up one of the more powerful generators
out there. Even so, it was mostly made for myself, so it will be
difficult for other people to use. 

The generation uses a greedy search that over time increases the
number of keys that are swapped at a time - this is done to break out
of local optima.

# Download
Downloads will be available on July 1st for EPKL, MSKLC, AHK, and Linux.
