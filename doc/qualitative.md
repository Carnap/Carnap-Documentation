# Qualitative Problems

the `QualitativeProblem` class indicates that a code block will contain
qualitative problems, either short-answer or multiple choice questions.

## Short Answer

To create a short-answer problem, use the class `ShortAnswer`, and simply
provide a short answer question, like so:

    ```{.QualitativeProblem .ShortAnswer}
    1.1 How are you feeling today?
    ```

The number indicates the exercise number. This is immediately followed by the
question. The result will be:

```{.QualitativeProblem .ShortAnswer}
1.1 How are you feeling today?
```

Student submissions to short-answer prompts will be recorded, but by default
will not be assigned any credit. They will, however, be visible in the review
section for the assignment, so it will be possible to assign them partial
credit, as if they were an exam problem. The behavior for awarding credit can
also be configured with the `give-credit` option, see Advanced Usage below.

## Multiple Choice

To create a multiple-choice problem, use the class `MultipleChoice`, and
provide a question along with a set of answers (one per line), like so:

    ```{.QualitativeProblem .MultipleChoice}
    1.2 How are you feeling today?
    | Good!
    | +OK!
    | Meh.
    ```

The answers should be typed as you want them to be displayed. Carnap doesn't
currently render formulas or LaTeX within multiple choice answers, and HTML
escape codes like `&or;` will cause some trouble for the answer-parser. If you
want to include a formula with symbols, just use the symbols directly in the
answer. You can copy-paste from here: ¬,→,∧,∨,∀,∃.

Answers marked with a `+` or a `*` will be accepted as correct. Answers marked
with a `-` or a `+` will be pre-selected. So the result of the above is:

```{.QualitativeProblem .MultipleChoice}
1.2 How are you feeling today?
| Good!
| +OK!
| Meh.
```

Which has "OK!" preselected and just one correct answer, namely "OK!".

## Multiple Selection

To create a multiple-selection problem, use the class `MultipleSelection`, 

To create a multiple-choice problem, use the class `MultipleChoice`, and
provide a question along with a set of answers (one per line), like so:

    ```{.QualitativeProblem .MultipleSelection}
    1.2 How are you feeling today?
    | - Bad!
    | + OK!
    | * I contain multitudes.
    ```

As above, answers should be typed as you want them displayed.

Answers marked with a `+` or a `*` must be selected for a correct answer, and
other answers must not be selected. Answers marked with a `-` or a `+` will be
pre-selected. So the result of the above is:

```{.QualitativeProblem .MultipleSelection}
1.2 How are you feeling today?
| - Bad!
| + OK!
| * I contain multitudes.
```


## Numerical

To create a numerical problem, use the class `.Numerical` and provide a
question and answer, in the format `ANSWER : QUESTION`, optionally pre-filling
with hint written below the question, like so:

    ```{.QualitativeProblem .Numerical}
    1.3 8 : How many bits in a byte?
    | 2^3
    ```

The above produces:

```{.QualitativeProblem .Numerical}
1.3 8 : How many bits in a byte?
| 2^3
```

Answers must be given as decimal expressions or fractions (so, the above $2^3$
won't be accepted without being evaluated). They'll be saved as decimal
expressions.

## Advanced Usage

#### Options and Attributes

In addition to allowing for turning off submission with `submission="none"`,
qualitative problems also have the following options. 

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------
`exam`                   Allows for submission of work which is incomplete or incorrect
`check`                  Adds a button which checks results without submitting
------------------------ ------------------------------------------------------------------

</div>

This won't have any effect on a short-answer question, since there's no notion
of "correct" to apply. Qualitative questions also permit assigning custom point
values with the `points=VALUE`, like most other graded problems.

Short answer questions also accept a `give-credit` option, which has the
following available settings

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------
`onSubmission`           Counts all submissions as correct
------------------------ ------------------------------------------------------------------

</div>

so, adding `give-credit="onSubmisson"` to a short answer question will award
credit automatically for any submission.
