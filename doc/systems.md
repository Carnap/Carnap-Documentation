# Systems Supported by Carnap

Carnap supports multiple "systems", i.e., languages with different
symbols and syntax conventions, in the various types of exercises. For
derivation exercises, a system implies a derivation system (set of
rules, and derivation style). For truth table, translation, and
counter-modeler exercises, the system implies a parser and a formula
renderer, i.e., it implies which formulas are accepted as correct, how
to parse them, and how to render formulas when they are displayed by
Carnap.

All sentence letters, predicate symbols, constants, and function
symbols (if allowed) take subscripts (e.g., $P_1$). Predicate and
function symbols also take superscripts (e.g., $P^2$) to indicate
arity. The parser does not enforce the arity, i.e., the arity is
always determined by the number of arguments actually given.

The systems supported are:

- [Allen & Hand, *Logic Primer*](#allen-hand-logic-primer)
- [Bergman, Moore & Nelson, *The Logic
  Book*](#bergman-moore-nelson-the-logic-book)
- [Bonevac, *Deduction*](#bonevac-deduction)
- [Magnus, *forall x*](#magnus-forall-x)
- [Gamut, *Logic, Language, and Meaning*](#gamut-logic-language-and-meaning)
- [Goldfarb, *Deductive Logic*](#goldfarb-deductive-logic)
- [Hardegree, *Symbolic Logic* and *Modal Logic*](#hardegree-symbolic-logic)
- [Hausman, Kahane & Tidman, *Logic and
  Philosophy*](#hausman-kahane-tidman-logic-and-philosophy)
- [Howard-Snyder, Howard-Snyder & Wasserman, *The Power of Logic*](#howard-snyder-howard-snyder-wasserman-the-power-of-logic)
- [Hurley, *Concise Introduction to Logic*](#hurley-concise-introduction-to-logic)
- [Ichikawa-Jenkins, *forall x: UBC*](#ichikawa-jenkins-forall-x-ubc)
- [Leach-Krouse, *The Carnap Book*](#leach-krouse-the-carnap-book)
- [Kalish & Montague, *Logic*](#kalish-montague-logic)
- [Open Logic Project](#open-logic-project)
- [Thomas-Bolduc & Zach, *forall x: Calgary*](#thomas-bolduc-zach-forall-x-calgary)
- [Tomassi, *Logic*](#tomassi-logic)


## Allen & Hand, *Logic Primer*

### Sentential logic

  + Selected with `system="..."`: `allenSL`
  + Sentence letters: `A`...`Z`
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: yes
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

    `A & B & (C_1 -> (~R_2 \/ [S <-> T]))`{system="allenSL"}

produces `A & B & (C_1 -> (~R_2 \/ [S <-> T]))`{system="allenSL"}.

### Predicate logic

Not yet supported.

## Bergman, Moore & Nelson, *The Logic Book* 

### Sentential logic

  + Selected with `system="..."`: `LogicBookSD` `LogicBookSDPlus`
  + Sentence letters:`A`...`Z`
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


## Bonevac, *Deduction*

### Sentential logic

  + Selected with `system="..."`: `bonevacSL`
  + Sentence letters: `a`...`z`
  + Brackets allowed `(`, `)`
  + Associative $\land$, $\lor$: no
  + Connectives: 

Connective Keyboard 
---------- ----------
→          `->`, `=>`, `>`
&          `/\`, `&`, `and`
∨          `\/`, `|`, `or`
↔          `<->`, `<=>`
¬          `-`, `~`, `not`
---------- ----------

Example:

    `(a & b) & (c_1 -> (~r_2 \/ (s <-> t)))`{system="bonevacSL"}

produces `(a /\ b) /\ (c_1 -> (~r_2 \/ (s <-> t)))`{system="bonevacSL"}.

### Quantificational logic

  + Selected with `system="..."`: `bonevacQL`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `w`
  + Function symbols: none
  + Variables: `x`...`z`
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

    `Ax(Gabx -> Ey(Hxy & Pa & ~x=v))`{system="bonevacQL"}

produces `Ax(Gabx -> Ey(Hxy & Pa & ~x=v))`{system="bonevacQL"}

## Magnus, *forall x*

### Sentential logic

  + Selected with `system="..."`: `magnusSL` `magnusSLPlus`
  + Sentence letters: `A`...`Z`
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

    `A & B & (C_1 -> (~R_2 \/ [S <-> T]))`{system="magnusSL"}

produces `A & B & (C_1 -> (~R_2 \/ [S <-> T]))`{system="magnusSL"}.

### Quantificational logic

  + Selected with `system="..."`: `magnusQL`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `w`
  + Function symbols: none
  + Variables: `x`...`z`
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

    `Ax(Gabx -> Ey(Hxy & Pa & ~x=v))`{system="magnusQL"}

produces `Ax(Gabx -> Ey(Hxy & Pa & ~x=v))`{system="magnusQL"}


## Gamut, *Logic, Language, and Meaning*

### Propositional logic

  + Selected with `system="..."`: `gamutIPND` `gamutPND` `gamutPNDPlus`
  + Sentence letters: `a`...`z`
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

## Goldfarb, *Deductive Logic*

### Propositional logic

  + Selected with `system="..."`: `goldfarbPropND`
  + Sentence letters: `a`...`z`
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

### Predicate logic

  + Selected with `system="..."`: `goldfarbND`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: none
  + Function symbols: none
  + Variables: `a` ... `z`
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


## Hardegree, *Symbolic Logic*

### Sentential logic

  + Selected with `system="..."`: `hardegreeSL`
  + Sentence letters: `A` ... `Z`
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

    `A & G & (R_1 -> (~R_2 \/ (_|_ <-> T)))`{system="hardegreeSL"}

produces `A & G & (R_1 -> (~R_2 \/ (_|_ <-> T)))`{system="hardegreeSL"}.

### Predicate logic

  + Selected with `system="..."`: `hardegreePL`
  + Sentence letters: none
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `s`
  + Function symbols: none
  + Variables: `t`...`z`
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

    `Ax(Gabx -> Ev(Hxe & Ov & _|_))`{system="hardegreePL"}

produces `Ax(Gabx -> Ev(Hxe & Ov & _|_))`{system="hardegreePL"}


## Hausman, Kahane & Tidman, *Logic and Philosophy*

### Sentential logic

  + Selected with `system="..."`: `hausmanSL`
  + Sentence letters: `A`...`Z`
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


## Howard-Snyder, Howard-Snyder & Wasserman, *The Power of Logic*

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

## Ichikawa-Jenkins, *forall x: UBC*

### Sentential logic

  + Selected with `system="..."`: `ichikawaJenkinsSL`
  + Sentence letters: `A`...`Z`
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


## Leach-Krouse, *The Carnap Book*
## Kalish & Montague, *Logic*

### Propositional logic

  + Selected with `system="..."`: `prop`, `montagueSC`
  + Sentence letters: `P` ... `W`
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

### First-order logic

  + Selected with `system="..."`: `firstOrder`, `montagueQC`
  + Sentence letters: `P` ... `W`
  + Predicate symbols: `F` ...`O`
  + Constant symbols: `a` ... `e`
  + Function symbols: `f` ... `h`
  + Variables: `v`...`z`
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

### Monadic second-order logic

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


### Polyadic second-order logic

  + Selected with `system="..."`: `polyadicSecondOrder`
  + Second-order variables: `Xn` ... `Zn`
  + Arity: given by $n$

Example:

    `AX2(\x[Ay(F(y) -> X2(x,y))](a))`{system="polyadicSecondOrder"}

produces `AX2(\x[Ay(F(y) -> X2(x,y))](a))`{system="polyadicSecondOrder"}

## Open Logic Project

Uses *forall x: Calgary*, 2019+ version.

## Thomas-Bolduc & Zach, *forall x: Calgary*

### Fall 2019 and after

The `2019` systems refer to the syntax used in *forall x: Carnap*,
Fall 2019 and after.  The TFL system allows leaving out extra
parentheses in conjunctions and disjunctions of more than 2 sentences.
The pre-2019 systems do not, so can be used if stricter parenthesis
rules are desired.  

The major change is in the syntax of the FOL systems, which wrap
arguments in parentheses. This allows support of function symbols and
terms. The `FOL2019` system also allows entering negated identities as
`x != y`. This is not done in *forall x: Calgary*, but is the
convention in the Open Logic Project.

#### Truth-functional logic

  + Selected with `system="..."`: `thomasBolducAndZachTFL2019`
  + Sentence letters: `A`...`Z`
  + Brackets allowed `(`, `)`, `[`, `]`
  + Associative $\land$, $\lor$: left

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

    `A /\ B /\ (C_1 -> (~R_2 \/ [S <-> T]))`{system="thomasBolducAndZachTFL2019"}

produces `A /\ B /\ (C_1 -> (~R_2 \/ [_|_ <-> T]))`{system="thomasBolducAndZachTFL2019"}.

#### First-order logic

  + Selected with `system="..."`: `thomasBolducAndZachFOL2019`, `thomasBolducAndZachFOLPlus2019`
  + Sentence letters: `A` .... `Z`
  + Predicate symbols: `A` ...`Z`
  + Constant symbols: `a` ... `r`
  + Function symbols: `a`...`t`
  + Variables: `s`...`z`
  + Atomic formulas: $F(a,x)$
  + Quantifiers: $\forall x$, $\exists x$

Quantifiers:

Connective Keyboard 
---------- ----------
∀          `A`
∃          `E`
=          `=`
≠          `!=`
---------- ----------

Example:

    `Ax(G(a,f(b),x) -> Es(H(x,s) /\ P /\ x!=s))`{system="thomasBolducAndZachFOL2019"}

produces `Ax(G(a,f(b),x) -> Es(H(x,s) /\ P /\ x!=s))`{system="thomasBolducAndZachFOL2019"}

### pre-Fall 2019

These syntax conventions were in force before the Fall 2019 edition of
*forall x: Calgary*. They are still useful: (a) They coincide with the
syntax conventions of Tim Button's *forall x: Cambridge* and the text
by Sean Ebbels-Duggan. (b) The TFL system requires all parentheses be
included and displays with all parentheses. So it can be used in
exercises that require TFL sentences be entered or displayed *without*
bracketing conventions.

#### Truth-functional logic

  + Selected with `system="..."`: `thomasBolducAndZachTFL`, `ebelsDugganTFL`
  + Sentence letters: `A`...`Z`
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

## Tomassi, *Logic*

### Propositional logic

  + Selected with `system="..."`: `tomassiPL`
  + Sentence letters: `P` ... `W`
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


# Todo:

The available set theory systems are: `elementarySetTheory` and
`separativeSetTheory`. The available propositional modal logic systems
are: `hardegreeL` `hardegreeK` `hardegreeT` `hardegreeB` `hardegreeD`
`hardegree4` and `hardegree5`. The available predicate modal logic
system is `hardegreeMPL`, and the available "world theory" system is
`hardegreeWTL`.
