# Carnap Documentation

1. [Carnap's Course Management Dashboard](dashboard.md)

   Explains how instructors set up courses, upload problem sets,
   assign uploaded problem set or problem sets from the [Carnap
   book](/book) them to their courses, and download grades.

2. [Carnap's Pandoc MarkDown](pandoc.md)

   Describes the format of problem sets that can be uploaded to and
   displayed by Carnap, and assigned to courses. This includes the
   MarkDown syntax, how to include problems in a problem set, how to
   display formulas, and how to include custom CSS or JavaScript on
   your problem sets.

3. Problem Types

   Carnap supports various kinds of problems, which are
   described on the following pages:

   a. [Syntax Checking](syntax-check.md) asks students to parse a formula.
   b. [Translation](translation.md) asks students for formulas
   which Carnap compares to model translations of English sentences.
   Can also be used for normal forms and equivalences.
   c. [Truth Tables](truth-tables.md) asks students to fill in
        truth tables and answer questions on the basis of truth tables.
   d. [Derivations](derivations.md) asks students to construct
      proofs in formal systems. Carnap can handle the following systems:
      - [Montague](montague.md): Montague-style systems, two of which
        are used in the Carnap book. 
      - [Logic Book](logicbook.md): The Fitch system used in Bergmann,
        Moore, and Nelson's *Logic Book*.
      - [forall x](forallx.md): Fitch system used in Magnus's original
        *forall x*.
      - [forall x: Calgary](forallx-yyc.md): Fitch system used in the
        *Calgary* version of *forall x* by Thomas-Bolduc and Zach.
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
   e. [Model Checking](modelchecker.md) asks students to
        provide first-order interpretations that make given formulas
        true or false, or show that arguments are invalid. 
   f. [Qualitative Problems](qualitative.md) provide ways for
        including multiple-choice, multi-select, short answer, and
        numerical questions on a problem set.
4. Installation Instructions
  a. [Carnap deployment/administration](administration.md)
  b. [Learning Tools Interoperability v1.3 integration](lti.md)
