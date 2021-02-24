# Countermodels

The `CounterModeler` class indicates that a code block will contain
countermodel construction exercises.

## Simple Countermodels

You can create simple countermodel problems, checking to see if one or more
formulas are true in a constructed model like this:

    ```{.CounterModeler .Simple}
    1.1 AxF(x), ExG(x)
    ```

The result will be:

```{.CounterModeler .Simple}
1.1 AxF(x), ExG(x)
```

Here is an example with some more interesting vocabulary:

    ```{.CounterModeler .Simple}
    1.2 AxAy(f(x,y) = f(y,x))
    ```

Producing:

```{.CounterModeler .Simple}
1.2 AxAy(f(x,y) = f(y,x))
```

The domain of the model must consist of one or more natural numbers. The tuples
making up the extensions of predicate and relation symbols are comma-separated
and enclosed in brackets, parentheses, or `<>` pairs, like this: `[0,0]` or
this `<1,1>`. The tuples themselves should be separated by commas, like this:
`[0,0],[1,0]`.

The extension of each constant must be a natural number. The extension of a
given function symbol will be a comma-separated list of tuples as above but
with the arguments separated from the value by a semicolon, thus: `[0,0;1]`.

Formulas containing free variables are treated as equivalent to their universal
closures.

## Validity Countermodels

You can create a countermodel problem for showing invalidity like this:

    ```{.CounterModeler .Validity}
    1.3 AxEyF(x,y) :|-: ExAyF(y,x)
    ```

Creating:

```{.CounterModeler .Validity}
1.3 AxEyF(x,y) :|-: ExAyF(y,x)
```

Validity countermodel problems can include comma-separated lists of formulas to
both the left and *right* of the turnstile. A countermodel is successful if it
makes all the formulas to the left of the turnstile true and all the formulas
to the right of the turnstile false.

## Constraint Countermodels

You can create a countermodel with some implicit constraints on the allowable models like this:

    ```{.CounterModeler .Constraint }
    1.4 ExEy(not x = y) : AxAyF(x,y)
    ```

Resulting in:

```{.CounterModeler .Constraint}
1.4 ExEy(not x = y) : AxAyF(x,y)
```

A countermodel with implicit constraints is successful if it makes all the
formulas to the right and the left of the `:` true.

## Advanced Usage

#### Options

In addition to setting a custom point value or turning off submission by adding
`points=VALUE` and `submission="none"`, several other options are available for
countermodels:

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------
`nocheck`                Disables the "check" button
`exam`                   Allows for submission of work which is incomplete or incorrect
`strictGivens`           Makes givens immutable (see below)
------------------------ ------------------------------------------------------------------


#### Counterexamples

There are also a number of options that affect what counts as a successful
countermodel. these are set using the `counterexample-to` attribute. The
options are:

<div class="table">

Name                     Counterexample is
------------------------ ------------------------------------------------------------------
`validity`               a situation in which all formulas are false
`tautology`              Same as `validity`
`equivalence`            a situation in which two formulas have different truth values
`inconsistency`          a situation in which all formulas are true
------------------------ ------------------------------------------------------------------

</div>

In the case of simple countermodels, these apply to all formulas. In the case
of validity countermodels, a successful countermodel is a situation in which
the formulas to the left of the turnstile are all true, and the ones to the
right of the turnstile have the counterexample property. Similarly in the case
of a constraint countermodel problem---all the constraints must be true, and
the other formulas must have the counterexample property.

#### Systems

The way that formulas are parsed and displayed can also be customized. This is
done by setting the `system` attribute to indicate which formal system you are
drawing your syntax from. So for example, 

    ~~~{.CounterModeler .Simple  system="LogicBookPD"}
    1.5 Ax->Bx
    ~~~

will generate:

~~~{.CounterModeler .Simple options="exam" system="LogicBookPD"}
1.5 Ax->Bx
~~~

The available systems are `firstOrder` `montagueQC` `magnusQL`
`thomasBolducAndZachFOL` `thomasBolducAndZachFOL2019`
`thomasBolducAndZachFOLPlus` `LogicBookPD` `LogicBookPDPlus` `hausmanPL`
`howardSnyderPL` `ichikawaJenkinsQL` `hardegreePL` `goldfarbAltND`
`goldfarbNDPlus` and `goldfarbAltNDPlus`.

#### Givens

It is also possible to give a "partial solution" to a countermodeling problem,
in which the model is partly filled in, and the student needs either to
complete it or correct it. To pre-populate models with "givens" in this way,
write each field you want filled in, preceded by the bar character `|` and
followed by a colon and what you want it filled in with, like this:


    ```{.CounterModeler .Simple}
    1.1 AxF(x), ExG(x)
    | Domain : 0,1,2
    | a : 1
    ```

Which will produce:

```{.CounterModeler .Simple}
1.1 AxF(x), ExG(x), H(a)
| Domain : 0,1,2
| a : 1
```

The field-names for the givens should match how the field-names would be
displayed in the exercise.

Ordinarily, givens function as hints. However, you can make it impossible for
students to change them (thereby turning them into requirements) by adding the
`strictGivens` option to your problem.
