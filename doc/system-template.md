# The XXX Proof System

Carnap supports proofs in the Fitch-style/Montague-style/Lemmon-style
proof system used in AUTHOR, [BOOK TITLE](LINK). 

## Proof layout

DESCRIBE FORMAT OF PROOFS; HERE FOR MONTAGUE STYLE:

Proofs consist of a series of lines. A line is either an assertion
line containing a formula followed by a `:` and then a justification
for that formula, a show line consisting of the word `show` followed
by a formula, or a QED line containing a `:` followed by a rule for an
indirect inference.

A show line begins a new subproof. The next line should be more
indented than the containing proof, and the lines directly contained
in this subproof should maintain this indentation level. (Lines
indirectly contained, by being part of a sub-sub-proof, will need to
be indented more deeply.) The subproof ends with a QED line at the
same level of indentation as the containing proof.

HERE FOR FITCH STYLE:

Proofs consist of a series of lines. A line is either an assertion
line containing a formula followed by a `:` and then a justification
for that formula, or a separator line containing two dashes, thus:
`--`.[^1] A justification consists of 

- zero or more numbers (citations of particular lines) and pairs of
  numbers separated by a dash (citations of a subproof contained
  within the given line range), followed by 
- the name of a rule being applied.

[SWITCH ORDER IF REQUIRED]

[^1]: These are intended for use when you have two contiguous subproofs and
need to separate them - since they're at the same level of indentation, you
need some extra indication to show that they're distinct subproofs.

A subproof is begun by increasing the indentation level. The first
line of a subproof should be more indented than the containing proof,
and the lines directly contained in this subproof should maintain this
indentation level. (Lines indirectly contained, by being part of a
sub-sub-proof, will need to be indented more deeply.) The subproof
ends when the indentation level of the containing proof is resumed.
Two contiguous sub-proofs of the same containing proof can be
distinguished from one another by inserting a separator line between
them at the same level of indentation as the containing proof. The
final *unindented* line of a derivation will serve as the conclusion
of the entire derivation.

NO LEMMON-STYLE SYSTEM DOCUMENTED YET

For example:

GIVE EXAMPLES

MONTAGUE: 

```{.Playground .SYSTEM-PROPOSITIONAL options="render resize fonts" init="now"}
Show P -> (P -> P)
   P:AS
   Show: P->P
      P:AS
   :CD 4
:CD 3
```

FITCH:

```{.Playground .SYSTEM-PROPOSITIONAL  options="resize render fonts" init="now"}
   P        :AS
      P     :AS
      P     :2 R
   P > P    :2-3 CI
P > (P > P) :1-4 CI
```

LEMMON:

## The Propositional System

### Notation

The different admissible keyboard abbreviations for the different
connectives is as follows:

<div class="table">

COPY TABLE FROM [systems.md](systems.md)

</div>

CHANGE AS NECESSARY:

The available sentence letters are $P$ through $W$, and the infinitely many
subscripted letters $P_1, P_2,\ldots$ written `P_1, P_2` and so on.

### Basic Rules

The propositional part of the system is selected by
`.SYSTEM-PROPOSITIONAL`. It has the following set of rules for direct
inferences:

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

We also have three rules for indirect inferences: `DD`, which closes a
show line of the form $Show: φ$ by citing an available line containing
$φ$ , `CD` which closes a show line of the form $Show: φ→ψ$ by citing
an available line containing $ψ$, and cancels the assumption $φ$ if it
is used to support this line, and `ID`, which choses a show line of
the form $Show: ¬φ$ by citing two available lines containing $ψ$ and
$¬ψ$, canceling the assumption $φ$ if it is used to support these
lines.

Finally, `PR` can be used to justify a line asserting a premise, and
`AS` can be used to justify a line making an assumption.

## The First Order System

### Notation

The different admissible keyboard abbreviations for quantifiers and
equality is as follows:

<div class="table">

COPY TABLE FROM [systems.md](systems.md)

</div>

CHANGE AS NECESSARY:

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

Example

EXAMPLE PREDICATE PROOF EG FOR FITCH-STYLE

```{.Playground .SYSTEM-PREDICATE options="resize render" guides="fitch" init="now"}
(Ax)Fx        :PR
(Ax)(Fx > Gx) :PR
Fa            :1 AE
Fa > Ga       :2 AE
Ga            :3,4 >E 
(Ax)Gx        :5 AI 
```

### Basic Rules

The first-order part of the system is selected by `.SYSTEM-PREDICATE`.
It extends the propositional part of the system with the following set
of new basic rules:

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

It also adds two new rules for indirect derivations: `UD`, which
closes a show line of the form $Show: ∀xφ(x)$ by citing an available
line $φ(a)$, where $a$ is a fresh constant[^1] , and `ED` which closes
a show line of the form $Show: ψ$ by citing an assertion of the form
$∃xφ(x)$, an assumption of the form $φ(a)$ and an assertion of the
form $ψ$, and cancels the assumption $φ(a)$, where $a$ is a fresh
constant.[^2]

[^1]: A fresh constant is one not appearing in the statement on the
show line or in any assumption or premise on which the justifications
for the show line depends, other than assumptions cancelled by the
inference rule in question. For pedagogical purposes, it's easiest to
say that a constant is fresh if it does not appear outside of the
given subproof.

[^2]: The fact that $φ(a)$ needs to be cited as a premise is
undesirable, and will be changed relatively soon, pending some
improvements to the proof checking algorithm.

