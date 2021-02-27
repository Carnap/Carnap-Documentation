#Frequently Asked Questions

<details>
<summary>How can I help my students recognize subproof boundaries better?</summary>

Carnap has a few options for indicating subproof boundaries. The two main
methods are to either render the proof separately from the input, or to overlay
indentation indicators that correspond to subproof boundaries.

The rendering option looks like this (details depending on the system):

~~~{.Playground .Prop options="fonts resize render" init="now"} 
|1.Show Q->P
|2.   Q         :AS
|3.   P         :PR
|4.:CD 3
~~~

and the overlay option looks like this (details depending on the system):

~~~{.Playground system="magnusSL" guides="fitch" init="now"} 
 P       :AS
 P/\P    :&I 1 1
 P       :&E 2
P->P     :->I 1-3
~~~

You can find details about overlaying indentation guides
[here](./derivations.md#indentation-guides), and details about the rendering
option [here](./derivations.md#options).

</details>

<details>
<summary>How can I encourage my students to slow down and think when writing derivations?</summary>

This is a good question. One option to discourage students from typing before
they think is to slow down the rate at which they get feedback. You can require
a button-press for feedback on a proof, or turn off feedback about correctness
entirely by using the settings `feedback="manual"` or `feedback="syntaxonly"`
respectively. Here's the link for more details on the [feedback
settings](./derivations.md#feedback).

</details>

<details> 
<summary>How can I use Carnap to give students an exam?</summary>

If you're using Carnap, an exam is an assignment just like any other
assignment. But depending on the type of format you want your exam to have, you
may want to set some options on that assignment.

If you'd like your students to be able to submit incorrect answers, rather than
having Carnap warn them when something is wrong, then you can add `exam` to the
options attribute of your exercises, writing them something like this:

    ~~~{.ProofChecker options="fonts exam" } 
    1.1 :|-: P->P
    ~~~

All the exercise types except for the syntax-checker support the `exam` option;
you can also set other options to disable checking or allow only certain types
of feedback on the unsubmitted work. Check the documentation for individual
exercise types to get the details on how to do that.

If your students are allowed to submit incorrect answers, you might want to
review them and assign partial credit. You can do that using the review area
that's associated with each assignment. There are also a few assignment
settings that might also be helpful for an exam. In particular, 

1. you can set a timer, so that exam needs to be completed in a certain number
   of minutes after its opened, and

2. you can set a "release date" for grades, so that students can only view
   grades after everyone has completed the exam.

Details on the review area, and assignment settings, can be found here:
[here](./dashboard.md#assign-uploaded-documents).

You may also want to know how reset the exam timer for certain students, or how
to offer accessibility accommodations for certain students. Information on how
to do that can be found [here](,/dashboard.md#actions-on-students)

</details>

<details>
<summary>How can I adjust deadlines for assignments?</summary>

There are two major deadlines associated with an assignment. One is the *due
date*. This is displayed on each student's user page, and determines whether
work counts as late. The other is the *visible* date. After the *visible* date
passes, the assignment is no longer visible to the student, and can't be
accessed. You can configure both of these dates by pressing the small "gear"
icon that appears next to the assignment listing in the "manage assignments"
tab on the instructor page.

You can also adjust deadlines per-student in two ways. One is to offer the
student an extension. You can do this by clicking the "calendar plus" icon
that appears next to the student's name in the class roster on your instructor
page. The extension will override both the due-date and the visibility date for
that student. You can also set a deadline adjustment policy for a specific
student by clicking the "clock" icon next to the student's name.

</details>

<details> 
<summary>How can I control student credit for late assignments?</summary>

By default, students receive half-credit (rounding down) for problems that are
submitted after the due date, but while the problem is still visible. However,
late credit is configurable using the `late-credit` option, which applies to
all exercises. You can set the `late-credit` option like this:

    ~~~{.SomeProblemType late-credit=4} 
    1.1 SOME PROBLEM
    ~~~

</details>

<details>
<summary>How can I control when grades are released?</summary>

Ordinarily, a student's score for a problem is visible (on the student's user
page) immediately after the student submits a problem. In some situations (for
example, during an exam), this can be undesirable.

If you want to release grades only after a certain time and date, then you can
set a "Release Grades After" time when you create the assignment. You can also
update this release time by pressing the "gear" icon next to the assignment on
your instructor page, in the "manage assignments" tab.

</details>

<details>
<summary>How can I embed a video in an assignment?</summary>

Carnap's markdown dialect supports [raw
HTML](https://pandoc.org/MANUAL.html#extension-raw_html), so you can embed
videos by including them in the same way that you might include them in an
ordinary webpage. There are two main options.

If your video is a file (a `.mp4`, `mov`, `avi` file or something similar) that
you have uploaded to a file hosting service somewhere, then you can point a
video tag at it by including something like this in your pandoc document:

    <video controls
        src="https://archive.org/download/day_the_earth_stood_still/day_the_earth_stood_still_512kb.mp4"
        width="560"></video>

Which will produce something like this (in browsers that support embedded
videos):

<video controls
    src="https://archive.org/download/day_the_earth_stood_still/day_the_earth_stood_still_512kb.mp4"
    width="560"></video>

More details on how to use `<video>` tags can be found
[here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video). 

Note: *Please don't upload video files to the Carnap site*. We're not designed
to serve these. Video files will need to be hosted elsewhere.

If your video hosted at a site like youtube or vimeo, rather than at a file
hosting service, then you can instead use an "embed code". Instructions for
obtaining an embed code for each of these services can be found here: [for
youtube](https://support.google.com/youtube/answer/171780?hl=en), and [for
vimeo](https://vimeo.zendesk.com/hc/en-us/articles/224969968-Embedding-videos-overview)

The embed code, when you get it, should look a bit like this:

    <iframe width="560" height="315"
        src="https://www.youtube.com/embed/nfeWlHVyBZQ" frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media;
        gyroscope; picture-in-picture" allowfullscreen></iframe>

And should result in something like this

<iframe width="560" height="315"
    src="https://www.youtube.com/embed/nfeWlHVyBZQ" frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope;
    picture-in-picture" allowfullscreen></iframe>

</details>

---

Want to offer a documentation suggestion or report a typo? Use the issue
tracker [here](https://github.com/Carnap/Carnap-Documentation/issues)!

Or, if you just have a quick question that's not addressed above, feel free to
send an email to [gleachkr@ksu.edu](mailto:gleachkr@ksu.edu)—if your question
comes up a lot, we'll add it to the FAQ.
