# Natural Deduction in the *forall x: Calgary* systems

This document gives a short description of how Carnap presents the
systems of natural deduction from [*forall x:
Calgary*](http://forallx.openlogicproject.org/), the remix by Aaron
Thomas-Bolduc and Richard Zach of Tim Button's Cambridge version of
P.D. Magnus's *forall x*.

The systems supported come in two versions, with slightly different
rules and different syntax in the first-order part: those for versions
of the book before Fall 2019, and those for the Fall 2019 edition and
after.  The versions for the pre-2019 editions are practically the
same as the systems in Tim Button's [*forall x:
Cambridge*](http://www.homepages.ucl.ac.uk/~uctytbu/OERs.html), except
that the LEM rule is called TND in Button's text.

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

Proofs consist of a series of lines. A line is either an assertion line
containing a formula followed by a `:` and then a justification for that
formula, or a separator line containing two dashes, thus: `--`. A
justification consists of a rule abbreviation followed by zero or more numbers
(citations of particular lines) and pairs of numbers separated by a dash
(citations of a subproof contained within the given line range).

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

Here's an example derivation, using the TFL system `.ZachTFL`:

```{.ProofChecker .ZachTFL options="render resize fonts" init="now"}
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

```{.Playground .ZachTFL options="render resize fonts render" guides="fitch" init="now"}
|   A \/ B:AS
|      A:AS
|      B \/ A:\/I 2
|   --
|      B:AS
|      B \/ A:\/I 5
|   B \/ A:\/E 1,2-3,5-6
|(A \/ B) -> (B \/ A):->I 1-7
```

### The TFL systems

The system `.ZachTFL` allows all rules below. `.ZachTFL2019` is like
`.ZachTFL` except it *disallows* all derived rules, i.e., the only
allowed rules are `R`, `X`, `IP`, and the I and E rules for the
connectives. 

It has the following set of rules for direct inferences:

<div class="table">
Basic rules:

Rule                   Abbreviation Premises     Conclusion
---------------------- ------------ ------------ -----------
And-Elim.              `∧E`         $φ∧ψ$        $φ/ψ$        
And-Intro.             `∧I`         $φ,ψ$        $φ∧ψ$
Or-Intro               `∨I`         $φ/ψ$        $φ∨ψ$
Negation-Elim          `¬E`         $φ,¬φ$       $⊥$
Explosion              `X`          $⊥$          $ψ$
Biconditional-Elim     `↔E`         $φ/ψ,φ↔ψ$    $ψ/φ$
---------------------- ------------ ------------ ------------

Derived rules:

Rule                   Abbreviation Premises     Conclusion
---------------------- ------------ ------------ -----------
Reiteration            `R`          $φ$          $φ$
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
4. `IP` (indirect proof), which justifies an assertion of the form $φ$ by citing
   a subproof beginning with the assumption $¬φ$ and ending with a conclusion
   $⊥$.
6. `LEM` (Law of the Excluded Middle), which justifies an assertion of the form
   $ψ$ by citing two subproofs beginning with assumptions $φ,¬φ$ respectively and
   each ending with the conclusion $ψ$. LEM is a derived rule.

Finally, `PR` can be used to justify a line asserting a premise, and `AS` can
be used to justify a line making an assumption. A note about the reason for an
assumption can be included in the rendered proof by writing `A/NOTETEXTHERE`
rather than `AS` for an assumption. Assumptions are only allowed on the first
line of a subproof.


## First-order logic

There are three proof systems corresponding to the Calgary remix of _forall
x_. All of them allow sentence letters in first-order formulas. The
available relation symbols are the same as for TFL: $A$ through $Z$,
together with the infinitely many subscripted letters $F_1,
F_2,\ldots$ written `F_1, F_2` etc. However, the available constants
and function symbols are only $a$ through $r$, together with the
infinitely many subscripted letters $c_1, c_2,\ldots$ written `c_1,
c_2,…`. The available variables are $s$ through $z$, with the
infinitely many subscripted letters $x_1, x_2,\ldots$ written `x_1,
x_2,…`.

As of the Fall 2019 edition of *forall x: Calgary*, the syntax for
first-order formulas has arguments to predicates in parentheses and
with commas (e.g., $F(a, b)$); prior to that edition, the convention
was the same as in the original and Cambridge editions of *forall x*
(e.g., $Fab$).

<div class="table">

Connective Keyboard 
---------- ----------
∀          `A`, `@`
∃          `E`, `3`
=          `=`
---------- ----------

</div>

The first-order *forall x: Calgary* systems for FOL extend the rules of
the system TFL with the following set of new basic rules:

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

There is one new rule for indirect derivations: `∃E`, which justifies
an assertion $ψ$ by citing an assertion of the form $∃xφ(x)$ and a
subproof beginning with the assumption $φ(σ)$ and ending with the
conclusion $ψ$, where $σ$ does not appear in $ψ, ∃xφ(x)$, or in any of
the undischarged assumptions or premises of the proof.

The original proof system for the Calgary version of *forall x*,
`.ZachFOL` adds, in addition to the (basic and derived) rules of
`.ZachTFL`, the rules

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

The 2019 versions of the FOL systems use the new syntax, i.e., $F(a,
b)$ instead of $Fab$. The system `.ZachFOL2019` allows only the basic
rules of the TFL system and the basic rules of FOL. The system
`.ZachFOLPlus2019` allows the basic and derived rules of `.ZachTFL`
and the CQ rules listed above.

In summary:

<div class="table">

System              TFL Rules        FOL Syntax  FOL Rules  
------------------- ---------------- ----------- -----------
`.ZachTFL`          Basic + Derived                         
`.ZachFOL`          Basic + Derived  Fab         Basic + CQ 
`.ZachTFL2019`      Basic                                   
`.ZachFOL2019`      Basic            F(a,b)      Basic      
`.ZachFOLPlus2019`  Basic + Derived  F(a,b)      Basic + CQ 
------------------- ---------------- ----------- -----------

</div>
