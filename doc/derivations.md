# Derivations

The `ProofChecker` class indicates that a code block will contain derivation
exercises. The `Playground` class indicates that a code block will generate a
"playground" in which instead of checking whether the proof establishes
something set in advance, Carnap will figure out what the proof establishes and
display it at the top of the proof-box. The formal systems used can be
controlled using predefined classes, or by setting attributes on the code-block
(see below).

## Predefined classes

To get started, it's possible to create simple exercises in the propositional
system of the Carnap book like this:

    ~~~{.ProofChecker .Prop} 
    1.1 P :|-: Q->P
    ~~~

Where the `:|-:` again indicates a turnstile. The result is then:

~~~{.ProofChecker .Prop} 
1.7 P:|-: Q->P
~~~

Similarly,

    ~~~{.Playground .Prop} 
    ~~~

generates

~~~{.Playground .Prop} 
~~~

The class `Prop` specifies that we wish to use the propositional formal system
of the Carnap book, and specifies a couple of UI-defaults for displaying proofs
in that system. The currently available predefined classes are:

<div class="table">

-------------------------------------------------------------------------------------------------------------------------------------
Class Strings                                                 Description
------------------------------------------------------------- ---------------------------------------------------------------------------
`.Prop`, `.FirstOrder`, `.SecondOrder`, `.PolySecondOrder`,   Montague-Style systems, the first two of which are used in the Carnap book. 
`.MontagueSC`,`.MontagueQC`, `ElementaryST`, `SeparativeST`

`.LogicBookSD`, `LogicBookSDPlus`, `LogicBookPD`,             Fitch style systems based on Bergmann Moore and Nelson's *Logic Book*. 
`.LogicBookPDPlus`

`.ForallxSL`, `.ForallxSLPlus`, `.ForallxQL`                  Fitch-style systems based on Magnus's *Forall x*.

`.ZachTFL`, `.ZachTFL2019`, `.ZachFOL`, `.ZachFOL2019`,       Fitch-style systems based on the Calgary Remix of *Forall x*.
`.ZachFOLPlus2019`

`.IchikawaJenkinsSL`, `.IchikawaJenkinsQL`                    Fitch-style systems based on the Ichikawa-Jenkins Remix of *Forall x*.

`.GamutMPND`, `.GamutIPND`, `.GamutPND`, `.GamutPNDPlus`      Fitch-style systems based on the systems used in Gamut's *Introduction to Logic*, including minimal and intuitionistic fragments of propositional logic.
`.GamutND`,

`HowardSnyderSL`,`HowardSnyderPL`                             Systems based on Howard-Snyder's *The Power of Logic*.

`HausmanSL`,`HausmanPL`                                       Systems based on Hausman's *Logic and Philosophy*.

`.GoldfarbND`, `.GoldfarbAltND`, `.GoldfarbNDPlus`,           Lemmon-style systems based on Goldfarb's *Deductive Logic*.
`.GoldfarbAltNDPlus`

`.TomassiPL`                                                  Lemmon-style system based on Tomassi's *Logic*

`.HardegreeSL`, `.HardegreePL`, `.HardegreeWTL`,              Hardegree-style systems based on Hardegree's *Modal Logic* 
`.HardegreeL`, `.HardegreeK`, `.HardegreeT`, `.HardegreeB`,  
`.HardegreeD`, `.Hardegree4`, `.Hardegree5`, `.HardegreeMPL`
-------------------------------------------------------------------------------------------------------------------------------------

</div>

## Advanced Usage

#### Options

Like the other exercises, derivations allow for `points=VALUE` and
`submission="none"`.

Derivations, however, currently have a little more depth than the other types
of exercises. There are, correspondingly, more options available:

<div class="table">

Name         Effect
------------ ------------------------------------------------------------------
`guides`     Includes vertical indentation-level indicators
`fonts`      Uses [Fira Logic](http://github.com/gleachkr/FiraLogic) font, including ligatures for logical symbols
`popout`     Makes it possible to open the problem in a new window
`render`     Renders a picture of the proof as you type
`indent`     Automatically indents newlines to the level of the previous line
`tabindent`  Insert indent on tab press
`resize`     Automatically resizes proof area
`exam`       Allows for submission of work which is incomplete or incorrect
------------ ------------------------------------------------------------------

</div>

These can all be included in the "options" string supplied to the options
attribute of the code block, like this:

    ~~~{.ProofChecker .Prop options="indent fonts popout render indent"} 
    1.8 P :|-: Q->P
    |1.Show Q->P
    |2.   Q:AS
    |3.   P:PR
    |4.:CD 3
    ~~~

The result of the above is:

~~~{.ProofChecker .Prop options="guides fonts popout resize render indent"} 
1.8 P :|-: Q->P
|1.Show Q->P
|2.   Q:AS
|3.   P:PR
|4.:CD 3
~~~

An options string will override any options that are included by default in a
given predefined class. For example, `.Prop` automatically turns on the
`resize` option. However if we have just

    ~~~{.ProofChecker .Prop options="indent"} 
    1.9 P :|-: Q->P 
    ~~~

We get a proofbox that resizes manually:

~~~{.ProofChecker .Prop options="indent"} 
1.9 P :|-: Q->P 
~~~

#### Partial Solutions

A partial solution to a problem can be included by following a problem with a
derivation that is line-by-line prefixed with the `|` character, optionally
(for readability) followed by a line number followed by a period, like this:

    ~~~{.ProofChecker .Prop} 
    1.7 P :|-: Q->P
    |1.Show Q->P
    |2.   Q:AS
    |3.   P:PR
    |4.:CD 3
    ~~~

This gives us:

~~~{.ProofChecker .Prop} 
1.7 P :|-: Q->P
|1.Show Q->P
|2.   Q:AS
|3.   P:PR
|4.:CD 3
~~~

Everything after the line number (or the `|` if you don't use numbers) is
included in the proof, so be careful about spaces!

You can also include a partial derivation without specific solution, by
replacing `.ProofChecker` with `.Playground`, writing for example:

```
~~~{.Playground .Prop} 
|1.Show Q->P
|2.   Q:AS
|3.   P:PR
|4.:CD 3
~~~
```

which gives you a proof box that calculates what has been derived and displays
it at the top, rather than calculating whether the derivation proves a given
sequent, thus:

~~~{.Playground .Prop} 
|1.Show Q->P
|2.   Q:AS
|3.   ?:PR
|4.:CD 3
~~~

#### Feedback

The defaults for feedback (check the proof with every keypress) can also be
overridden by setting the feedback attribute. The override options for feedback
are

<div class="table">

Name          Effect 
------------- ------------------------------------
`manual`      require a button-press for feedback
`syntaxonly`  warn about syntax errors, but do not check proof for correctness
`none`        do not offer feedback
------------- ------------------------------------

</div>

So,

    ~~~{.ProofChecker .Prop submission="none" feedback="manual"} 
    1.10 P :|-: Q->P
    ~~~

produces

~~~{.ProofChecker .Prop submission="none" feedback="manual"} 
1.10 P :|-: Q->P
~~~

#### Systems

If you don't want to use a predefined class, you can set the system option
manually. This will give you complete control over which options are set—only
the ones you select will be active. So you would write something like:

    ~~~{.ProofChecker system="prop" submission="none" feedback="manual"} 
    1.11 -Q :|-: Q->P
    ~~~

to produce

~~~{.ProofChecker system="prop" submission="none" feedback="manual"} 
1.11 -Q :|-: Q->P
~~~

The available propositional systems are: `prop` `montagueSC` `LogicBookSD`
`LogicBookSDPlus` `hausmanSL` `howardSnyderSL` `ichikawaJenkinsSL` `hausmanSL`
`magnusSL` `magnusSLPlus` `thomasBolducAndZachTFL`
`thomasBolducAndZachTFL2019` `gamutMPND` `gamutIPND`,
`gamutPND` `gamutPNDPlus` `tomassiPL` and `hardegreeSL`. The available
first-order systems are: `firstOrder` `montagueQC` `magnusQL`
`thomasBolducAndZachFOL` `thomasBolducAndZachFOL2019`
`thomasBolducAndZachFOLPlus2019` `LogicBookPD` `LogicBookPDPlus` `gamutND`
`hausmanPL` `howardSnyderPL` `ichikawaJenkinsQL` `hardegreePL` `goldfarbAltND`
`goldfarbNDPlus` and `goldfarbAltNDPlus`. The available set theory systems are:
`elementarySetTheory` and `separativeSetTheory`. The available second-order
systems are: `secondOrder` and `PolySecondOrder`. The available propositional
modal logic systems are: `hardegreeL` `hardegreeK` `hardegreeT` `hardegreeB`
`hardegreeD` `hardegree4` and `hardegree5`. The available predicate modal logic
system is `hardegreeMPL`, and the available "world theory" system is
`hardegreeWTL`.

#### Initialization

The `init` attribute may be set to "now" in order to check the proof as soon as
it is loaded, instead of waiting for a user interaction.

#### Indentation Guides

Besides just the indentation guide created by setting `guides` in the options
string, there are several more refined overlays available for increasing the
readability of a typed proof. These are configured by setting the `guides`
attribute. The available options for guides are:

<div class="table">

Name               Effect 
------------------ ------------------------------------
`montague`         Simple indentation gudie
`fitch`            A fitch style proof overlay
`hausman`          A Hausman style proof overlay
`howard-snyder`    A Howard-Snyder style proof overlay
------------------ ------------------------------------

</div>

So, 

    ~~~{.Playground .ForallxSL guides="fitch"} 
     P       :AS
     P/\P    :&I 1 1
     P       :&E 2
    P->P        :->I 1-3
    ~~~

Produces:

~~~{.Playground .ForallxSL guides="fitch" init="now" options="fonts resize"} 
 P       :AS
 P/\P    :&I 1 1
 P       :&E 2
P->P     :->I 1-3
~~~
