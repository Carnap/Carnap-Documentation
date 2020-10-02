# Natural Deduction in Logic Book Systems

This document gives a short description of how Carnap presents the systems of
natural deduction from Bergmann Moore and Nelson's *Logic Book*. At least some
prior familiarity with Fitch-style proof systems is assumed.

## Propositional Systems

### Notation

The different admissible keyboard abbreviations for the different connectives
are as follows:

<div class="table">

Connective Keyboard 
---------- ----------
⊃          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
~          `-`, `~`, `not`
---------- ----------

</div>

The available sentence letters are $A$ through $Z$, together with the
infinitely many subscripted letters $P_1, P_2,\ldots$ written `P_1, P_2` and so
on.

Proofs consist of a series of lines. A line is either an assertion line
containing a formula followed by a `:` and then a justification for that
formula, or a separator line containing two dashes, thus: `--`.[^1] A
justification consists of zero or more numbers (citations of particular lines)
and pairs of numbers separated by a dash (citations of a subproof contained
within the given line range), followed by the name of a rule being applied.

[^1]: These are intended for use when you have two contiguous subproofs and
need to separate them - since they're at the same level of indentation, you
need some extra indication to show that they're distinct subproofs.

A subproof is begun by increasing the indentation level. The first line of a
subproof should be more indented than the containing proof, and the lines
directly contained in this subproof should maintain this indentation level.
(Lines indirectly contained, by being part of a sub-sub-proof, will need to be
indented more deeply.) The subproof ends when the indentation level of the
containing proof is resumed; hence, two contiguous sub-proofs of the same
containing proof can be distinguished from one another by inserting a separator
line between them at the same level of indentation as the containing proof. The
final *unindented* line of a derivation will serve as the conclusion of the
entire derivation.

Here's an example derivation, using system SD from the *Logic Book*

```{.Playground .LogicBookSD options="resize render" guides="fitch" init="now"}
   P        :AS
      P     :AS
      P     :2 R
   P > P    :2-3 CI
P > (P > P) :1-4 CI
```

and here is one using system PD

```{.Playground .LogicBookPD options="resize render" guides="fitch" init="now"}
(Ax)Fx        :PR
(Ax)(Fx > Gx) :PR
Fa            :1 AE
Fa > Ga       :2 AE
Ga            :3,4 >E 
(Ax)Gx        :5 AI 
```

### Basic Rules

#### Logic Book System SD

The minimal system SD from the *Logic Book* (the system used in a proofchecker
constructed with `.LogicBookSD` in Carnap's [Pandoc
Markup](pandoc.md)) has the following set
of rules for direct inferences:

<div class="table">

Rule                   Abbreviation Premises      Conclusion
---------------------- ------------ ------------- -----------
And-Elim.              `&E`         $φ\&ψ$        $φ/ψ$        
And-Intro.             `&I`         $φ,ψ$         $φ\&ψ$
Or-Intro               `\/I`        $φ/ψ$         $φ∨ψ$
Conditional-Elim       `->E`.`CE`   $φ,φ⊃ψ$       $ψ$
Biconditional-Elim     `<->E`,`BE`  $φ/ψ, φ↔ψ$    $ψ/φ$
Reiteration            `R`          $φ$           $φ$
---------------------- ------------ ------------- -----------

</div>

We also have five rules for indirect inferences:

1. `->I` (also denoted `CI`), which justifies an assertion of the form $φ⊃ψ$ by
   citing a subproof beginning with the assumption $φ$ and ending with the
   conclusion $ψ$; 
2. `<->I`, (also denoted `BI`) which justifies an assertion of the form φ↔ψ by
   citing two subproofs, beginning with assuptions $φ$, $ψ$, respectively, and
   ending with conclusions  $ψ$, $φ$, respectively;
3. `~I`, which justifies an assertion of the form $~φ$ by citing a subproof
   beginning with the assumption $φ$ and ending with a pair of lines $ψ$,$~ψ$.
4. `~E`, which justifies an assertion of the form φ by citing a subproof
   beginning with the assumption $~φ$ and ending with a pair of lines $ψ$,$~ψ$.
3. `∨E`, which justifies an assertion of the form χ by citing a line φ∨ψ, and
   two subproofs beginning the assumptions $φ,ψ$ respectively and both ending
   with a line χ.

Finally, `PR` or `Assumption` (to keep with the *Logic Book* terminology) can
be used to justify a line asserting a premise, and `AS` can be used to justify
a line making an assumption. `A/SOMEADDITIONALTEXT` (where
`SOMEADDITIONALTEXT` indicates some additional text to be included alongside
the assumption in the rendered proof) can also be used to justify an
assumption. Assumptions are only allowed on the first line of a subproof.

#### Logic Book System SD Plus

The extended system SD Plus (the system used in a proofchecker constructed with
`.LogicBookSDPlus` in Carnap's [Pandoc
Markup](pandoc.md)) also adds the
following rules:

<div class="table">

Rule                   Abbreviation Premises      Conclusion
---------------------- ------------ ------------- -----------
Modus Tollens          `MT`         $φ⊃ψ,\sim ψ$  $\sim φ$
Hypothetical Syllogism `HS`         $φ⊃ψ, ψ⊃χ$    $φ⊃χ$
Disjunctive Syllogism  `DS`         $\sim ψ, φ∨ψ$ $φ$
                                    $\sim φ, φ∨ψ$ $ψ$
---------------------- ------------ ------------- -----------

As well as the following exchange rules, which can be used within a
propositional context Φ:

Rule                   Abbreviation Premises                      Conclusion
---------------------- ------------ ----------------------------- ----------------
Commutation            `Comm`       $Φ(φ\&ψ)$                     $Φ(ψ\&φ)$
                                    $Φ(φ∨ψ)$                      $Φ(ψ∨φ)$
Association            `Assoc`      $Φ(φ\&(ψ\&χ))$                $Φ((φ\&ψ)\&χ)$
                                    $Φ((φ\&ψ)\&χ)$                $Φ(φ\&(ψ\&χ))$
                                    $Φ(φ∨(ψ∨χ))$                  $Φ((φ∨ψ)∨χ)$
                                    $Φ((φ∨ψ)∨χ)$                  $Φ(φ∨(ψ∨χ))$
Implication            `Impl`       $Φ(φ⊃ψ)/Φ(\sim φ∨ψ)$          $Φ(φ⊃ψ)/Φ(\sim φ∨ψ)$
Double Negation        `DN`         $Φ(φ)/Φ(\sim \sim φ)$         $Φ(\sim \sim φ)/Φ(φ)$
Idempotence            `Idem`       $Φ(φ)$                        $Φ(φ\&φ)$
                                    $Φ(φ\&φ)$                     $Φ(φ)$
                                    $Φ(φ)$                        $Φ(φ∨φ)$
                                    $Φ(φ∨φ)$                      $Φ(φ)$
DeMorgan's Laws        `DeM`        $Φ(\sim (φ\&ψ))$              $Φ(\sim φ∨\sim ψ)$
                                    $Φ(\sim (φ∨ψ))$               $Φ(\sim φ\&\sim ψ)$
                                    $Φ(\sim φ∨\sim ψ)$            $Φ(\sim (φ\&ψ))$
                                    $Φ(\sim φ\&\sim ψ)$           $Φ(\sim (φ∨ψ))$   
Transposition          `Trans`      $Φ(φ⊃ψ)$                      $Φ(\sim ψ⊃\sim φ))$   
                                    $Φ(\sim ψ⊃\sim φ))$           $Φ(φ⊃ψ)$
Exportation            `Exp`        $Φ(φ⊃(ψ⊃χ))$                  $Φ(φ\&ψ⊃χ)$
                                    $Φ(φ\&ψ⊃χ)$                   $Φ(φ⊃(ψ⊃χ))$
Distribution           `Dist`       $Φ(φ\&(ψ∨χ))$                 $Φ((φ\&ψ)∨(φ\&χ))$
                                    $Φ((φ\&ψ)∨(φ\&χ))$            $Φ(φ\&(ψ∨χ))$
                                    $Φ(φ∨(ψ\&χ))$                 $Φ((φ∨ψ)\&(φ∨χ))$
                                    $Φ((φ∨ψ)\&(φ∨χ))$             $Φ(φ∨(ψ\&χ))$
Equivalence            `Equiv`      $Φ(φ↔ψ)$                      $Φ(φ⊃ψ\&ψ⊃φ)$
                                    $Φ(φ⊃ψ\&ψ⊃φ)$                 $Φ(φ↔ψ)$      
                                    $Φ(φ↔ψ)$                      $Φ((φ\&ψ)∨(\sim ψ\&\sim φ))$
                                    $Φ((φ\&ψ)∨(\sim ψ\&\sim φ))$  $Φ(φ↔ψ)$      
---------------------- ------------ ----------------------------- ----------------

</div>

## First-Order Systems

### Notation

The different admissible keyboard abbreviations for quantifiers are as follows:

<div class="table">

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
---------- ----------

</div>

The Logic Book first order systems contain sentence letters $A$ through $Z$,
together with the infinitely many subscripted letters $P_1, P_2,\ldots$ written
`P_1, P_2` and so on.

Application of a relation symbol is indicated by directly appending the
arguments to the symbol.

The available relation symbols are $A$ through $Z$, together with the
infinitely many subscripted letters $F_1, F_2,\ldots$ written `F_1, F_2,…`. The
arity of a relation symbol is determined from context.

The available constants are $a$ through $v$, with the infinitely many
subscripted letters $c_1, c_2,\ldots$ written `c_1, c_2,…`. 

The available variables are $w$ through $z$, with the infinitely many
subscripted letters $x_1, x_2,\ldots$ written `x_1, x_2,…`.

Quantificational phrases are formed by appending a variable to a quantifier,
and wrapping the result in parentheses.

### Basic Rules

The first-order *Logic Book* systems PD and PD+ (the systems used in
proofcheckers constructed with `.LogicBookPD`, and `LogicBookPDPlus`
respectively) extend the rules of the system SD and SD+ respectively with the
following set of new basic rules:

<div class="table">

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Existential Introduction    `EI`         $φ(σ)$             $(∃x)φ(x)$

Universal  Elimination      `AE`         $(∀x)φ(x)$         $φ(σ)$

Universal  Introduction     `AI`         $φ(σ)$             $(∀x)φ(x)$

--------------------------------------------------------------------------

</div>

Where Universal Introduction is subject to the restriction that $σ$ must not
appear in $φ(x)$, or any undischarged assumption or in any premise of the
proof.[^2]

[^2]: Technically, Carnap checks only the assumptions and premises that are
used in the derivation of $φ(σ)$. This has the same effect in terms of what's
derivable, but is a little more lenient.

It also adds one new rule for indirect derivations: `EE`, which justifies an
assertion $ψ$ by citing an assertion of the form $(∃x)φ(x)$ and a subproof
beginning with the assumption $φ(σ)$ and ending with the conclusion $ψ$, where
$σ$ does not appear in $ψ, (∃x)φ(x)$, or in any of the undischarged assumptions
or premises of the proof.

To these rules, PD+ also adds the exchange rule:

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Quantifier Negation         `QN`         $Φ(\sim (∀xφ)(x))$ $Φ((∃x)\sim φ(x))$

                                         $Φ((∃x)\sim φ(x))$ $Φ(\sim (∀x)φ(x))$

                                         $Φ(\sim (∃xφ)(x))$ $Φ((∀x)\sim φ(x))$

                                         $Φ((∀x)\sim φ(x))$ $Φ(\sim (∃x)φ(x))$

--------------------------------------------------------------------------
