# Chains of equivalences

This document gives a short description of how Carnap presents the
systems of "chains of equivalences" that allow transformations of
sentences into equivalent sentences, e.g., in disjunctive or
conjunctive normal form.

## Notation

The system uses the parser/syntax of [*forall x: Calgary*](systems.md#thomas-bolduc-zach-forall-x-calgary) and the *Open
Logic Text*.

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
∀          `A`, `@`
∃          `E`, `3`
---------- ----------

</div>

Proofs consist of a series of lines. Every line contains a formula
followed by a `:` and then a rule abbreviation. The first line is
justified by `:PR`.  The available rules are all equivalences, and can
be applied to subformulas of a given formula.  It is assumed that
every line follows from the immediately preceding line by one of the
equivalence rules below. 

## Equivalences for TFL (propositional logic)

The equivalence proof checker is selected
using `.ZachPropEq`.

```{.ProofChecker .ZachPropEq}
Ex1 A \/ ~(B \/ C) :|-: (A \/ ~C) /\ (A \/ ~B)
|A \/ ~(B \/ C) :PR
|A \/ ~(C \/ B) :Comm
|A \/ (~C /\ ~B) :DeM
|(A \/ ~C) /\ (A \/ ~B) :Dist
```

The following exchange rules are allowed. They can be used within a
propositional context Φ:

<div class="table">

Rule                   Abbreviation Premises          Conclusion
---------------------- ------------ ----------------- -----------
Double Negation        `DN`         $Φ(φ)/Φ(¬¬φ)$     $Φ(¬¬φ)/Φ(φ)$
Conditional            `Cond`       $Φ(φ→ψ)$          $Φ(¬φ∨ψ)$
                                    $Φ(¬φ∨ψ)$         $Φ(φ→ψ)$      
                                    $Φ(φ∨ψ)$          $Φ(¬φ→ψ)$
                                    $Φ(¬φ→ψ)$         $Φ(φ∨ψ)$      
Biconditional Exchange `Bicond`     $Φ(φ↔ψ)$          $Φ(φ→ψ∧ψ→φ)$
                                    $Φ(φ→ψ∧ψ→φ)$      $Φ(φ↔ψ)$      
DeMorgan's Laws        `DeM`        $Φ(¬(φ∧ψ))$       $Φ(¬φ∨¬ψ)$
                                    $Φ(¬(φ∨ψ))$       $Φ(¬φ∧¬ψ)$
                                    $Φ(¬φ∨¬ψ)$        $Φ(¬(φ∧ψ))$
                                    $Φ(¬φ∧¬ψ)$        $Φ(¬(φ∨ψ))$
Commutativity          `Comm`       $Φ(φ∧ψ)$          $Φ(ψ∧φ)$
                                    $Φ(φ∨ψ)$          $Φ(ψ∨φ)$
Associativity          `Assoc`      $Φ(φ∧(ψ∧χ))$      $Φ((φ∧ψ)∧χ)$
                                    $Φ((φ∧ψ)∧χ)$      $Φ(φ∧(ψ∧χ))$
                                    $Φ(φ∨(ψ∨χ))$      $((φ∨ψ)∨χ)$
                                    $((φ∨ψ)∨χ)$       $Φ(φ∨(ψ∨χ))$      
Distributivity         `Dist`       $Φ(φ∨(ψ∧χ))$      $Φ((φ∨ψ)∧(φ∨χ))$
                                    $Φ((φ∨ψ)∧(φ∨χ))$  $Φ(φ∨(ψ∧χ))$
                                    $Φ(φ∧(ψ∨χ))$      $((φ∧ψ)∨(φ∧χ))$
                                    $((φ∧ψ)∨(φ∧χ))$   $Φ(φ∧(ψ∨χ))$
Idempotence            `Id`         $Φ(φ∧φ)$          $Φ(φ)$
                                    $Φ(φ)$            $Φ(φ∧φ)$
                                    $Φ(φ∨φ)$          $Φ(φ)$
                                    $Φ(φ)$            $Φ(φ∨φ)$
Absorption             `Abs`        $Φ(φ∧(φ∨ψ))$      $Φ(φ)$
                                    $Φ(φ)$            $Φ(φ∧(φ∨ψ))$
                                    $Φ(φ∨(φ∧ψ))$      $Φ(φ)$
                                    $Φ(φ)$            $Φ(φ∨(φ∧ψ))$
Simplification         `Simp`       $Φ(φ∧(ψ∨¬ψ))$     $Φ(φ)$
                                    $Φ(φ∨(ψ∧¬ψ))$     $Φ(φ)$
                                    $Φ(φ∨(ψ∨¬ψ))$     $Φ(ψ∨¬ψ)$
                                    $Φ(φ∧(ψ∧¬ψ))$     $Φ(ψ∧¬ψ)$
---------------------- ------------ ----------------- ------------

</div>
The rules for distributivity, absorption, and simplification allow for
implicit commutativity, so e.g., `Distr` also allows replacing
$(ψ∧χ)∨φ$ by $(ψ∨φ)∧(χ∨φ)$, and `Simp` allows replacing $(¬ψ∨ψ)∧φ$ by
$φ$.

If the conclusion of the target entailment is left empty, and the
`tests` option is set, the checker will accept any proof where the
last line meets the test. So for instance, to require students to
transform a sentence into conjunctive normal form, you would assign

    ```{.ProofChecker .ZachPropEq tests="CNF"}
    Ex1 A \/ ~(B \/ C) :|-: 
    |A \/ ~(B \/ C) :PR
    ```

```{.ProofChecker .ZachPropEq tests="CNF"}
Ex1 A \/ ~(B \/ C) :|-: 
|A \/ ~(B \/ C) :PR
```

A proof playground is also supported.

    ```{.Playground .ZachPropEq}
    ```

```{.Playground .ZachPropEq}
```

The available tests are the same as for [translation
exercises](translations.md), and can be combined. If combined, multiple
tests have to be separated by spaces.

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

## The FOL Systems

The system `.ZachFOLEq` extends the rules of `.ZachPropEq` by
equivalence rules for quantifiers. Those are:

<div class="table">

Rule                        Abbreviation Premises            Conclusion
--------------------------- ------------ ------------------- --------------
Variable Renaming           `VR`         $∀ x\,φ(x)$         $∀ y\,φ(y)$
                                         $∃ x\,φ(x)$         $∃ y\,φ(y)$
Quantifier Negation         `QN`         $¬∀xφ(x)$           $∃x¬φ(x)$
                                         $∃x¬φ(x)$           $¬∀xφ(x)$
                                         $¬∃xφ(x)$           $∀x¬φ(x)$
                                         $∀x¬φ(x)$           $¬∃xφ(x)$
Quantifier Distribution     `QD`         $∀ x(φ(x) ∧ ψ(x))$  $∀ x\,φ(x) ∧ ∀ x\,ψ(x)$
                                         $∃ x(φ(x) ∨ ψ(x))$  $∃ x\,φ(x) ∨ ∀ x\,ψ(x)$
Quantifier Shift for $∀$    `QSA`        $∀ x(φ(x) ∧ ψ)$     $∀ x\,φ(x) ∧ ψ$
                                         $∀ x\,φ(x) ∧ ψ$     $∀ x(φ(x) ∧ ψ)$
                                         $∀ x(φ(x) ∨ ψ)$     $∀ x\,φ(x) ∨ ψ$
                                         $∀ x\,φ(x) ∨ ψ$     $∀ x(φ(x) ∨ ψ)$
                                         $∀ x(φ(x) → ψ)$     $∃ x\,φ(x) → ψ$
                                         $∃ x\,φ(x) → ψ$     $∀ x(φ(x) → ψ)$
                                         $∀ x(ψ → φ(x))$     $ψ → ∀ x\,φ(x)$
                                         $ψ → ∀ x\,φ(x)$     $∀ x(ψ → φ(x))$
Quantifier Shifts for $∃$    `QSE`       $∃ x(φ(x) ∧ ψ)$     $∃ x\,φ(x) ∧ ψ$
                                         $∃ x\,φ(x) ∧ ψ$     $∃ x(φ(x) ∧ ψ)$
                                         $∃ x(φ(x) ∨ ψ)$     $∃ x\,φ(x) ∨ ψ$
                                         $∃ x\,φ(x) ∨ ψ$     $∃ x(φ(x) ∨ ψ)$
                                         $∃ x(φ(x) → ψ)$     $∀ x\,φ(x) → ψ$
                                         $∀ x\,φ(x) → ψ$     $∃ x(φ(x) → ψ)$
                                         $∃ x(ψ → φ(x))$     $ψ → ∃ x\,φ(x)$
                                         $ψ → ∃ x\,φ(x)$     $∃ x(ψ → φ(x))$
--------------------------- ------------ ------------------- --------------

</div>

Note that Carnap actually considers all formulas equal up to renaming
of bound variables. Thus, the `VR` rules are provided just for
completeness (and will allow any numer of renamings of bound
variables).  Any variable renaming necessary to apply a quantifier
shift can be done implicitly without first invoking the `VR` rule.

The FOL system has an additional test, `PNF`, that requires the final
line to be in prenex normal form.

    ```{.ProofChecker .ZachFOLEq options="resize" feedback="manual" tests="PNF"}
    Ex2 ~(Ax P(x) <-> Ey Q(y)) :|-: 
    |~(Ax P(x) <-> Ey Q(y)) :PR
    ```

```{.ProofChecker .ZachFOLEq options="resize" feedback="manual" tests="PNF"}
Ex2 ~(Ax P(x) <-> Ey Q(y)) :|-: 
|~(Ax P(x) <-> Ey Q(y)) :PR
|~((Ax P(x) -> Ey Q(y)) /\ (Ey Q(y) -> Ax P(x))) :Bicond
|~(Ax P(x) -> Ey Q(y)) \/ ~(Ey Q(y) -> Ax P(x)) :DeM
|~(Ax P(x) -> Ey Q(y)) \/ ~Ay( Q(y) -> Ax P(x)) :QSA
|~(Ax P(x) -> Ey Q(y)) \/ ~AyAx( Q(y) ->  P(x)) :QSA
|~(Ax P(x) -> Ey Q(y)) \/ Ey~Ax( Q(y) ->  P(x)) :QN
|~(Ax P(x) -> Ey Q(y)) \/ EyEx~( Q(y) ->  P(x)) :QN
|(Ax P(x) /\ ~Ey Q(y)) \/ EyEx~( Q(y) ->  P(x)) :Cond
|(Ax P(x) /\ Ay~ Q(y)) \/ EyEx~( Q(y) ->  P(x)) :QN
|(Ax P(x) /\ Ax~ Q(x)) \/ EyEx~( Q(y) ->  P(x)) :VR
|Ax(P(x) /\ ~Q(x)) \/ EyEx~( Q(y) ->  P(x)) :QD
|Ey[Ax(P(x) /\ ~Q(x)) \/ Ex~( Q(y) ->  P(x))] :QSE
|EyEx[Ax(P(x) /\ ~Q(x)) \/ ~( Q(y) ->  P(x))] :QSE
```
