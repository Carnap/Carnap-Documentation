# Natural deduction in the original *forall x* systems

This document gives a short description of how Carnap presents the
systems of natural deduction from P.D. Magnus' [*forall
x*](https://www.fecundity.com/logic/). At least some prior familiarity
with Fitch-style proof systems is assumed.

There are several alternate versions (remixes) of *forall x*, which
use slightly different syntax and/or rules. The versions supported by
Carnap are:

- The original version of *forall x* by P.D. Magnus, described on this
  page.
- [*forall x: Calgary*](forallx-yyc.md)
- [*forall x: Mississippi State*](forallx-msu.md)
- [*forall x: Pittsbugh*](forallx-pitt.md)
- *forall x: UBC*

## Notation

The different admissible keyboard abbreviations for the different connectives
are as follows:

<div class="table">

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
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

Here's an example derivation, using system SL of P.D. Magnus *forall
x*, activated in Carnap by `.ForallxSL`:

```{.ProofChecker .ForallxSL options="render resize fonts" init="now"}
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

Or, with a Fitch-style guides overlay (activated with `guides="fitch"`):

```{.Playground .ForallxSL options="render resize fonts" guides="fitch" init="now"}
|   A \/ B:AS
|      A:AS
|      B \/ A:\/I 2
|   --
|      B:AS
|      B \/ A:\/I 5
|   B \/ A:\/E 1,2-3,5-6
|(A \/ B) -> (B \/ A):->I 1-7
```

There is also a playground mode:

```{.Playground .ForallxSL options="render resize fonts"  init="now"}
```

## Sentential logic

### *forall x* System SL

The minimal system SL for P.D. Magnus' *forall x* (the system used in
a proofchecker constructed with `.ForallxSL` in Carnap's [Pandoc
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
Reiteration            `R`          $φ$           $φ$
---------------------- ------------ ------------- -----------

</div>

We also have four rules for indirect inferences:

1. `→I`, which justifies an assertion of the form $φ→ψ$ by citing a subproof
   beginning with the assumption $φ$ and ending with the conclusion $ψ$; 
2. `↔I`, which justifies an assertion of the form φ↔ψ by citing two
   subproofs, beginning with assuptions $φ$, $ψ$, respectively, and
   ending with conclusions  $ψ$, $φ$, respectively;
3. `¬I`, which justifies an assertion of the form $¬φ$ by citing a
   subproof beginning with the assumption $φ$ and ending with a pair
   of lines $ψ$,$¬ψ$.
3. `¬E`, which justifies an assertion of the form φ by citing a
   subproof beginning with the assumption $¬φ$ and ending with a pair
   of lines $ψ$,$¬ψ$.

Finally, `PR` can be used to justify a line asserting a premise, and
`AS` can be used to justify a line making an assumption. A note about
the reason for an assumption can be included in the rendered proof by
writing `A/NOTETEXTHERE` rather than `AS` for an assumption.
Assumptions are only allowed on the first line of a subproof.

### *forall x* System SL Plus

The extended system SL Plus for P.D. Magnus' *forall x* (the system used in a
proofchecker constructed with `.ForallxSLPlus` in Carnap's [Pandoc
Markup](pandoc.md)) also adds the
following rules:

<div class="table">

Rule                   Abbreviation Premises      Conclusion
---------------------- ------------ ------------- -----------
Dilemma                `DIL`        $φ∨ψ,φ→χ,ψ→χ$ $χ$        
Hypothetical Syllogism `HS`         $φ→ψ, ψ→χ$    $φ→χ$
Modus Tollens          `MT`         $φ→ψ,¬ψ$      $¬φ$
---------------------- ------------ ------------- -----------

As well as the following exchange rules, which can be used within a
propositional context Φ:

Rule                   Abbreviation Premises      Conclusion
---------------------- ------------ ------------- -----------
Commutativity          `Comm`       $Φ(φ∧ψ)$      $Φ(ψ∧φ)$
                                    $Φ(φ∨ψ)$      $Φ(ψ∨φ)$
                                    $Φ(φ↔ψ)$      $Φ(ψ↔φ)$
Double Negation        `DN`         $Φ(φ)/Φ(¬¬φ)$ $Φ(¬¬φ)/Φ(φ)$
Material Conditional   `MC`         $Φ(φ→ψ)$      $Φ(¬φ∨ψ)$
                                    $Φ(¬φ∨ψ)$     $Φ(φ→ψ)$      
                                    $Φ(φ∨ψ)$      $Φ(¬φ→ψ)$
                                    $Φ(¬φ→ψ)$     $Φ(φ∨ψ)$      
BiConditional Exchange `↔ex`        $Φ(φ↔ψ)$      $Φ(φ→ψ∧ψ→φ)$
                                    $Φ(φ→ψ∧ψ→φ)$  $Φ(φ↔ψ)$      
DeMorgan's Laws        `DeM`        $Φ(¬(φ∧ψ))$   $Φ(¬φ∨¬ψ)$
                                    $Φ(¬(φ∨ψ))$   $Φ(¬φ∧¬ψ)$
                                    $Φ(¬φ∨¬ψ)$    $Φ(¬(φ∧ψ))$
                                    $Φ(¬φ∧¬ψ)$    $Φ(¬(φ∨ψ))$   
---------------------- ------------ ------------- -----------

</div>

## Quantificational logic

The proof system for Magnus's *forall x*, QL, is activated using `.ForallxQL`.

### Notation

The different admissible keyboard abbreviations for quantifiers and
equality is as follows:

<div class="table">

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

</div>


The *forall x* first-order systems do not contain sentence letters.

Application of a relation symbol is indicated by directly appending the arguments to the symbol.

The available relation symbols are $A$ through $Z$, together with the
infinitely many subscripted letters $F_1, F_2, \ldots$ written `F_1,
F_2. The arity of a relation symbol is determined from context.

The available constants are a through w, with the infinitely many
subscripted letters $c_1, c_2, \ldots$ written `c_1, c_2,…`.

The available variables are $x$ through $z$, with the infinitely many
subscripted letters $x_1, x_2,\dots$ written `x_1, x_2,…`.

### Basic Rules

The first-order *forall x* systems QL (the systems used in
proofcheckers constructed with `.ForallxQL`) extend the rules of the
system SL with the following set of new basic rules:

<div class="table">

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Existential Introduction    `∃I`         $φ(σ)$             $∃xφ(x)$

Universal  Elimination      `∀E`         $∀xφ(x)$           $φ(σ)$

Universal  Introduction     `∀E`         $φ(σ)$             $∀xφ(x)$

Equality Introduction       `=I`                            $σ=σ$

Equality Elimination        `=E`         $σ=τ,φ(σ)/φ(τ)$    $φ(τ)/φ(σ)$

--------------------------------------------------------------------------

</div>


Where Universal Introduction is subject to the restriction that $σ$ must not
appear in $φ(x)$, or any undischarged assumption or in any premise of the
proof.[^1]

[^1]: Technically, Carnap checks only the assumptions and premises that are
used in the derivation of $φ(σ)$. This has the same effect in terms of what's
derivable, but is a little more lenient.

It also adds one new rule for indirect derivations: `∃E`, which justifies an
assertion $ψ$ by citing an assertion of the form $∃xφ(x)$ and a subproof
beginning with the assumption $φ(σ)$ and ending with the conclusion $ψ$, where
$σ$ does not appear in $ψ, ∃xφ(x)$, or in any of the undischarged assumptions
or premises of the proof.

### forall x QL Plus

The system QL Plus, activated with `.ForallxQLPlus`, includes all the
rules of SL Plus, as well as the following exchange rules, which can
be used within a context Φ:

Rule                   Abbreviation Premises       Conclusion
---------------------- ------------ -------------- --------------
Quantifier Negation    `QN`         $Φ(∀x¬φ(x)))$  $Φ(¬∃xφ(x)))$
                                    $Φ(¬∀xφ(x)))$  $Φ(∃x¬φ(x)))$
                                    $Φ(∃x¬φ(x)))$  $Φ(¬∀xφ(x)))$
                                    $Φ(¬∃xφ(x)))$  $Φ(∀x¬φ(x)))$
---------------------- ------------ -------------- --------------
