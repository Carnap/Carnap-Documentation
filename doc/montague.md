# Natural Deduction in the Carnap Book

This document gives a short description of the systems of natural deduction
used in the Carnap book, and the two available second-order extensions of these
systems. At least some prior familiarity with Montague-style proof systems is
assumed.

## The Propositional System

### Notation

The different admissible keyboard abbreviations for the different connectives
is as follows:

<div class="table">

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
∧          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

</div>

The available sentence letters are $P$ through $W$, and the infinitely many
subscripted letters $P_1, P_2,\ldots$ written `P_1, P_2` and so on.

Proofs consist of a series of lines. A line is either an assertion line
containing a formula followed by a `:` and then a justification for that
formula, a show line consisting of the word `show` followed by a formula, or a
QED line containing a `:` followed by a rule for an indirect inference.

A subproof begins a new show line. The next line should be more indented than
the containing proof, and the lines directly contained in this subproof should
maintain this indentation level. (Lines indirectly contained, by being part of
a sub-sub-proof, will need to be indented more deeply.) The subproof ends with
a QED line at the same level of indentation as the containing proof.

For example:

```{.Playground .Prop options="render resize fonts"}
Show P -> (P -> P)
   P:AS
   Show: P->P
      P:AS
   :CD 4
:CD 3
```

### Basic Rules

The propositional part of the system (the system used in a proofchecker
constructed with `.Prop` in Carnap's [Pandoc
Markup](pandoc.md)) has the following set
of rules for direct inferences:

<div class="table">

Rule                   Abbreviation Premises     Conclusion
---------------------- ------------ ------------ -----------
Simplification         `S`          $φ∧ψ$        $φ/ψ$        
Adjunction             `ADJ`        $φ,ψ$        $φ∧ψ$
Modus Ponens           `MP`         $φ,φ→ψ$      $ψ$
Modus Tollens          `MT`         $¬ψ,φ→ψ$     $¬φ$
Modus Tollendo Ponens  `MTP`        $¬ψ/¬φ,φ∨ψ$  $φ/ψ$
Addition               `ADD`        $φ/ψ$        $φ∨ψ$
Conditional to Bicond. `CB`         $ψ→φ, φ→ψ$   $ψ↔φ$
Biconditional to Cond. `BC`         $ψ↔φ$        $ψ→φ/φ→ψ$
Double Negation Intro. `DNI`        $φ$          $¬¬φ$
Double Negation Elem.  `DNE`        $¬¬φ$        $φ$
Double Negation        `DN`         $φ/¬¬φ$      $¬¬φ/φ$
---------------------- ------------ ------------ -----------

</div>

We also have three rules for indirect inferences: `DD`, which closes a show
line of the form $Show: φ$ by citing an available line containing $φ$ , `CD`
which closes a show line of the form $Show: φ→ψ$ by citing an available line
containing $ψ$, and cancels the assumption $φ$ if it is used to support this
line, and `ID`, which choses a show line of the form $Show: ¬φ$ by citing two
available lines containing $ψ$ and $¬ψ$, canceling the assumption $φ$ if it is
used to support these lines.

Finally, `PR` can be used to justify a line asserting a premise, and `AS` can
be used to justify a line making an assumption.

### Derived Rules

Additional rules previously derived by users are allowed. These are regular
rules of direct inference, and use abbreviations of the form `D-NAME`, where
`NAME` is chosen by the user.

## The First Order System

### Notation

The different admissible keyboard abbreviations for quantifiers and equality is
as follows:

<div class="table">

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

</div>

Sentence letters are as in the propositional system.

Application of a function or relation symbol is indicated by wrapping a
comma-separated list of arguments in parentheses, and appending this to the
symbol.

The available relation symbols are $F$ through $O$, with the infinitely many
subscripted letters $F_1, F_2,\ldots$ written `F_1, F_2,…`. The arity of a
relation symbol is determined from context.

The available constants are $a$ through $e$, with the infinitely many
subscripted letters $c_1, c_2,\ldots$ written `c_1, c_2,…`. 

The available function symbols are $f$ through $h$, with the infinitely many
subscripted letters $f_1, f_2,\ldots$ written `f_1, f_2,…`. The arity of a
function symbol is determined from context.

The available variables are $v$ through $z$, with the infinitely many
subscripted letters $x_1, x_2,\ldots$ written `x_1, x_2,…`.

### Basic Rules

The first-order part of the system (the system used in a proofchecker
constructed with `.FirstOrder`) extends the propositional part of the system
with the following set of new basic rules:

<div class="table">

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Leibniz's Law               `LL`         $τ=σ, φ(τ)/φ(σ)$   $φ(σ)/φ(τ)$

Leibniz's Law (negative)    `LL`         $φ(τ),¬φ(σ)$       $¬(τ=σ)$

Euclid's Law                `EL`         $τ=σ$              $θ(τ) = θ(σ)$

Universal Instantiation     `UI`         $∀xφ(x)$           $φ(τ)$

Existential Generalization  `EG`         $φ(τ)$             $∃xφ(x)$

Quantifier Negation         `QN`         $¬∀xφ(x)/          $∃x¬φ(x)/
                                         ¬∃xφ(x)/           ∀x¬φ(x)/
                                         ∃¬xφ(x)/           ¬∀xφ(x)/
                                         ∀¬xφ(x)$           ¬∃xφ(x)$

Symmetry                    `Sm`         $τ=σ$              $σ=τ$

Reflexivity                 `ID`                            $τ=τ$
--------------------------------------------------------------------------

</div>

It also adds two new rules for indirect derivations: `UD`, which closes a show
line of the form $Show: ∀xφ(x)$ by citing an available line $φ(a)$, where $a$
is a fresh constant[^1] , and `ED` which closes a show line of the form $Show:
ψ$ by citing an assertion of the form $∃xφ(x)$, an assumption of the form
$φ(a)$ and an assertion of the form $ψ$, and cancels the assumption $φ(a)$,
where $a$ is a fresh constant.[^2]

[^1]: A fresh constant is one not appearing in the statement on the show line
or in any assumption or premise on which the justifications for the show
line depends, other than assumptions cancelled by the inference rule in
question. For pedagogical purposes, it's easiest to say that a constant is
fresh if it does not appear outside of the given subproof.

[^2]: The fact that $φ(a)$ needs to be cited as a premise is undesirable, and
will be changed relatively soon, pending some improvements to the proof
checking algorithm.

### Traditional Kalish and Montague Rules

The basic rules for first-order logic listed above are not precisely the same
as the rules given by Kalish and Montague in *Formal Logic*. In particular,
universal derivations work differently, and existential derivations are
replaced by a rule of existential instantiation. 

Universal Derivations in *Formal Logic* closing a show line of the form $Show:
∀xφ(x)$ are required to end by citing an available line $\phi(x)$ in which
$\phi$ occurs with precisely the same variable free as we see bound in $\forall
x\phi(x)$. Furthermore, the variable $x$ must not occur free on any line
available from the salient show line.

The rule of `EI` of existential instantiation allows one to infer from a
premise of the form $\exists x\phi(x)$ that $\phi(y)$ for some variable not
occurring *free or bound* on any earlier line in the proof.

These rules can be activated by using `.MontagueQC` (for "Quantifier Calculus")
instead of `.FirstOrder` in the construction of the proof-checker.

## The Monadic Second-Order System 

### Notation

The different admissible keyboard abbreviations for monadic second-order
lambdas is as follows:

<div class="table">

Connective Keyboard 
---------- ----------
λ          \\
---------- ----------

</div>

First order syntax is as in the first-order system.

The available second-order variables are $X$ through $Z$, with the infinitely
many subscripted variables $X_1, X_2,\ldots$ written `X_1, X_2,…`.

A lambda abstract has the form $λx[φ(x)]$, and can be applied like a predicate.
Lambdas can only be applied to formulas, so the only abstracts that can be
produced are for monadic relations.

### Basic Rules

The monadic second-order system (the system used in a proofchecker constructed
with `.SecondOrder`) extends the first-order part of the system with the
following set of new basic rules:

<div class="table">

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Abstraction                 `ABS`        $φ(σ)$             $λx[φ(x)](σ)$

Application                 `APP`        $λx[φ(x)](σ)$      $φ(σ)$

Monadic Univ. Instantiation `UI`         $∀XΦ(X)$           $Φ(ζ)$

Monadic Ex. Generalization  `EG`         $Φ(ζ)$             $∃XΦ(X)$
--------------------------------------------------------------------------

</div>

Where ζ is schematic for a unary lambda term. 

And with rules for indirect derivation UD and EG exactly analogous to the
first-order case, except that a fresh second-order variable  is used rather
than a fresh constant.

## The Polyadic Second-Order System 

### Notation

First order syntax is as in the first-order system.

The available 2nd-order $n$-ary variables are $XN$ through $ZN$ (where $N$ is
replaced by the arity of the variable), with the infinitely many subscripted
variables $XN_1, XN_2,\ldots$ written `XN_1, XN_2,…`.

A lambda abstract has the form $λx_1…λx_n[φ(x_1,…,x_n)]$, and can be applied
like an $n$-ary relation symbol.

### Basic Rules

The polyadic second-order system (the system used in a proofchecker constructed
with `.PolySecondOrder`) extends the first-order part of the system with the
following set of new basic rules:

<div class="table">

--------------------------------------------------------------------------------------------------------------------------
Rule                        Abbreviation Premises                             Conclusion
--------------------------- ------------ ------------------------------------ --------------------------------------------
$n$-Abstraction               `ABSN`       $φ(σ_1,…,σ_n)$                       $λx_1…x_n[φ(x_1,…,x_n)](σ_1,…σ_n)$

$n$-Application               `APPN`       $λx_1…x_n[φ(x_1,…,x_n)](σ_1,…σ_n)$   $φ(σ_1,…,σ_n)$

$n$-ary Univ. Instantiation   `UIN`        $∀XNΦ(XN)$                           $Φ(ζ^n)$

$n$-ary Ex. Generalization    `EGN`        $Φ(ζ^n)$                             $∃XNΦ(XN)$
--------------------------------------------------------------------------------------------------------------------------

</div>

Where $ζ^n$ is schematic for an $n$-ary lambda term.

And with rules of $n$-ary universal and existential derivation `UDN` and `EGN`
exactly analogous to the first-order case, except that a fresh second-order
variable is used rather than a fresh constant.
