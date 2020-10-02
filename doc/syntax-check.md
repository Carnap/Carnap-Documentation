# Syntax Check Exercises

Chapter 1 of the Carnap book includes exercises that require identifying the
main connective of a formula and of its sub-formulas in order to break that
formula down into atomic sentences. This helps students learn how sentences are
structured by connectives.

To add a formula-parsing exercise of this kind, use the classes `SynCheck` (to
indicate that you're checking syntax) and `Match` to indicate that you want to
display as many parentheses as possible.

So, following text:

    ~~~{.SynChecker .Match} 
    1.1 P /\ Q /\ R 
    ~~~

will generate:

~~~{.SynChecker .Match} 
1.1 P /\ Q /\ R 
~~~

`1.1` is a problem number that will be used to save the problem when the
student submits it, and `P /\ Q /\ R` is the formula to be parsed. 

In Chapter 2 of the Carnap book, this exercise is repeated, but with some
parentheses omitted by the precedence rules for the Boolean connectives. For a
formula parsing exercise more like the chapter 2 problems, just change `Match`
to `MatchClean`, so that you write:

    ~~~{.SynChecker .MatchClean} 
    1.2 P /\ Q /\ R 
    ~~~

The result will be 

~~~{.SynChecker .MatchClean} 
1.2 P /\ Q /\ R 
~~~

## Syntax Check Options

You can require explicit "parsing of atoms" (pressing return with when an atom
is highlighted to acknowledge that it contains no connectives) by including
adding `parseAtoms` in the options attribute. So for example, 

    ~~~{.SynChecker .MatchClean submission="none" options="parseAtoms"} 
    1.3 P->Q
    ~~~

Generates

~~~{.SynChecker .MatchClean submission="none" options="parseAtoms"} 
1.3 P->Q
~~~
