

Write the following line and evaluate it (Ctrl+Enter)

```haskell
sound "bd"
```

You should hear a bass drum. Now try changing (and re-evaluating) the
line of code. Some sounds you could try:

```
    flick sid can metal future gabba sn mouth gretsch mt arp h cp newnotes
    bass hc bass0 hh bass1 bass2 oc bass3 ho odx diphone2 house off ht
    tink perc bd industrial pluck trump printshort jazz voodoo birds3
    procshort blip drum jvbass psr wobble drumtraks koy rave ravebass
    bottle kurt latibro rm sax lighter lt arpy feel less stab ul casio
```

To stop the sound evaluate:

```haskell
silence
```

(or press ctrl-.)

Each of these names stands for a sets of sounds. You can pick
different sounds from a set by using `:` and a number, for example for
the third 'arpy' sound:

```haskell
sound "arpy:2"
```

(you start counting at `0` for the first sound)

Ok lets start sequencing sounds:

```haskell
sound "arpy:1 arpy:2 arpy:3"
```

All the sounds in a sequence are played in one cycle.

```haskell
sound "bd sn"

sound "bd sn hh cp mt arpy drum"

sound "bd sn hh cp mt arpy drum odx bd arpy bass2 feel future"
```

If things get too intense we can slow things down with a function
called `slow`:

```haskell
slow 4 (sound "bd sn hh cp mt arpy drum odx bd arpy bass2 feel future")
```

We can add rests in our sequence with `~`:

```haskell
slow 2 (sound "arpy:1 ~ arpy:3")
```

So far the sounds in our sequences have been evenly distributed.. But
we can break things up.

We can take a step in a pattern and break it down into a subpattern like this:

```haskell
sound "[bd sn] hh"
~~~

The square brackets group the samples inside in one single step of the cycle.

We can start nesting patterns to create complexity from simplicity!

```haskell
sound "[bd bd] bd [sn sn sn] sn sn]"
```

We can also create polyrhythms by using commas:

```haskell
sound "[hh hh, arpy arpy:1 arpy:2]"
```

Adding as many layers as we want:

```haskell
sound "[hh, sn cp sn, arpy:4 arpy:2, odx, ~ cp]"
```

We can mix square brackets and commas too:

```haskell
sound "[hh, [sn*2] cp sn, arpy:4 arpy:2, arpy [arpy:4 [arpy:1 arpy:2] arpy:3 arpy], odx, ~ cp]"
```

Asterisks are multipliers and can be used to repeat the same step as
many times we want:


```haskell
sound "bd*8 bd*3"
```

We can also divide using `/`, the sample is then played half as often,
in this case:

```haskell
sound "bd bd/2"
```

## FUNCTIONS!

We can reverse a pattern with rev ...

```haskell
rev (sound "[[bd sn] cp]")
```

... or only sometimes ...

```haskell
sometimes rev (sound "[[bd sn] cp]")
```

... or every 2 cycles ...

```haskell
every 2 rev (sound "[[bd sn] cp]")
```

... or only in one speaker.

```haskell
jux rev (sound "[[bd sn] cp]")
```

We can slow or speed a pattern with `slow` or `density`:

```haskell
density 2 (sound "[[bd sn] cp]")

every 2 (density 2) (sound "[[bd sn] cp]")
```

We can also pattern sound effects:

```haskell
sound "bd sn*2 bd*3"
  # vowel "a e"
  # speed "2"
```
  
That's probably enough for this workshop, but there is more! See
http://tidalcycles.org/

You'll see examples on the website are prefixed by something like `d1
$` to select a 'pattern stream' - this isn't used in the interface
you're using.
