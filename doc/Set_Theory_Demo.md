#Set Theory Demo

Here's a demo of Carnap's (alpha-stage) support for natural deduction in set
theory.

The rules are those of the Carnap book's first-order system (The one used in a
proof checker constructed with `.FirstOrder`—See the documentation for
[Montague Systems](montague.md)), plus
the following bi-directional replacement rules:

<div class="table">

--------------------------------------------------------------------------
Rule                        Abbreviation Premises           Conclusion
--------------------------- ------------ ------------------ --------------
Union Definition            `Def-U`      $Φ(τ∈σ∨τ∈θ)$       $Φ(x∈σ∪θ)$

Intersection Definition     `Def-I`      $Φ(τ∈σ∧τ∈θ)$       $Φ(x∈σ∩θ)$

Complement Definition       `Def-C`      $Φ(τ∈σ∧¬τ∈θ)$      $Φ(x∈σ/θ)$

Power Set Definition        `Def-P`      $Φ(τ⊆θ)$           $Φ(τ∈Pow(θ))$

Subset Definition           `Def-S`      $Φ(∀x(x∈τ→x∈θ))$   $Φ(τ⊆θ)$

Separation Definition       `Def-{}`     $Φ(τ∈θ∧φ(τ))$      $Φ(τ∈{x∈θ|φ(x)})$

Equality Definition         `Def-=`      $Φ(∀x(x∈τ↔x∈σ))$   $Φ(τ=σ)$
--------------------------------------------------------------------------

</div>

Symbols are:

<div class="table">

Symbol     Keyboard 
---------- ----------
∩          `I`
∪          `U`,
∈          `in`, `<<`, `<e` 
⊆          `within`, `<(`, `<s`
---------- ----------

</div>

Here's an example proof:

```{.Playground .SeparativeST init="now"}
Ax(x in a -> x within a) :PR
Show P(a) within P(P(a))
 Show Ax(x in P(a) -> x in P(P(a)))
  Show b in P(a) -> b in P(P(a))
   b in P(a) :AS
   b within a:Def-P 5
   Ax(x in b -> x in a):Def-S 6
   Show b in P(P(a))
    Show Ax(x in b -> x in P(a))
     Show c in b -> c in P(a)
      c in b :AS
      c in b -> c in a:UI 7
      c in a :MP 11 12
      c in a -> c within a :UI 1
      c within a:MP 13 14
      c in P(a):Def-P 15
     :CD 16
    :UD10
    b within P(a):Def-S 9
    b in P(P(a)):Def-P 19
   :DD 20
  :CD 8
 :UD 4
 P(a) within P(P(a)):Def-S 3
:DD 24
```
