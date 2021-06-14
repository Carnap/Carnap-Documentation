# Truth Tables

The `TruthTable` class indicates that a code block will contain truth table
exercises.

## Simple Truth Tables

You can create simple truth table problems, checking to see if a formula is a
tautology, by also adding the class `Simple`, like so:

    ~~~{.TruthTable .Simple}
    2.1 ((P/\Q)\/R)<->((P\/R)/\(Q\/R))
    ~~~

the number 2.1 indicates the exercise number, and the formula is the one for
which you will be constructing a truth table. This produces:

~~~{.TruthTable .Simple}
2.1 ((P/\Q)\/R)<->((P\/R)/\(Q\/R))
~~~

You can also use a comma-separated list of formulas, like so:

    ~~~{.TruthTable .Simple}
    2.2 (P/\Q)\/R, (P\/R)/\(Q\/R)
    ~~~

This example produces:

~~~{.TruthTable .Simple}
2.2 (P/\Q)\/R, (P\/R)/\(Q\/R)
~~~

Simple truth tables can be (by default) checked for correctness, and will be
considered correct when every row is filled in correctly. A problem can also be
solved by indicating a counterexample to tautology. A row is considered a
counterexample if *all* the formulas in the problem are false on that row.

## Validity Truth Tables

If, instead of `Simple`, you add the class `Validity`, like so:

    ~~~{.TruthTable .Validity}
    2.3 P :|-: ((P/\Q)\/R)<->((P\/R)/\(Q\/R))
    ~~~

the result is a truth-table for checking the validity of an argument (in this
case, `P :|-: ((P/\Q)\/R)<->((P\/R)/\(Q\/R))`, where `:|-:` is just a stylized
way of typing out the turnstile). The above produces:

~~~{.TruthTable .Validity}
2.3 P :|-: ((P/\Q)\/R)<->((P\/R)/\(Q\/R))
~~~

Validity truth-table problems can include comma-separated lists of formulas to
both the left and *right* of the turnstile. For example, 

~~~{.TruthTable .Validity}
2.4 P,Q :|-: (P/\Q), (P\/R)/\(Q\/R)
~~~

produces:

    ~~~{.TruthTable .Validity}
    2.4 P,Q :|-: (P/\Q), (P\/R)/\(Q\/R)
    ~~~

Validity truth tables can be (by default) checked for correctness. A table is
correct when every row has been filled in, with rows that are counterexamples
to validity marked `F`, and rows that are not counterexamples to validity
marked `T`. A counterexample to validity can also be provided directly by
pressing the counterexample button and entering the truth values of the
relevant row. A row is considered a counterexample to validity only if all the
formulas to the left of the sequent are true, and *all* the formulas to the
right of the sequent are false.[^1]

[^1]: There's some arbitrariness in how we choose to think about the validity
of multi-conclusion arguments. This approach is the most natural from the point
of view of the sequent calculus.

## Partial Truth Tables

You can also create truth table problems that involve filling in a single row.
To do this, add the class `Partial`, like so:

    ~~~{.TruthTable .Partial}
    2.5 (P/\Q), (P\/R)/\(Q\/R)
    ~~~

creating something like this:

~~~{.TruthTable .Partial}
2.5 (P/\Q), (P\/R)/\(Q\/R)
~~~

By default, the row is considered correct if it is filled in correctly, with
any assignment of truth values to the atoms. However by using givens (see
below), partial truth tables can be used to ask students to test for variety of
different properties.

## Advanced Usage

#### Options

In addition to setting a custom point value or turning off submission by adding
`points=VALUE` and `submission="none"`, several
other options are available for truth tables:

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------
`nocheck`                Disables the "check" button
`nocounterexample`       Disables the "counterexample" button
`exam`                   Allows for submission of work which is incomplete or incorrect
`autoAtoms`              Prepopulates atomic sentence columns with truth values
`turnstilemark`          Uses `✓` and `✗` rather than `T` and `F` under the turnstile
`immutable`              Makes the truth table immutable (useful for displaying truth tables)
`nodash`                 Uses ` ` rather than `-` in empty cells (useful for printing worksheets)
`strictGivens`           Makes givens (see below) immutable
`hiddenGivens`           Hides givens (see below)
------------------------ ------------------------------------------------------------------

</div>

So for example, 

    ~~~{.TruthTable .Validity options="nocheck nocounterexample"}
    2.6 P :|-: Q
    ~~~

Generates:

~~~{.TruthTable .Validity options="nocheck nocounterexample"}
2.6 P :|-: Q
~~~

#### Counterexamples

There are also a number of options that affect what counts as a counterexample.
these are set using the `counterexample-to` attribute. The options are:

<div class="table">

Name                     Counterexample is
------------------------ ------------------------------------------------------------------
`validity`               a situation in which all formulas are false
`tautology`              same as `validity`
`equivalence`            a situation in which two formulas have different truth values
`inconsistency`          a situation in which all formulas are true
`contradiction`          same as `inconsistency`
------------------------ ------------------------------------------------------------------

</div>

In the case of simple truth tables, these apply to all formulas. In the case of
validity truth tables, a counterexample is a situation in which the formulas to
the left of the turnstile are all true, and the ones to the right of the
turnstile have the counterexample property. Hence, a validity problem in which
the counterexample is `equivalence` is basically using a truth table to test
whether the formulas to the right of the turnstile are equivalent "under the
assumption" that the formulas to the left of the turnstile are true.

Here's an example of a truth table looking for a counterexample to the
equivalence of two formulas

```{.TruthTable .Simple counterexample-to:"equivalence"}
2.7 P<->Q,  P->Q
```

#### Systems

The way that formulas are parsed and displayed can also be customized. This is
done by setting the `system` attribute to indicate which formal system you are
drawing your syntax from. So for example, 

    ~~~{.TruthTable .Simple system="LogicBookSD"}
    2.8 A > B & C
    ~~~

will generate:

~~~{.TruthTable .Simple system="LogicBookSD"}
2.8 A > B & C
~~~

The available systems are: `prop` `montagueSC` `LogicBookSD` `LogicBookSDPlus`
`hausmanSL` `howardSnyderSL` `ichikawaJenkinsSL` `hausmanSL` `magnusSL`
`magnusSLPlus` `thomasBolducAndZachTFL` `thomasBolducAndZachTFL2019`
`tomassiPL` and `hardegreeSL`.

#### Givens

It is also possible to give a "partial solution" to a truth table problem, in
which the truth table is partly filled in, and the student needs either to
complete it or correct it. To pre-populate simple and validity tables with
"givens" in this way, write the truth table you want, preceded by the bar
character `|`, after the problem. So, 

    ~~~{.TruthTable .Simple}
    2.9 P \/~P
    |   T - FT
    |   F - TF
    ~~~

Generates

~~~{.TruthTable .Simple}
2.9 P \/~P
|   T - FT
|   F - TF
~~~

You do need to fill in every row entirely. If a row is the wrong length, or if
there are the wrong number of rows, the table will not be pre-populated. If you
wish to make the givens you assign immutable (to clarify that they are a hint,
rather than something that needs to be corrected), you can use the
`strictGivens` option. 

Givens behave similarly for partial truth tables. For example, 

    ~~~{.TruthTable .Partial}
    2.10 P \/~P
    |   F - TF
    ~~~

will produce:

~~~{.TruthTable .Partial}
2.10 P \/~P
|   F - TF
~~~

However: if a partial truth table is constructed with givens, then a solution
will only be accepted if it is "consistent" with the givens. So in the above
case, the only acceptable solution will be one that assigns `T` to `P`. The
givens can be hidden, using `hiddenGivens` if you want to, for example, ask
students to make a sentence truth and you want them to figure out the relation
between the truth of a sentence and the truth value of the main connective.

if you wish to hide some givens, but not others, you can use a colon to
separate the sentences that will have visible truth values from those that will
not. For example, you can write

    ~~~{.TruthTable .Partial options="hiddenGivens"}
    2.11 Q : Q->P
    |    T   TT -
    ~~~

to create a problem in which the student must make `Q->P` true under the
assumption that `Q` is true. The result is like this:

~~~{.TruthTable .Partial options="hiddenGivens"}
2.11 Q : Q->P
|    T   TT -
~~~

so this can also be used to create problems in which students are responsible
for filling in a certain row of the truth table.

Finally, if more than one row of givens is provided to a partial truth table,
then any solution which is compatible with *any one* of the rows will be
accepted. So for example, you can write:

    ~~~{.TruthTable .Partial options="hiddenGivens"}
    2.12 P/\Q, P\/Q
    |    -T -  -F - 
    |    -F -  -T - 
    ~~~

In order to ask students to provide a row that witnesses the inequivalence of
these two sentences. The result will be:

~~~{.TruthTable .Partial options="hiddenGivens"}
2.12 P/\Q, P\/Q
|    -T -  -F - 
|    -F -  -T - 
~~~

#### Custom Marks

The marks for truth and falsity can be configured to something other than the
usual `T` and `F` by setting the `falseMark` and `trueMark` attributes. So for
example 

    ```{.TruthTable .Validity trueMark="1" falseMark="0"}
    2.13 P,Q:|-:P/\Q
    ```

will produce

```{.TruthTable .Validity trueMark="1" falseMark="0"}
2.13 P,Q:|-:P/\Q
```

The handling of givens remains the same in the presence of a configured
`falseMark` or `trueMark` attribute. So,for example

    ```{.TruthTable .Validity trueMark="1" falseMark="0"}
    2.14 P,Q:|-:P/\Q
    | TT----
    | FT----
    | TF----
    | FF----
    ```

will produce

```{.TruthTable .Validity trueMark="1" falseMark="0"}
2.14 P,Q:|-:P/\Q
| TT----
| FT----
| TF----
| FF----
```
