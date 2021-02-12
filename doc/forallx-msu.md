# Natural Deduction in the *forall x: Mississippi State* systems

This document gives a short description of how Carnap presents the
systems of natural deduction from Greg Johnson's [*forall x:
Mississippi
State*](http://blog.loighic.net/forallx-the-mississippi-state-edition).
At least some prior familiarity with Fitch-style proof systems is
assumed.

## Notation

The different admissible keyboard abbreviations for the different connectives
are as follows:

<div class="table">

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
&          `/\`, `and`
∨          `v`, `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

</div>

The available sentence letters are $A$ through $Z$, together with the
infinitely many subscripted letters $P_1, P_2,\ldots$ written `P_1,
P_2` and so on.

Proofs consist of a series of lines. A line is either an assertion
line containing a formula followed by a `:` and then a justification
for that formula, or a separator line containing two dashes, thus:
`--`. A justification consists of a rule abbreviation followed by zero
or more numbers (citations of particular lines) and pairs of numbers
separated by a dash (citations of a subproof contained within the
given line range).

A subproof is begun by increasing the indentation level. The first
line of a subproof should be more indented than the containing proof,
and the lines directly contained in this subproof should maintain this
indentation level. (Lines indirectly contained, by being part of a
sub-sub-proof, will need to be indented more deeply.) The subproof
ends when the indentation level of the containing proof is resumed;
hence, two contiguous sub-proofs of the same containing proof can be
distinguished from one another by inserting a separator line between
them at the same level of indentation as the containing proof. The
final *unindented* line of a derivation will serve as the conclusion
of the entire derivation.

Here's an example derivation, using the TFL system `.JohnsonSL`:

```{.ProofChecker .JohnsonSL options="render resize fonts" init="now"}
Ex ~P \/ (R & Q) :|-: P -> Q
|~P \/ (R & Q) :PR
|    P :AS
|    ~~P :DN 2
|    R & Q :\/E 1,3
|    Q :&E 4
|P -> Q :->I 2-5
```

Or, with a Fitch-style guides overlay (activated with
`guides="fitch"`):

```{.ProofChecker .JohnsonSL options="render resize fonts" guides="fitch" init="now"}
Ex ~P \/ (R & Q) :|-: P -> Q
|~P \/ (R & Q) :PR
|    P :AS
|    ~~P :DN 2
|    R & Q :\/E 1,3
|    Q :&E 4
|P -> Q :->I 2-5
```

There is also a playground mode:

```{.Playground .JohnsonSL options="render resize fonts"  init="now"}
```

The system for Johnson's *forall x: Mississippi State* (the system used in
a proofchecker constructed with `.JohnsonSL` in Carnap's [Pandoc
Markup](pandoc.md)) has the following set of rules for direct
inferences:

<div class="table">

Rule                   Abbreviation Premises      Conclusion
---------------------- ------------ ------------- -----------
And-Elim               `∧E`         $φ∧ψ$         $φ/ψ$        
And-Intro              `∧I`         $φ,ψ$         $φ∧ψ$
Or-Elim                `∨E`         $¬ψ, φ∨ψ$     $φ$
                                    $¬φ, φ∨ψ$     $ψ$
Or-Intro               `∨I`         $φ$           $φ∨ψ$
                                    $ψ$           $φ∨ψ$
Conditional-Elim       `→E`         $φ,φ→ψ$       $ψ$
Biconditional-Elim     `↔E`         $φ, φ↔ψ$      $ψ$
                                    $ψ, φ↔ψ$      $φ$
Biconditional-Intro    `↔I`         $φ→ψ, ψ→φ$    $φ↔ψ$
Double Negation        `DN`         $φ$           $¬¬φ$
Reiteration            `R`          $φ$           $φ$
---------------------- ------------ ------------- -----------
</div>

We also have four rules for indirect inferences:

1. `→I`, which justifies an assertion of the form $φ→ψ$ by citing a subproof
   beginning with the assumption $φ$ and ending with the conclusion $ψ$; 
2. `¬I`, which justifies an assertion of the form $¬φ$ by citing a subproof
   beginning with the assumption $φ$ and ending with a pair of lines $ψ$,$¬ψ$.
3. `¬E`, which justifies an assertion of the form φ by citing a subproof
   beginning with the assumption $¬φ$ and ending with a pair of lines $ψ$,$¬ψ$.

Finally, `PR` can be used to justify a line asserting a premise, and `AS` can
be used to justify a line making an assumption. A note about the reason for an
assumption can be included in the rendered proof by writing `A/NOTETEXTHERE`
rather than `AS` for an assumption. Assumptions are only allowed on the first
line of a subproof.