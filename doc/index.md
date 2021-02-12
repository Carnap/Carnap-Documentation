# Carnap Documentation

## Quick start guide

[Quick Start Guide for Instructors](quickstart.md)

Describes how you make assignments for use in Carnap, and how they are
made available to students.

## Using the Carnap site

[Carnap's Course Management Dashboard](dashboard.md)

Explains how instructors set up courses, upload problem sets,
assign uploaded problem set or problem sets from the [Carnap
book](/book) them to their courses, and download grades.

## Writing assignments

[Carnap's Pandoc MarkDown](pandoc.md)

Describes the format of problem sets that can be uploaded to and
displayed by Carnap, and assigned to courses. This includes the
MarkDown syntax, how to include problems in a problem set, how to
display formulas, and how to include custom CSS or JavaScript on
your problem sets.

[Carnap's JavaScript Extension API](javascript.md)

Describes how to incorporate external JavaScript into assignments, for custom
interactive behavior.

## Systems supported by Carnap

[Systems supported by Carnap](systems.md)

Describes the syntax, ASCII-only variants of symbols used, and
idiosyncrasies of the various systems supported by Carnap. Note: not all
of these systems have supported corresponding proof systems.

## Exercise types

Carnap supports various kinds of problems, which are
described on the following pages:

1. [Syntax Checking](syntax-check.md) exercises ask students to parse
   a formula.
2. [Translation](translation.md) exercises ask students for formulas
   which Carnap compares to model translations of English sentences.
      These can also be used for normal forms and equivalences.
3. [Truth Tables](truth-tables.md) exercises ask students to fill in
      truth tables and answer questions on the basis of truth tables.
4. [Derivations](derivations.md) exercises asks students to construct
      proofs in formal systems, which Carnap checks for correctness 
      on-the-fly. Carnap can handle the following systems:
  - [Montague](montague.md): Montague-style systems, two of which
    are used in the Carnap book. 
  - [Logic Book](logicbook.md): The Fitch system used in Bergmann,
        Moore, and Nelson's *Logic Book*.
  - [forall x](forallx.md): Fitch system used in Magnus's original
        *forall x*.
  - [forall x: Calgary](forallx-yyc.md): Fitch system used in the
        *Calgary* version of *forall x* by Thomas-Bolduc and Zach (and
        also in Tim Button's *forall x: Cambridge*.
  - [Chains of equivalences](equivalences.md): a simple proof system
    where every line results from the previous one by substituting 
    equivalents.
  - Fitch-style systems of Gamut's *Introduction to Logic*.
  - Systems based on Howard-Snyder's *The Power of Logic*.
  - Systems based on Hausman's *Logic and Philosophy*.
  - Lemmon-style systems based on Goldfarb's *Deductive Logic*.
  - Lemmon-style system based on Tomassi's *Logic*
  - Hardegree-style systems based on Hardegree's *Modal Logic*
  - [Sequent Calculus](sequent-calculus.md): Gentzen's sequent
        systems LK and LJ.
  - [Gentzen-Prawitz Natural Deduction](gentzen-ND.md): Gentzen's
        original tree-style natural deduction proofs as also used by
        Prawitz.
5. [Model Checking](modelchecker.md) asks students to
        provide first-order interpretations that make given formulas
        true or false, or show that arguments are invalid. 
6. [Qualitative Problems](qualitative.md) provide ways for
        including multiple-choice, multi-select, short answer, and
        numerical questions on a problem set.

## Installation instructions

1. [Carnap deployment/administration](administration.md)
2. [Learning Tools Interoperability v1.3 integration](lti.md)

---

Want to offer a documentation suggestion or report a typo? Use the issue
tracker [here](https://github.com/Carnap/Carnap-Documentation/issues)!
