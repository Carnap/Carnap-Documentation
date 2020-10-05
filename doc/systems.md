# Systems Supported

Carnap supports multiple systems in the various types of exercises.
For derivation exercises, a system implies a derivation system (set of
rules, and derivation style). For truth table, translation, and
counter-modeler exercises, the system implies a parser and a formula
renderer, i.e., it implies which formulas are accepted as correct and
how to parse them, and how to render symbols in formulas. 

### Leach-Krouse, *The Carnap Book*

#### Propositional logic

  + Selected with `system="..."`: `prop`, `montagueSC`
  + Sentence letters: `P` ... `W`
  + With subscripts: yes
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: left
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
∧          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

Example:

    `P /\ Q /\ (R_1 -> (~R_2 \/ (S <-> T)))`{system="prop"}

produces `P /\ Q /\ (R_1 -> (~R_2 \/ (S <-> T)))`{system="prop"}.

#### First-order Logic
`firstOrder` 

### Kalish/Montague, *Logic*

`montagueSC`

Example:

    `P /\ Q /\ (R_1 -> (~R_2 \/ (S <-> T)))`{system="montagueSC"}

produces `P /\ Q /\ (R_1 -> (~R_2 \/ (S <-> T)))`{system="montagueSC"}.

 `montagueQC` 

### Bergman, Moore, Nelson, *The Logic Book* 

  + Selected with `system="..."`: `LogicBookSD` `LogicBookSDPlus`
  + Sentence letters:`A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: left
  + Connectives: 

Connective Keyboard 
---------- ----------
⊃          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
~          `-`, `~`, `not`
---------- ----------

Example:

    `A /\ B /\ (C_1 -> (~R_2 \/ (S <-> T)))`{system="LogicBookSD"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ (S <-> T)))`{system="LogicBookSD"}.

`LogicBookPD` `LogicBookPDPlus`


### Hausman, *Logic and Philosophy*

  + Selected with `system="..."`: `hausmanSL`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`, `{`, `}`, `[`, `]` (only in that order)
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
⊃          `⊃`, `→`,`>`
∙          `.`, `∧`, `∙`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`, `<>`
~          `-`, `~`, `not`
---------- ----------

Example:

    `(A . B) . (C_1 > {~R_2 \/ [S <> T]})`{system="hausmanSL"}

produces `(A . B) . (C_1 > {~R_2 \/ [S <> T]})`{system="hausmanSL"}.

`hausmanPL` 

### Hurley, *Concise Introduction to Logic*

  + Selected with `system="..."`: `hurleySL`
  + Sentence letters: `A`...`Z`
  + With subscripts: ?
  + Brackets allowed `(`, `)`, `[`, `]`, `{`, `}`
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
⊃          `⊃`, `→`,`>`
∙          `.`, `∧`, `∙`
∨          `\/`, `|`, `or`
≡          `<->`, `<=>`, `<>`
~          `-`, `~`, `not`
---------- ----------

Example:

    `(A . B) . [C_1 > (~R_2 \/ {S <-> T})]`{system="hurleySL"}

produces `(A . B) . [C_1 > (~R_2 \/ {S <-> T})]`{system="hurleySL"}.

`hurleyPL`? 


### Howard-Snyder, *Logic and Philosophy*

  + Selected with `system="..."`: `howardSnyderSL`
  + Sentence letters: `A`...`Z`
  + With subscripts: ?
  + Brackets allowed `(`, `)`, `[`, `]`, `{`, `}`
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
∙          `.`, `∧`, `∙`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`, `<>`
~          `-`, `~`, `not`
---------- ----------

Example:

    `(A . B) . [C_1 -> (~R_2 \/ {S <-> T})]`{system="howardSnyderSL"}

produces `(A . B) . [C_1 -> (~R_2 \/ {S <-> T})]`{system="howardSnyderSL"}.

`howardSnyderPL`


### Allen

  + Selected with `system="..."`: `allenSL`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: yes
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

Example:

    `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="allenSL"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="allenSL"}.

`magnusQL`

### Magnus, *forall x*

  + Selected with `system="..."`: `magnusSL` `magnusSLPlus`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: yes
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

Example:

    `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="magnusSL"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="magnusSL"}.

`magnusQL`

### Thomas-Bolduc/Zach, *forall x: Calgary*, and variants

#### pre-Fall 2019, and Ebels-Duggan

  + Selected with `system="..."`: `thomasBolducAndZachTFL`, `ebelsDugganTFL`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`, `>`
∧          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
⊥          `!?`, `_|_`
---------- ----------

Example:

    `(A /\ B) /\ (C_1 -> (~R_2 \/ [_|_ <-> T]))`{system="thomasBolducAndZachTFL"}

produces `(A /\ B) /\ (C_1 -> (~R_2 \/ [_|_ <->
T]))`{system="thomasBolducAndZachTFL"}.

Example:

    `(A /\ B) /\ (C_1 -> (~R_2 \/ [_|_ <-> T]))`{system="ebelsDugganTFL"}

produces `(A /\ B) /\ (C_1 -> (~R_2 \/ [_|_ <-> T]))`{system="ebelsDugganTFL"}.


#### Fall 2019 and after, and Gallow, *forall x: Pittsburgh*

  + Selected with `system="..."`: `thomasBolducAndZachTFL2019`, `GallowSL`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: left

Example:

    `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="thomasBolducAndZachTFL2019"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ [_|_ <-> T]))`{system="thomasBolducAndZachTFL2019"}.

    `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="gallowSL"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ [_|_ <-> T]))`{system="gallowSL"}.


`thomasBolducAndZachFOL` `thomasBolducAndZachFOL2019`
`thomasBolducAndZachFOLPlus2019` 

### Ichikawa-Jenkins, *forall x: UBC*

  + Selected with `system="..."`: `ichikawaJenkinsSL`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: yes
  + Connectives: 

Connective Keyboard 
---------- ----------
⊃          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
≡          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

Example:

    `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="ichikawaJenkinsSL"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="ichikawaJenkinsSL"}.

 
 `ichikawaJenkinsQL` 

### Gamut

  + Selected with `system="..."`: `gamutIPND` `gamutPND` `gamutPNDPlus`
  + Sentence letters: `a`...`z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`, `>`
∧          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
⊥          `!?`, `_|_`
---------- ----------

Example:

    `(a /\ b) /\ (c_1 -> (~r_2 \/ (_|_ <-> t)))`{system="gamutIPND"}

produces `(a /\ b) /\ (c_1 -> (~r_2 \/ (_|_ <-> t)))`{system="gamutIPND"}.

`gamutND`

### Tomassi

  + Selected with `system="..."`: `tomassiPL`
  + Sentence letters: `P` ... `W`
  + With subscripts: yes
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: left
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
~          `-`, `~`, `not`
---------- ----------


Example:

    `P /\ Q /\ (R_1 -> (~R_2 \/ (S <-> T)))`{system="tomassiPL"}

produces `P /\ Q /\ (R_1 -> (~R_2 \/ (S <-> T)))`{system="tomassiPL"}.

### Hardegree

  + Selected with `system="..."`: `hardegreeSL`
  + Sentence letters: `P` ... `W`
  + With subscripts: yes
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: left
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`,`>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
~          `-`, `~`, `not`
⨳          `!?`, `_|_`
---------- ----------
Example:

    `P /\ Q /\ (R_1 -> (~R_2 \/ (_|_ <-> T)))`{system="hardegreeSL"}

produces `P /\ Q /\ (R_1 -> (~R_2 \/ (_|_ <-> T)))`{system="hardegreeSL"}.

`hardegreePL`

### Bonevac

  + Selected with `system="..."`: `bonevacSL`
  + Sentence letters: `a`...`z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`, `>`
∧          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

Example:

    `(a /\ b) /\ (c_1 -> (~r_2 \/ (s <-> t)))`{system="bonevacSL"}

produces `(a /\ b) /\ (c_1 -> (~r_2 \/ (s <-> t)))`{system="bonevacSL"}.

`gamutND`

### Goldfarb

  + Selected with `system="..."`: `goldfarbPropND`
  + Sentence letters: `a`...`z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`, `>`
∧          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
⊥          `!?`, `_|_`
---------- ----------

Example:

    `(a /\ b) /\ (c_1 -> (~r_2 \/ (_|_ <-> t)))`{system="goldfarbPropND"}

produces `(a /\ b) /\ (c_1 -> (~r_2 \/ (_|_ <-> t)))`{system="goldfarbPropND"}.

## Open Logic Project

Uses *forall x: Calgary*, 2019+ version.

# Todo:

The available set theory systems are:
`elementarySetTheory` and `separativeSetTheory`. The available second-order
systems are: `secondOrder` and `PolySecondOrder`. The available propositional
modal logic systems are: `hardegreeL` `hardegreeK` `hardegreeT` `hardegreeB`
`hardegreeD` `hardegree4` and `hardegree5`. The available predicate modal logic
system is `hardegreeMPL`, and the available "world theory" system is
`hardegreeWTL`.
