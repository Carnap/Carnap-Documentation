#Translations 

the `Translate` class indicates that a code block will contain translation
exercises that require symbolizing natural language sentences.

##Propositional Logic

You can create propositional logic translation problems by also adding the
class `Prop`, like so:

    ~~~{.Translate .Prop}
    3.1 P/\Q : People want to know what's going on and questions are unavoidable
    ~~~

The number 3.1 indicates the exercise number, and the colon separates the
solution from the text that will be presented for translation. The result of
the above is:

~~~{.Translate .Prop}
3.1 P/\Q : People want to know what's going on and questions are unavoidable
~~~

To complete it, replace the text to the left of the submit solution button with
your translation, press return to check, and then press "Submit Solution".
Propositional translations are considered correct if they are logically
equivalent to the original answer. So for example, `Q/\P` will be accepted
above.

##First-Order Translation

It is also possible to create first-order translation problems using the class `FOL`, thus:

    ~~~{.Translate .FOL}
    3.2 AxF(x) : Everything is fine
    ~~~

with the result:

~~~{.Translate .FOL}
3.2 AxF(x) : Everything is fine
~~~

These are completed as above. Equivalence of first-order sentences is
undecidable, so we can't check it, but we can catch most cases of "equivalent"
translations by using some rewriting rules.[^1] So, for example `~Ex~F(x)` will
be accepted above.

[^1]: the procedure is roughly as follows:

    a. using the standard rules of passage, drive quantifiers in as far as possible
       in both the submitted solution $S_0$, and in the target sentence $T_0$, generating two
       result sentences $S_1$,$T_1$
    b. using the standard rules of passage, pull out quantifiers as far as
       possible, in every possible way, generating a set $S_2$ of sentences from
       $S_1$, and a set of sentences $T_2$ from $T_1$
    c. allowing permutation of quantifiers within blocks, look for pairs of
       sentences $(S_3,T_3)$ with matching quantifier prefixes. Canonically
       rename the variables. Check the matricies of the resulting formulas for
       propositional equivalence.

##Advanced usage

####Multiple Solutions

If you wish to allow students to find one translation of a sentence that admits
several formalizations, you can use a comma-separated list of admissible
solutions. So, 

    ~~~{.Translate .FOL}
    3.5 (P /\ Q) \/ R, P/\(Q\/R) : Jack jumped the fence and was caught by the watchman or got away.
    ~~~

generates 

~~~{.Translate .FOL}
3.5 (P /\ Q) \/ R, P/\(Q\/R) : Jack jumped the fence and was caught by the watchman or got away.
~~~

####Options and Attributes

In addition to allowing for custom point values with `points=VALUE`, and
turning off submission with `submission="none"`, translations also have the
following options

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------------
`nocheck`                Disables checking solutions
`exam`                   Allows for submission of work which is incomplete or incorrect
`checksyntax`            When `exam` is active, blocks submission of syntactically incorrect work
------------------------ ------------------------------------------------------------------------

</div>

These can be included in the space separated list supplied to the `options`
attribute. 

The way that formulas are parsed can also be customized. This is done by
setting the `system` attribute to indicate which formal system you are drawing
your syntax from. So for example, 

    ~~~{.Translate .FOL system="magnusQL"}
    3.5 AxBx : Everything is bananas
    ~~~

will generate:

~~~{.Translate .FOL system="magnusQL"}
3.5 AxBx : Everything is bananas
~~~

For first-order translations, the available systems are: `firstOrder`
`montagueQC` `magnusQL` `thomasBolducAndZachFOL` `thomasBolducAndZachFOL2019`
`LogicBookPD` `LogicBookPDPlus` `hausmanPL` `howardSnyderPL`
`ichikawaJenkinsQL` `hardegreePL` `goldfarbAltND` `goldfarbNDPlus` and
`goldfarbAltNDPlus`. For propositional translations, the available systems are:
`prop` `montagueSC` `LogicBookSD` `LogicBookSDPlus` `hausmanSL`
`howardSnyderSL` `ichikawaJenkinsSL` `hausmanSL` `magnusSL` `magnusSLPlus`
`thomasBolducAndZachTFL` `thomasBolducAndZachTFL2019` `tomassiPL` and
`hardegreeSL`.

Finally, you can impose one or more extra tests on a translation. This is done
by setting the `tests` attribute to indicate which tests you wish to require
the translation to pass. The available tests for propositional translations are

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------
`CNF`                    Requires conjunctive normal form
`DNF`                    Requires disjunctive normal form
`maxCon:N`               Requires that the translation contain N or fewer connectives
`maxNot:N`               Requires that the translation contain N or fewer negations
`maxAnd:N`               Requires that the translation contain N or fewer conjunctions
`maxIff:N`               Requires that the translation contain N or fewer biconditionals
`maxIf:N`                Requires that the translation contain N or fewer conditionals
`maxOr:N`                Requires that the translation contain N or fewer disjunctions
`maxFalse:N`             Requires that the translation contain N or fewer falsity constants
`maxAtom:N`              Requires that the translation contain N or fewer atomic sentences
------------------------ ------------------------------------------------------------------

</div>
 
The available tests for first-order translations are all the propositional
tests, plus:

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------
`PNF`                    Requires prenex normal form
------------------------ ------------------------------------------------------------------

</div>

When using multiple tests, their names must be separated by spaces, so for
example,

    ~~~{.Translate .FOL tests="PNF maxNeg:0"}
    3.6 ~Ex~F(x) : Nothing is not bananas.
    ~~~

will generate:

~~~{.Translate .FOL tests="PNF maxNeg:0"}
3.6 ~Ex~F(x) : Nothing is not bananas.
~~~

####Partial Solutions

It's possible to include a partial solution to a translation problem, by
including the partial solution after a `|` following the problem. So for
example,

    ~~~{.Translate .FOL options="nocheck"}
    3.7 AxF(x) : Everything is fine
    | For all x, x is fine
    ~~~

Generates

~~~{.Translate .FOL options="nocheck"}
3.7 AxF(x) : Everything is fine
| For all x, x is fine
~~~

