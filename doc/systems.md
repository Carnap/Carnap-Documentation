# Systems Supported

Carnap supports multiple systems in the various types of exercises.
For derivation exercises, a system implies a derivation system (set of
rules, and derivation style). For truth table, translation, and
counter-modeler exercises, the system implies a parser and a formula
renderer, i.e., it implies which formulas are accepted as correct and
how to parse them, and how to render symbols in formulas. 

## Leach-Krouse, *The Carnap Book*
## Kalish/Montague, *Logic*


### Propositional logic

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

### First-order Logic

  + Selected with `system="..."`: `firstOrder`, `montagueQC`
  + Sentence letters: `P` ... `W`
  + Predicate symbols: `F` ...`O`
  + Constant symbols: `a` ... `e`
  + Function symbols: `f` ... `h`
  + Variables: `v`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $F(a,x)$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    `Ax(G(a,f(b),x) -> Ev(H(x,v) /\ P /\ ~(x=v)))`{system="firstOrder"}

produces `Ax(G(a,f(b),x) -> Ev(H(x,v) /\ P /\ ~(x=v)))`{system="firstOrder"}

### Monadic Second-order Logic

  + Selected with `system="..."`: `secondOrder`
  + Second-order variables: `X` ... `Z`

Symbols:

Connective Keyboard 
---------- ----------
λ          `\`
---------- ----------

Example: 

Example:

    `AX(\x[Ey(F(y) /\ X(x))](a))`{system="secondOrder"}

produces `AX(\x[Ey(F(y) /\ X(x))](a))`{system="secondOrder"}


### Polyadic Second-order Logic

  + Selected with `system="..."`: `polyadicSecondOrder`
  + Second-order variables: `Xn` ... `Zn`
  + Arity: given by $n$

Example:

    `AX2(\x[Ay(F(y) -> X2(x,y))](a))`{system="polyadicSecondOrder"}

produces `AX2(\x[Ay(F(y) -> X2(x,y))](a))`{system="polyadicSecondOrder"}


## Bergman, Moore, Nelson, *The Logic Book* 

### Sentential logic

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

### Predicate logic

  + Selected with `system="..."`: `LogicBookPD`
  + Sentence letters: `A` ... `Z`
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `v`
  + Function symbols: no
  + Variables: `w`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $(\forall x)$, $(\exists x)$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
---------- ----------

Example:

    `(Ax)(Gabx -> (Ew)(Hxw /\ P))`{system="LogicBookPD"}

produces `(Ax)(Gabx -> (Ew)(Hx /\ P))`{system="LogicBookPD"}

### Predicate logic with equality

  + Selected with `system="..."`: `LogicBookPDE`
  + Function symbols: `a`...`t`
  + Variables: `w`...`z`

Connective Keyboard 
---------- ----------
=          `=`
---------- ----------

Example:

    `(Ax)(Gabx -> (Ew)(Hxw /\ P /\ ~f(x)=w))`{system="LogicBookPDE"}

produces `(Ax)(Gabx -> (Ew)(Hxw /\ P /\ ~f(x)=w))`{system="LogicBookPDE"}


## Hausman, Kahane, Tidman, *Logic and Philosophy*

### Sentential logic

  + Selected with `system="..."`: `hausmanSL`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `[`, `]`, `(`, `)`, `{`, `}`,  (only in that order)
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

    `[A . B] . [C_1 > (~R_2 \/ {S <> T})]`{system="hausmanSL"}

produces `[A . B] . [C_1 > (~R_2 \/ {S <> T})]`{system="hausmanSL"}.

### Predicate logic

  + Selected with `system="..."`: `hausmanPL` 
  + Sentence letters: `A` ... `Z`
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `t`
  + Function symbols: no
  + Variables: `u`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $(x)$, $(\exists x)$

Quantifiers:

Connective Keyboard 
---------- ----------
∃          `E`
=          `=`
---------- ----------

Example:

    `(x)[Gabx > (Eu)(Hxu . {P \/ ~x=u})]`{system="hausmanPL"}

produces `(x)[Gabx > (Eu)(Hxu . {P \/ ~x=u})]`{system="hausmanPL"}


## Hurley, *Concise Introduction to Logic*

### Sentential logic

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

### Predicate logic

  + Selected with `system="..."`: `hurleyPL` 
  + Sentence letters: `A` ... `Z`
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `w`
  + Function symbols: no
  + Variables: `x`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $(x)$, $(\exists x)$

Quantifiers:

Connective Keyboard 
---------- ----------
∃          `E`
=          `=`
---------- ----------

Example:

    `(x)[Gabx > (Ey)(Hxy . {P \/ ~x=y})]`{system="hurleyPL"}

produces `(x)[Gabx > (Ey)(Hxy . {P \/ ~x=y})]`{system="hurleyPL"}

## Howard-Snyder, *Logic and Philosophy*

### Sentential logic

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

### Predicate logic

  + Selected with `system="..."`: `howardSnyderPL` 
  + Sentence letters: `A` ... `Z`
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `u`
  + Function symbols: no
  + Variables: `v`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $(x)$, $(\exists x)$

Quantifiers:

Connective Keyboard 
---------- ----------
∃          `E`
=          `=`
---------- ----------

Example:

    `(x)[Gabx -> (Ev)(Hxv . (P \/ ~x=v))]`{system="howardSnyderPL"}

produces `(x)[Gabx -> (Ev)(Hxv . (P \/ ~x=v))]`{system="howardSnyderPL"}

## Allen

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

## Magnus, *forall x*

### Sentential logic

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

### Quantificational logic

  + Selected with `system="..."`: `magnusQL`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `w`
  + Function symbols: none
  + Variables: `x`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    `Ax(Gabx -> Ey(Hxy /\ Pa /\ ~x=v))`{system="magnusQL"}

produces `Ax(Gabx -> Ey(Hxy /\ Pa /\ ~x=v))`{system="magnusQL"}

## Thomas-Bolduc/Zach, *forall x: Calgary*

### Fall 2019 and after

#### Truth-functional logic

  + Selected with `system="..."`: `thomasBolducAndZachTFL2019`
  + Sentence letters: `A`...`Z`
  + With subscripts: yes
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: left

Example:

    `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="thomasBolducAndZachTFL2019"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ [_|_ <-> T]))`{system="thomasBolducAndZachTFL2019"}.

#### First-order Logic

  + Selected with `system="..."`: `thomasBolducAndZachFOL2019`, `thomasBolducAndZachFOLPlus2019`
  + Sentence letters: `A` .... `Z`
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `r`
  + Function symbols: `a`...`t`
  + Variables: `s`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $F(a,x)$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    `Ax(G(a,f(b),x) -> Es(H(x,s) /\ P /\ ~x=s))`{system="thomasBolducAndZachFOL2019"}

produces `Ax(G(a,f(b),x) -> Es(H(x,s) /\ P /\ ~x=s))`{system="thomasBolducAndZachFOL2019"}

### pre-Fall 2019, and Ebels-Duggan

#### Truth-functional logic

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

#### First-order logic

  + Selected with `system="..."`: `thomasBolducAndZachFOL`
  + Sentence letters: `A` .... `Z`
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `r`
  + Function symbols: none
  + Variables: `s`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    `Ax(Gabx -> Es(Hxs /\ P /\ ~x=s))`{system="thomasBolducAndZachFOL"}

produces `Ax(Gabx -> Es(Hxs /\ (P \/ ~x=s)))`{system="thomasBolducAndZachFOL"}


## Ichikawa-Jenkins, *forall x: UBC*

### Sentential logic

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


### Quantificational logic

  + Selected with `system="..."`: `ichikawaJenkinsQL`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `w`
  + Function symbols: none
  + Variables: `x`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    `Ax(Gabx -> Ey(Hxy /\ Pa /\ ~x=y))`{system="ichikawaJenkinsQL"}

produces `Ax(Gabx -> Ey(Hxy /\ (Pa /\ ~x=y)))`{system="ichikawaJenkinsQL"}
 
  

## Gamut, *Logic, language, and meaning*

### Propositional logic

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

### Predicate logic

  + Selected with `system="..."`: `gamutND`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `r`
  + Function symbols: none
  + Variables: `s`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    `Ax(Gabx -> Ew(Hxw /\ (_|_ \/ ~x=w)))`{system="gamutND"}

produces `Ax(Gabx -> Ew(Hxw /\ (_|_ \/ ~x=w)))`{system="gamutND"}


## Tomassi, *Logic*

### Propositional logic

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

### Predicate logic

  + Selected with `system="..."`: `tomassiQL`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `t`
  + Function symbols: none
  + Variables: `u`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    `Ax[Gabx -> Ev(Hxv /\ Pr /\ ~(x=v))]`{system="tomassiQL"}

produces `Ax[Gabx -> Ev(Hxv /\ Pr /\ ~(x=v))]`{system="tomassiQL"}

## Hardegree, *Symbolic logic*

### Sentential logic

  + Selected with `system="..."`: `hardegreeSL`
  + Sentence letters: `P` ... `Z`
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

### Predicate logic

  + Selected with `system="..."`: `hardegreePL`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `S`
  + Function symbols: none
  + Variables: `t`...`z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fax$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
---------- ----------

Example:

    ``Ax(G(a,b,x) -> Ev(H(x,e) /\ O(v)))`{system="hardegreePL"}

produces `Ax(G(a,b,x) -> Ev(H(x,e) /\ O(v)))`{system="hardegreePL"}

## Bonevac

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

### Goldfarb, *Deductive Logic*

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

#### Predicate logic

  + Selected with `system="..."`: `goldfarbND`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: none
  + Function symbols: none
  + Variables: `a` ... `z`
  + With subscripts: yes
  + Arity determined: by context
  + Atomic formulas: $Fxy$
  + Quantifiers: $(\forall x)$, $(\exists x)$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
---------- ----------

Example:

    `(Ax)(Gabx -> (Ew)(Hxw /\ P))`{system="goldfarbND"}

produces `Ax(Gax -> Ew(Hxw /\ Pw))`{system="goldfarbND"}

## Open Logic Project

Uses *forall x: Calgary*, 2019+ version.

# Todo:

The available set theory systems are:
`elementarySetTheory` and `separativeSetTheory`. The available second-order
systems are: `secondOrder` and `polyadicSecondOrder`. The available
propositional modal logic systems are: `hardegreeL` `hardegreeK` `hardegreeT`
`hardegreeB` `hardegreeD` `hardegree4` and `hardegree5`. The available
predicate modal logic system is `hardegreeMPL`, and the available "world
theory" system is `hardegreeWTL`.
