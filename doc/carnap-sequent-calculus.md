#Sequent Calculus Deductions

The `Sequent` class indicates that a code block will contain sequent-calculus
deduction exercises, which require the production of a sequent calculus
deduction.

These problems use [ProofJS](https://github.com/gleachkr/proofjs) for their
user interface. An initial click may be required to select a node. Once a node
is selected, `Enter` will create a sibling node (on any node but the root),
`Ctrl-Enter` will create a new child node, and `Ctrl-Shift-Enter` will create a
new parent node (on any node but the root node). Nodes can be selected by
either pressing `Tab` and `Shift-Tab` to cycle, or by using the mouse. Changes
can be undone and redone with `Ctrl-Z` and `Shift-Ctrl-Z` respectively. The
subtree above a selected node can be deleted with `Ctrl-Backspace`, and
subtrees can be cut-copy-pasted with `Shift-Ctrl-X`, `Shift-Ctrl-C` and
`Shift-Ctrl-V` respectively.

##Available Systems

At the moment, four systems are available:

<div class="table">

System   Description
-------- --------------------------------------------------------------
propLK   A system based on the propositional fragment of Gentzen's LK
propLJ   A system based on the propositional fragment of Gentzen's LJ
foLK     A system based on the full first order system of LK
foLJ     A system based on the full first order system of LJ
-------- --------------------------------------------------------------

</div>

Exercises are given by specifying the desired endsequent. So an exercise can be
constructed like so:

    ```{.Sequent .propLK}
    1.1 P->Q, Q->R :|-: P->R
    ```

which produces:

```{.Sequent .propLK}
1.1 P->Q, Q->R :|-: P->R
```

(Remember to click on a node in order to interact, and to press `Ctrl-Enter` to
create the first child node)

A completed proof will look like this:

```{.Sequent .propLK init="now" options="displayJSON"}
1.2 P, P->Q :|-: Q
| {"ident":11,"label":"P->Q,P:|-:Q","rule":"->L","forest":[{"ident":12,"label":"Q,P:|-:Q","rule":"Cut","forest":[{"ident":13,"label":"R,P,Q:|-:Q","rule":"XL","forest":[{"ident":58,"label":"Q,P,R:|-:Q","rule":"WL","forest":[{"ident":59,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":14,"label":"","rule":"","forest":[]}]}]}]},{"ident":14,"label":"Q,P:|-:Q,R","rule":"XR","forest":[{"ident":57,"label":"Q,P:|-:R,Q","rule":"WR","forest":[{"ident":10,"label":"Q,P:|-:Q","rule":"WL","forest":[{"ident":12,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":13,"label":"","rule":"","forest":[]}]}]}]}]}]},{"ident":15,"label":"P:|-:Q,P","rule":"WR","forest":[{"ident":16,"label":"P:|-:P","rule":"Ax","forest":[{"ident":11,"label":"","rule":"","forest":[]}]}]}]}
```

With `:|-:` indicating a turnstile, and rule names to the right of inference lines.

##Rules for LK and LJ

Here's a brief summary of LK's propositional "operational" rules:

<div class="table">

Rule    Premise Sequents     Conclusion Sequent
-----   ------------------   ---------------------------
`&R`    Γ ⊢ Δ,φ ; Γ ⊢ Δ,ψ    Γ ⊢ Δ, φ & ψ
`&L`    φ, Γ ⊢ Δ             φ & ψ, Γ ⊢ Δ
`&L`    ψ, Γ ⊢ Δ             φ & ψ, Γ ⊢ Δ
`∨L`    φ, Γ ⊢ Δ ; ψ, Γ ⊢ Δ  φ ∨ ψ, Γ ⊢ Δ   
`∨R`    Γ ⊢ Δ, φ             Γ ⊢ Δ, φ ∨ ψ
`∨R`    Γ ⊢ Δ, ψ             Γ ⊢ Δ, φ ∨ ψ
`→L`    Γ ⊢ Δ, φ; ψ, Γ ⊢ Δ   φ → ψ, Γ ⊢ Δ
`→R`    φ, Γ ⊢ Δ, ψ          Γ ⊢ Δ, φ → ψ
`¬L`    Γ ⊢ Δ, φ             ¬φ, Γ ⊢ Δ
`¬R`    φ, Γ ⊢ Δ             Γ ⊢ Δ, ¬φ
-----   -------------------  ----------------------------

</div>

Some structural rules (interchange, and contraction) are applied automatically
to the parts of the sequent that match the Γ and Δ, so there is some room for a
little bit of laxness there.[^1]

[^1]: Variations on the sequent calculus without this simplification will be
supported in the future.

The following explicit structural inferences are allowed:

<div class="table">

Rule    Premise Sequents        Conclusion Sequent
-----   ---------------------   ---------------------------
`CR`    Γ ⊢ Δ                   Γ ⊢ Δ
`CL`    Γ ⊢ Δ                   Γ ⊢ Δ
`XR`    Γ ⊢ Δ                   Γ ⊢ Δ
`XL`    Γ ⊢ Δ                   Γ ⊢ Δ
`WR`    Γ ⊢ Δ                   Γ ⊢ Δ,Δ'
`WL`    Γ ⊢ Δ                   Γ,Γ' ⊢ Δ
`Cut`   φ, Γ ⊢ Δ ; Γ' ⊢ Δ',φ    Γ,Γ' ⊢ Δ,Δ'
`Ax`                            φ ⊢ φ
-----   ---------------------   ---------------------------

</div>

The contraction and exchange rules are actually redundant here, because of the
fact that structural rules are applied automatically to the formulas
substituted in for Γ,Δ. They're included here for presentation. Weakening is
modified to allow for an arbitrary number of new formulas to be added.

The first order system for LK adds the following rules to the above:

<div class="table">

Rule    Premise Sequents       Conclusion Sequent
-----   --------------------   ---------------------------
`∀L`    φ(τ), Γ ⊢ Δ            ∀υφ(υ), Γ ⊢ Δ
`∃L`    φ(τ), Γ ⊢ Δ            ∃υφ(υ), Γ  ⊢ Δ
`∀R`    Γ ⊢ Δ, φ(τ)            Γ ⊢ Δ, ∀υφ(υ)
`∃R`    Γ ⊢ Δ, φ(τ)            Γ ⊢ Δ, ∃υφ(υ)
-----   --------------------   ---------------------------

</div>

The usual eigenvariable restrictions apply to `∀L` and `∃R`: the term `τ` must
be a constant or variable that does not occur anywhere in the conclusion of the
inference (i.e. not in Γ,Δ, or φ(υ)).

The propositional and first-order systems for LJ are just like those for LK
with the additional restriction that at most one formula can occur on the right
hand side of a sequent.

##Syntax for LK and LJ

As usual, in writing formulas and inference rules, any of `&`,`∧` or `/\ ` can
be used for conjunction, and any of `∨`, `v`, and `\/` can be used for
disjunction. Any of `->` or `→` can be used for the conditional, and any of
`¬`, `-`, or `~` for negation. Sentence letters are `P` through `W` or `P` with
subscripts like so: `P_1`. Predicates are `F` through `L`, or `F` with a
subscript. Variables are `v` through `z` or `x` with a subscript and constants
are `a` through `e` or `c` with a subscript.

##Advanced Usage

###Options

In addition to the standard `points=VALUE` and `submission="none"` options,
sequent calculus exercises allow for you to set `init="now"` to have
proofchecking begin as soon as the proof is loaded (rather than waiting for
input) as well as the following options:

<div class="table">

Name               Effect
------------------ ------------------------------------------------------------------------------
`displayJSON`      `Ctrl-?` will toggle display of an editable JSON representation of the proof
------------------ ------------------------------------------------------------------------------

</div>

###JSON Serialization

Proof 1.2 above was generated using the displayJSON option, with the following
invocation:

    ```{.Sequent .propLK init="now" options="displayJSON"}
    1.2 P, P->Q :|-: Q
    | {"ident":11,"label":"P->Q,P:|-:Q","rule":"->L","forest":[{"ident":12,"label":"Q,P:|-:Q","rule":"Cut","forest":[{"ident":13,"label":"R,P,Q:|-:Q","rule":"XL","forest":[{"ident":58,"label":"Q,P,R:|-:Q","rule":"WL","forest":[{"ident":59,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":14,"label":"","rule":"","forest":[]}]}]}]},{"ident":14,"label":"Q,P:|-:Q,R","rule":"XR","forest":[{"ident":57,"label":"Q,P:|-:R,Q","rule":"WR","forest":[{"ident":10,"label":"Q,P:|-:Q","rule":"WL","forest":[{"ident":12,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":13,"label":"","rule":"","forest":[]}]}]}]}]}]},{"ident":15,"label":"P:|-:Q,P","rule":"WR","forest":[{"ident":16,"label":"P:|-:P","rule":"Ax","forest":[{"ident":11,"label":"","rule":"","forest":[]}]}]}]}
    ```

The `displayJSON` option is useful for saving and communicating proofs, since
one can reproduce a proof by pasting its JSON representation into the panel
where the JSON representation is displayed. It's also useful for creating
exercises in which the problems are partially completed, since, as in the
example above, one can prefill an exercise by supplying a JSON representation
below the statement of the problem (beginning each line of the JSON with a bar
character `|`).

###Playgrounds

You can generate a sequent calculus playground (where there is no goal, but
where what you've proved is displayed) using something like the following:

    ```{.SequentPlayground .propLK init="now" options="displayJSON"}
    {"ident":11,"label":"P->Q,P:|-:Q","rule":"->L","forest":[{"ident":12,"label":"Q,P:|-:Q","rule":"Cut","forest":[{"ident":13,"label":"R,P,Q:|-:Q","rule":"XL","forest":[{"ident":58,"label":"Q,P,R:|-:Q","rule":"WL","forest":[{"ident":59,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":14,"label":"","rule":"","forest":[]}]}]}]},{"ident":14,"label":"Q,P:|-:Q,R","rule":"XR","forest":[{"ident":57,"label":"Q,P:|-:R,Q","rule":"WR","forest":[{"ident":10,"label":"Q,P:|-:Q","rule":"WL","forest":[{"ident":12,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":13,"label":"","rule":"","forest":[]}]}]}]}]}]},{"ident":15,"label":"P:|-:Q,P","rule":"WR","forest":[{"ident":16,"label":"P:|-:P","rule":"Ax","forest":[{"ident":11,"label":"","rule":"","forest":[]}]}]}]}
    ```

Or like:

    ```{.SequentPlayground .propLK init="now" options="displayJSON"}
    ```

The result, in the first case, will be:

```{.SequentPlayground .propLK init="now" options="displayJSON"}
{"ident":11,"label":"P->Q,P:|-:Q","rule":"->L","forest":[{"ident":12,"label":"Q,P:|-:Q","rule":"Cut","forest":[{"ident":13,"label":"R,P,Q:|-:Q","rule":"XL","forest":[{"ident":58,"label":"Q,P,R:|-:Q","rule":"WL","forest":[{"ident":59,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":14,"label":"","rule":"","forest":[]}]}]}]},{"ident":14,"label":"Q,P:|-:Q,R","rule":"XR","forest":[{"ident":57,"label":"Q,P:|-:R,Q","rule":"WR","forest":[{"ident":10,"label":"Q,P:|-:Q","rule":"WL","forest":[{"ident":12,"label":"Q:|-:Q","rule":"Ax","forest":[{"ident":13,"label":"","rule":"","forest":[]}]}]}]}]}]},{"ident":15,"label":"P:|-:Q,P","rule":"WR","forest":[{"ident":16,"label":"P:|-:P","rule":"Ax","forest":[{"ident":11,"label":"","rule":"","forest":[]}]}]}]}
```

and in the second will be:

```{.SequentPlayground .propLK init="now" options="displayJSON"}
```

Try editing each proof, and see how the displayed sequent changes!
