# Gentzen-Prawitz Natural Deduction

The `TreeDeduction` class indicates that a code block will contain
Gentzen-Prawitz natural deduction exercises, which require the
production of a Gentzen-Prawitz deduction tree.

These problems use [ProofJS](https://github.com/gleachkr/proofjs) for
their user interface. An initial click may be required to select a
node. Once a node is selected, `Enter` will create a sibling premise
(on any node but the root), `Ctrl-Enter` will create a new premise
above the focused node, and `Ctrl-Shift-Enter` will create a new
conclusion node below the focused node (on any node but the root
node). Nodes can be selected by either pressing `Tab` and `Shift-Tab`
to cycle, or by using the mouse. Changes can be undone and redone with
`Ctrl-Z` and `Shift-Ctrl-Z` respectively. The subtree above a selected
node can be deleted with `Ctrl-Backspace`, and subtrees can be
cut-copy-pasted with `Shift-Ctrl-X`, `Shift-Ctrl-C` and `Shift-Ctrl-V`
respectively.

## Available Systems

At the moment, four systems are available:

<div class="table">

System                Description
--------------------- -------------------------------------------------------------------------
propNK                A system based on the propositional fragment of Gentzen's NK
propNJ                A system based on the propositional fragment of Gentzen's NJ
openLogicNK           The propositional fragement of the Open Logic project's natural deduction
openLogicFOLNK        The full (first-order with equality) Open Logic project natural deduction
openLogicArithNK      openLogicFOLNK for the language of arithmetic
openLogicExArithNK    openLogicFOLNK for the language of arithmetic with arbitrary predicates and functions
openLogicSTNK         openLogicFOLNK for the basic language of set theory with arbitrary predicates and functions
openLogicExSTNK       openLogicFOLNK for the basic language of set theory
openLogicESTNK        openLogicFOLNK for an extended language of set theory
openLogicExESTNK      openLogicFOLNK for an extended language of set theory with arbitrary predicates and functions
openLogicSSTNK        openLogicFOLNK for an extended language of set theory with separation abstracts
openLogicExSSTNK      openLogicFOLNK for an extended language of set theory with separation abstracts and arbitrary predicates and functions
--------------------- -------------------------------------------------------------------------

</div>

Exercises are given by specifying the system, and the sequent to be
proved. So an exercise can be constructed like so:

    ```{.TreeDeduction .propNK}
    1.1 P\/Q, ~P :|-: Q 
    ```

which produces:

```{.TreeDeduction .propNK}
1.1 P\/Q, ~P :|-: Q 
```

Instead of `.propNK` etc, you can also use `system="propNK"`.

(Remember to click on a node in order to interact, and to press
`Ctrl-Enter` to create the first child node)

A completed proof will look like this:

```{.TreeDeduction .propNK init="now"}
1.2 :|-: (P->Q)->((R->P)->(R->Q))
| {
|   "label": "(P->Q)->((R->P)->(R->Q))",
|   "rule": "->I(1)",
|   "ident": 0,
|   "forest": [
|     {
|       "label": "(R->P)->(R->Q)",
|       "rule": "->I(2)",
|       "ident": 1,
|       "forest": [
|         {
|           "label": "R->Q",
|           "rule": "->I(3)",
|           "ident": 2,
|           "forest": [
|             {
|               "label": "Q",
|               "rule": "->E",
|               "ident": 3,
|               "forest": [
|                 {
|                   "label": "P->Q",
|                   "rule": "(1)",
|                   "ident": 4,
|                   "forest": [
|                     {
|                       "label": "",
|                       "rule": "",
|                       "ident": 5,
|                       "forest": []
|                     }
|                   ]
|                 },
|                 {
|                   "label": "P",
|                   "rule": "->E",
|                   "ident": 6,
|                   "forest": [
|                     {
|                       "label": "R->P",
|                       "rule": "(2)",
|                       "ident": 7,
|                       "forest": [
|                         {
|                           "label": "",
|                           "rule": "",
|                           "ident": 8,
|                           "forest": []
|                         }
|                       ]
|                     },
|                     {
|                       "label": "R",
|                       "rule": "(3)",
|                       "ident": 9,
|                       "forest": [
|                         {
|                           "label": "",
|                           "rule": "",
|                           "ident": 10,
|                           "forest": []
|                         }
|                       ]
|                     }
|                   ]
|                 }
|               ]
|             }
|           ]
|         }
|       ]
|     }
|   ]
| }
```

With rule names to the right of inference lines, and assumptions
labeled to the right of the rule citation (with or without
parentheses). Discharged assumptions are marked using an inference
with empty premise, and the assumption label on its own to the right
of the inference line.

## Rules for `.propNJ` and `.propNK`

Here's a brief summary of NJ's propositional rules. The notation [ψ]/φ
indicates that an assumption ψ can be discharged from the subproof establishing
φ

<div class="table">

Rule    Premises             Conclusion
-----   ------------------   ---------------------------
`∧I`    φ, ψ                 φ∧ψ
`∧E`    φ∧ψ                  φ OR ψ
`∨I`    φ                    φ∨ψ OR ψ∨φ
`∨E`    φ∨ψ, [φ]/χ, [ψ]/χ    χ
`→I`    [φ]/ψ                φ→ψ
`→E`    φ,φ→ψ                ψ
`¬I`    [φ]/⊥                ¬φ
`¬E`    φ, ¬φ                ⊥
`¬E`    ⊥                    φ
-----   -------------------  ----------------------------

</div>

NK results from the addition of one more rule:

<div class="table">

Rule    Premises             Conclusion
-----   ------------------   ---------------------------
`LEM`                        φ∨¬φ
-----   -------------------  ----------------------------

</div>

The syntax of formulas accepted for is that for the propositional
systems for Kalish & Montague/The Carnap Book in the [Systems
Reference](systems.md#leach-krouse-the-carnap-book).

## Rules for Open Logic Systems

For the systems `.openLogicNK`, etc., the rules are:

<div class="table">

Rule    Premises             Conclusion
-----   ------------------   ---------------------------
`∧I`    φ, ψ                 φ∧ψ
`∧E`    φ ∧ ψ                φ OR ψ
`∨I`    φ                    φ∨ψ OR ψ∨φ
`∨E`    φ∨ψ, [φ]/χ, [ψ]/χ    χ
`→I`    [φ]/ψ                φ→ψ
`→E`    φ,φ→ψ                ψ
`↔I`    [φ]/ψ, [ψ]/φ         φ↔ψ
`↔E`    φ↔ψ, φ               ψ
        φ↔ψ, ψ               φ
`¬I`    [φ]/⊥                ¬φ
`¬E`    φ, ¬φ                ⊥
`X`     ⊥                    φ
`IP`    [¬φ]/⊥               φ
-----   -------------------  ----------------------------

</div>

For the first order systems, we also have the rules:

<div class="table">

Rule    Premises             Conclusion
-----   ------------------   ---------------------------
`∀I`    φ(a)                 ∀x φ(x)
`VE`    ∀x φ(x)              φ(t)
`∃I`    φ(t)                 ∃x φ(x)
`∨E`    ∃x φ(x), [φ(a)]/ψ    ψ
`=I`                         t=t
`=E`    φ(t),t=s             φ(s)
-----   -------------------  ----------------------------

</div>

The syntax of accepted for the Open Logic systems is described in the
[Systems Reference](systems.md#open-logic-project). The natural
deduction systems for arithmetic and set theory only differ in the
syntax; there are no axioms.

Here is an example of a derivation in the language of arithmetic:

```{.TreePlayground .openLogicArithNK init="now" options="displayJSON"}
|{"ident":7,"label":"Ax ~ x < 0","rule":"AI","forest":[{"ident":11,"label":"~ a < 0","rule":"~I 1","forest":[{"ident":11,"label":"_|_","rule":"~E","forest":[{"ident":12,"label":"Ez z' + a = 0","rule":"->E","forest":[{"ident":14,"label":"a < 0","rule":"1","forest":[{"ident":51,"label":"","rule":"","forest":[]}]},{"ident":15,"label":"a < 0 -> Ez z'+a = 0","rule":"->I 2","forest":[{"ident":52,"label":"Ez z'+a = 0","rule":"<->E","forest":[{"ident":52,"label":"a < 0 <-> Ez z'+a = 0","rule":"AE","forest":[{"ident":53,"label":"Ay(a < y <-> Ez z'+a = y)","rule":"AE","forest":[{"ident":54,"label":"AxAy(x < y <-> Ez z'+x = y)","rule":"","forest":[]}]}]},{"ident":62,"label":"a < 0","rule":"2","forest":[{"ident":63,"label":"","rule":"","forest":[]}]}]}]}]},{"ident":13,"label":"~Ez z' + a = 0","rule":"AE","forest":[{"ident":64,"label":"Ax~Ez z' + x = 0","rule":"","forest":[]}]}]}]}]}
```

## Advanced Usage

### Options

In addition to the standard `points=VALUE` and `submission="none"` options,
Gentzen-Prawitz natural deduction exercises allow for you to set `init="now"`
to have proofchecking begin as soon as the proof is loaded (rather than waiting
for input) as well as the following allowed arguments to `options="…"`:

<div class="table">

Option name        Effect
------------------ ------------------------------------------------------------------------------
`prepopulate`      Prepopulates the endformula of an exercises with the conclusion to be shown
`displayJSON`      `Ctrl-?` will toggle display of an editable JSON representation of the proof
------------------ ------------------------------------------------------------------------------

</div>

### JSON Serialization

Here's an incomplete proof, showing how to use the `displayJSON` option:

```{.TreeDeduction .propNK init="now" options="displayJSON"}
1.1 P\/Q, ~P :|-: Q
| {"ident":12,"label":"Q","rule":"\\/E", "forest":[
|   {"ident":13,"label":"P\\/Q","rule":"", "forest":[]},
|   {"ident":14,"label":"Q","rule":"(1)",  "forest":[
|       {"ident":17,"label":"","rule":"","forest":[]}
|   ]},
|   {"ident":15,"label":"Q","rule":"?","forest":[
|       {"ident":18,"label":"?","rule":"","forest":[]}
|   ]}
| ]}
```

To show the JSON representation, click to focus one of the input areas in the
proof and press `Ctrl-?`. To edit the deduction by editing the JSON, try
replacing one of the `Q`s in the JSON panel with a `P`. The deduction will
update to reflect the JSON, so long as the JSON is a well-formed representation
of a deduction.

The above was generated with

    ```{.TreeDeduction .propNK init="now" options="displayJSON"}
    1.1 P\/Q, ~P :|-: Q 
    | {"ident":12,"label":"Q","rule":"\\/E", "forest":[
    |   {"ident":13,"label":"P\\/Q","rule":"", "forest":[]},
    |   {"ident":14,"label":"Q","rule":"(1)",  "forest":[
    |       {"ident":17,"label":"","rule":"","forest":[]}
    |   ]},
    |   {"ident":15,"label":"Q","rule":"?","forest":[
    |       {"ident":18,"label":"?","rule":"","forest":[]}
    |   ]}
    | ]}
    ```

The `displayJSON` option is useful for saving and communicating proofs, since
one can reproduce a proof by pasting its JSON representation into the panel
where the JSON representation is displayed. It's also useful for creating
exercises in which the problems are partially completed, since, as in the
example above, one can prefill an exercise by supplying a JSON representation
below the statement of the problem.

### Playgrounds

One can generate a Gentzen-Prawitz playground (where there is no goal, but
where what you've proved is displayed) using something like the following:

    ```{.TreePlayground .propNK init="now" options="displayJSON"}
    | {"ident":12,"label":"Q","rule":"\\/E (1) (2)","forest":[
    |   {"ident":13,"label":"P\\/Q","rule":"","forest":[]},
    |   {"ident":14,"label":"Q","rule":"(1)","forest":[
    |       {"ident":17,"label":"","rule":"","forest":[]}
    |   ]},
    |   {"ident":15,"label":"Q","rule":"-E","forest":[
    |       {"ident":18,"label":"!?","rule":"-E","forest":[
    |           {"ident":24,"label":"P","rule":"(2)","forest":[
    |               {"ident":27,"label":"","rule":"","forest":[]}
    |           ]},
    |           {"ident":25,"label":"-P","rule":"","forest":[]}
    |       ]}
    |   ]}
    | ]}
    ```

The result, in this case, will be:

```{.TreePlayground .propNK init="now" options="displayJSON"}
| {"ident":12,"label":"Q","rule":"\\/E (1) (2)","forest":[
|   {"ident":13,"label":"P\\/Q","rule":"","forest":[]},
|   {"ident":14,"label":"Q","rule":"(1)","forest":[
|       {"ident":17,"label":"","rule":"","forest":[]}
|   ]},
|   {"ident":15,"label":"Q","rule":"-E","forest":[
|       {"ident":18,"label":"!?","rule":"-E","forest":[
|           {"ident":24,"label":"P","rule":"(2)","forest":[
|               {"ident":27,"label":"","rule":"","forest":[]}
|           ]},
|           {"ident":25,"label":"-P","rule":"","forest":[]}
|       ]}
|   ]}
| ]}
```

Try editing the proof to see how the displayed sequent changes!
