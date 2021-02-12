# Natural Deduction in the *forall x: Pittsburgh* systems

This document gives a short description of how Carnap presents the
systems of natural deduction from [*forall x:
Pittsburgh*](http://jdmitrigallow.com/teaching/logic19/text.pdf), the
remix by Dimitri Gallow of Aaron Thomas-Bolduc and Richard Zach's
Calgary version of P.D. Magnus's *forall x*.

The syntax of formulas accepted is described in the [Systems
Reference](systems.md#gallow-forall-x-pittsburgh).

## Truth-functional logic

### Notation

The different admissible keyboard abbreviations for the different connectives
are as follows:

<div class="table">

Connective Keyboard 
---------- ----------
→          `->`, `=>`, `>`
∧          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
⊥          `!?`, `_|_`
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

Here's an example derivation, using the system `.GallowSL`:

```{.ProofChecker .GallowSL options="render resize fonts" init="now"}
Ex :|-: (A \/ B) -> (B \/ A)
|   A \/ B:AS
|      A:AS
|      B \/ A:\/I 2
|   --
|      B:AS
|      B \/ A:\/I 5
|   B \/ A:\/E 1,2-3,5-6
|(A \/ B) -> (B \/ A):->I 1-7
```

Or, `.GallowSLPlus` with a Fitch-style guides overlay (activated with
`guides="fitch"`):

```{.Playground .GallowSLPlus options="resize fonts" guides="fitch" init="now"}
|   A \/ B:AS
|      A:AS
|      B \/ A:\/I 2
|   --
|      B:AS
|      B \/ A:\/I 5
|   B \/ A:\/E 1,2-3,5-6
|(A \/ B) -> (B \/ A):->I 1-7
```

Simple indent guides overlay (activated with `guides="indent"`) with
system `.GallowPL`:

```{.Playground .GallowPL options="resize fonts" guides="indent" init="now"}
|   A \/ B:AS
|      A:AS
|      B \/ A:\/I 2
|   --
|      B:AS
|      B \/ A:\/I 5
|   B \/ A:\/E 1,2-3,5-6
|(A \/ B) -> (B \/ A):->I 1-7
```

### The SL systems

The system `.GallowSLPlus` allows all rules below. `.GallowSL` is like
`.GallowSLPlus` except it *disallows* all derived rules, i.e., the
only allowed rules are `R`, and the I and E rules for the connectives
and for ⊥. 

It has the following set of rules for direct inferences:

<div class="table">
Basic rules:

Rule                   Abbreviation Premises     Conclusion
---------------------- ------------ ------------ -----------
And-Elim.              `∧E`         $φ∧ψ$        $φ/ψ$        
And-Intro.             `∧I`         $φ,ψ$        $φ∧ψ$
Or-Intro               `∨I`         $φ/ψ$        $φ∨ψ$
Contradiction-Intro    `⊥I`         $φ,¬φ$       $⊥$
Contradiction-Elim     `⊥E`         $⊥$          $ψ$
Biconditional-Elim     `↔E`         $φ/ψ,φ↔ψ$    $ψ/φ$
Reiteration            `R`          $φ$          $φ$
---------------------- ------------ ------------ ------------

Derived rules:

Rule                   Abbreviation Premises     Conclusion
---------------------- ------------ ------------ -----------
Disjunctive Syllogism  `DS`         $¬ψ/¬φ,φ∨ψ$  $φ/ψ$
Modus Tollens          `MT`         $φ→ψ,¬ψ$     $¬φ$
Double Negation Elim.  `DNE`        $¬¬φ$        $φ$                
DeMorgan's Laws        `DeM`        $¬(φ∧ψ)$     $¬φ∨¬ψ$ 
                                    $¬(φ∨ψ)$     $¬φ∧¬ψ$ 
                                    $¬φ∨¬ψ$      $¬(φ∧ψ)$
                                    $¬φ∧¬ψ$      $¬(φ∨ψ)$
---------------------- ------------ ------------ -----------

</div>

We also have five rules for indirect inferences:

1. `→I`, which justifies an assertion of the form $φ→ψ$ by citing a subproof
   beginning with the assumption $φ$ and ending with the conclusion $ψ$; 
2. `↔I`, which justifies an assertion of the form $φ↔ψ$ by citing two subproofs,
   beginning with assumptions $φ$, $ψ$, respectively, and ending with
   conclusions  $ψ$, $φ$, respectively;
3. `¬I`, which justifies an assertion of the form $¬φ$ by citing a subproof
   beginning with the assumption $φ$ and ending with a conclusion $⊥$.
5. `∨E`, which justifies an assertion of the form φ by citing a disjunction
   $ψ∨χ$ and two subproofs beginning with assumptions $ψ,χ$ respectively and
   each ending with the conclusion $φ$.
4. `¬E` (indirect proof), which justifies an assertion of the form $φ$
   by citing a subproof beginning with the assumption $¬φ$ and ending
   with a conclusion $⊥$.
6. `LEM` (Law of the Excluded Middle), which justifies an assertion of
   the form $ψ$ by citing two subproofs beginning with assumptions
   $φ,¬φ$ respectively and each ending with the conclusion $ψ$. LEM is
   a derived rule.

Finally, `PR` can be used to justify a line asserting a premise, and
`AS` can be used to justify a line making an assumption. A note about
the reason for an assumption can be included in the rendered proof by
writing `A/NOTETEXTHERE` rather than `AS` for an assumption.
Assumptions are only allowed on the first line of a subproof.


## Predicate logic

There are two proof systems corresponding to the Pittsburgh remix of
_forall x_. All of them allow sentence letters in first-order
formulas. The available relation symbols are the same as for SL: $A$
through $Z$, together with the infinitely many subscripted letters
$F_1, F_2,\ldots$ written `F_1, F_2` etc. However, the available
constants and function symbols are only $a$ through $v$, together with
the infinitely many subscripted letters $c_1, c_2,\ldots$ written
`c_1, c_2,…`. The available variables are $w$ through $z$, with the
infinitely many subscripted letters $x_1, x_2,\ldots$ written `x_1,
x_2,…`.

<div class="table">

Connective Keyboard 
---------- ----------
∀          `A`, `@`
∃          `E`, `3`
---------- ----------

</div>

The predicate logic system `.GallowPL` of  *forall x: Pittsburgh* extend the
rules of the system `.GallowSL` with the following set of new
basic rules:

<div class="table">

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Existential Introduction    `∃I`         $φ(σ)$             $∃xφ(x)$

Universal  Elimination      `∀E`         $∀xφ(x)$           $φ(σ)$

Universal  Introduction     `∀E`         $φ(σ)$             $∀xφ(x)$
--------------------------------------------------------------------------

</div>

Where Universal Introduction is subject to the restriction that $σ$ must not
appear in $φ(x)$, or any undischarged assumption or in any premise of the
proof.[^1]

[^1]: Technically, Carnap checks only the assumptions and premises that are
used in the derivation of $φ(σ)$. This has the same effect in terms of what's
derivable, but is a little more lenient.

There is one new rule for indirect derivations: `∃E`, which justifies
an assertion $ψ$ by citing an assertion of the form $∃xφ(x)$ and a
subproof beginning with the assumption $φ(σ)$ and ending with the
conclusion $ψ$, where $σ$ does not appear in $ψ, ∃xφ(x)$, or in any of
the undischarged assumptions or premises of the proof.

The proof system `.GallowPLPlus` for the Pittsburgh version of *forall x*
adds, in addition to the (basic and derived) rules of `.GallowPL`, the
rules

<div class="table">

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Conversion of Quantifiers   `CQ`         $¬∀xφ(x)$          $∃x¬φ(x)$

                                         $∃x¬φ(x)$          $¬∀xφ(x)$

                                         $¬∃xφ(x)$          $∀x¬φ(x)$

                                         $∀x¬φ(x)$          $¬∃xφ(x)$

--------------------------------------------------------------------------
</div>


