# Carnap's Pandoc MarkDown

Within Carnap, shared documents and problem sets are created using *pandoc*
markdown, a simple formatting language (akin to LaTeX) developed by John
McFarlane as part of the [Pandoc](https://pandoc.org) project. Pandoc markdown
extends John Gruber's original markdown syntax with some additional niceties.

It would be a little redundant to give the full specifications for pandoc
markdown here, since there are many excellent resources already available.
See, instead,

1. John Gruber's original [markdown
   specification](https://daringfireball.net/projects/markdown/).
2. The [Pandoc user's guide](http://pandoc.org/MANUAL.html#pandocs-markdown)

If you learn best from example, it's also possible to download the source code
for documents shared on Carnap.io from the shared document list, available at
<https://carnap.io/shared>. The pandoc source for this document, should you
wish to inspect it, is available
[here](https://github.com/Carnap/Carnap-Documentation/blob/master/doc/pandoc.md).

You can create pandoc documents in any text editing program. Pandoc is nothing
but plain text that is written with some special notation to indicate how text
is to be formatted. For example, you can write `*italic*` to generate the text
"*italic*". However, there are some very good text-editor plugins and dedicated
applications available for working with Pandoc. These provide extra features
like live previews of the formatted text. A list of these can be found
[here](https://github.com/jgm/pandoc/wiki/Pandoc-Extras#editors). An online
pandoc editor, with live previews of what the rendered document will look like,
can be found at <http://markup.rocks>.

## Pandoc Extensions

Carnap's pandoc parser incorporates the following pandoc extensions:

* [raw\_html](https://pandoc.org/MANUAL.html#raw-html)
* [markdown\_in\_html\_blocks](https://pandoc.org/MANUAL.html#raw-html)
* [auto\_identifiers](https://pandoc.org/MANUAL.html#headings-and-sections)
* [tex\_math\_dollars](https://pandoc.org/MANUAL.html#math)
* [fenced\_divs](https://pandoc.org/MANUAL.html#extension-fenced_divs)
* [bracketed\_spans](https://pandoc.org/MANUAL.html#extension-bracketed_spans)
* [fenced\_code\_blocks](https://pandoc.org/MANUAL.html#fenced-code-blocks)
* [backtick\_code\_blocks](https://pandoc.org/MANUAL.html#fenced-code-blocks)
* [line\_blocks](https://pandoc.org/MANUAL.html#line-blocks)
* [fancy\_lists](https://pandoc.org/MANUAL.html#ordered-lists)
* [startnum](https://pandoc.org/MANUAL.html#extension-startnum)
* [definition\_lists](https://pandoc.org/MANUAL.html#definition-lists)
* [example\_lists](https://pandoc.org/MANUAL.html#numbered-example-lists)
* [simple\_tables](https://pandoc.org/MANUAL.html#tables)
* [multiline\_tables](https://pandoc.org/MANUAL.html#tables)
* [footnotes](https://pandoc.org/MANUAL.html#footnotes)
* [fenced\_code\_attributes](https://pandoc.org/MANUAL.html#fenced_code_blocks)
* [inline_code\_attributes](https://pandoc.org/MANUAL.html#fenced_code_blocks)
* [shortcut\_reference\_links](https://pandoc.org/MANUAL.html#reference-links)
* [link\_attributes](https://pandoc.org/MANUAL.html#extension-link_attributes)
* [yaml\_metadata\_block](https://pandoc.org/MANUAL.html#metadata-blocks)
* [task\_lists](https://pandoc.org/MANUAL.html#ordered-lists)

For more details, about each of these extensions, please see the [Pandoc Users
Guide](https://pandoc.org/MANUAL.html#extensions).

## Exercises

### General Pattern

Carnap's exercises are created by including special *code blocks* within a
pandoc document. A code block looks something like this:

    ~~~ 
    CONTENT GOES HERE
    ~~~

To indicate which type of exercise you want to create, you apply *classes* and
*data attributes* to the code block. That would look something like this:

    ~~~{.SOMECLASS .ANOTHER attribute="value"}
    label CONTENT GOES HERE
    ~~~

with classes indicated by a leading `.`, and attributes assigned with the `=`
sign, and surrounded by quotes. 

The leading `label` within the body of the code block will be used to generate
an anchor tag to your exercise, so that you can link directly to the exercise
at the URL `ASSIGNMENTURL#exercise-label` where `ASSIGNMENTURL` is the URL for
the assignment, and `label` is the label you gave to that particular exercise.

### Some common attributes

Here are some common attributes that can be applied to to any exercise

<div class="table">

Name                     Effect
------------------------ ------------------------------------------------------------------
`points`                 Sets a custom point value
`late-credit`            Sets a custom point value for a late submission
`submission`             Controls how work is submitted. Set to "none" to disable submission
`options`                Exercise-specific options
------------------------ ------------------------------------------------------------------

</div>

the `options` attribute might require some extra explanation. This attribute is
set to a string of space separated words, indicating what special options are
set for the exercise-block it is attached to. Different types of exercises
allow for different options.

### Random problems

When you create a problem set, the different problems within a code block will
generally be assigned numbers or some other identifier. So you might write

    ~~~ 
    1.1 SOME PROBLEM
    ~~~

If the same identifier is used for a contiguous series of problems (all part of
the same code block and next to one another), then when the problem set is
assigned and viewed by a student, one of the problems in the series will be
chosen randomly and displayed. So, for example given 

    ~~~ 
    1.1 PROBLEM A
    1.1 PROBLEM B
    ~~~

Students will see PROBLEM A or PROBLEM B, but not both. A student reloading the
page will continue to see the same problem, so if they see PROBLEM A on the
first viewing, they'll continue to see PROBLEM A.

The selection of a random problem only takes place when the document is viewed
as an assignment, so when the document is viewed through the instructor's
"manage documents" tab, all the variant problems will be displayed.

### Choose-One problems

If more than one problem is given the same label but the problems are *not*
part of the same code block or are not next to one another, then both problems
will be displayed. However, within each assignment, a student can submit at
most one problem with a given label. So if you want to give your students the
option to choose just one of several problems to complete, you can set those
problems to all share a single label.

### Exercise Types

There are currently eight types of exercises:

1. [Syntax Checking](./syntax-check.md)
2. [Translation](./translation.md)
3. [Truth Tables](./truth-tables.md)
4. [Derivations](./derivations.md)
5. [Model Checking](./modelchecker.md)
6. [Qualitative Problems](./qualitative.md)
7. [Sequent Calculus Problems](./sequent-calculus.md)
8. [Gentzen-Prawitz Natural Deduction Problems](./gentzen-ND.md)

To learn more about each one, follow the links above.

## Other Features

### Formula Parsing

Carnap's formula parser can be used to render and display formulas and sequents
inline within a pandoc document. So for example, writing something like

    `AxF(x)\/Ex-F(x)`{system="firstOrder"}

Will produce the output `AxF(x)\/Ex-F(x)`{system="firstOrder"}.

Any system that's available for [derivations](./derivations.md) can
be used in the formula parser. The available propositional systems are: `prop`
`montagueSC` `LogicBookSD` `LogicBookSDPlus` `hausmanSL` `howardSnyderSL`
`ichikawaJenkinsSL` `hausmanSL` `magnusSL` `magnusSLPlus`
`thomasBolducAndZachTFL` `thomasBolducAndZachTFL2019` `gamutMPND`, `gamutIPND`
`gamutPND` `gamutPNDPlus` `tomassiPL` and `hardegreeSL`. The available
first-order systems are: `firstOrder` `montagueQC` `magnusQL`
`thomasBolducAndZachFOL` `thomasBolducAndZachFOL2019`
`thomasBolducAndZachFOLPlus2019` `LogicBookPD` `LogicBookPDPlus` `gamutND`
`hausmanPL` `howardSnyderPL` `ichikawaJenkinsQL` `hardegreePL` `goldfarbAltND`
`goldfarbNDPlus` and `goldfarbAltNDPlus`. The available set theory systems are:
`elementarySetTheory` and `separativeSetTheory`. The available second-order
systems are: `secondOrder` and `PolySecondOrder`. The available propositional
modal logic systems are: `hardegreeL` `hardegreeK` `hardegreeT` `hardegreeB`
`hardegreeD` `hardegree4` and `hardegree5`. The available predicate modal logic
system is `hardegreeMPL`, and the available "world theory" system is
`hardegreeWTL`.

### Custom CSS

The standard [bootstrap](https://getboostrap.com) CSS that is used for styling
the appearance of an assignment can be overriden by including a `css` entry as
part of a [yaml metadata block](https://pandoc.org/MANUAL.html#metadata-blocks)
within a carnap pandoc document.

The CSS entry can include either a url for a single CSS stylesheet, like so:

    ---
    css: https://ghcdn.rawgit.org/Carnap/Carnap-Contrib/main/css/hide-points.css 
    --- 

or for several stylesheets, like so:

    ---
    css:
    - https://ghcdn.rawgit.org/Carnap/Carnap-Contrib/main/css/hide-points.css
    - https://ghcdn.rawgit.org/Carnap/Carnap-Contrib/main/css/another-stylesheet.css
    --- 

The stylesheets can be hosted anywhere, including on the Carnap server. In
order to host a stylesheet, just upload it as if it were a pandoc document, but
be sure to give it the filetype extension "css", so name it something like
"mystylesheet.css". You'll then able able to access it with a metadata block of
the form:

    --- 
    css:
    - https://carnap.io/shared/youremail@gmail.com/custom.css
    --- 

If you wish to not just partly override the bootstrap css, but to completely
disable it, adding your new css to a blank slate (other than the css used to
style Carnap's exercises), then you can instead use a `base-css` entry to set
the new base css style. For example,

    --- 
    base-css: 
    - https://static.carnap.io/css/tufte.css
    - https://static.carnap.io/css/tuftextra.css
    --- 

will configure your document to have a
[tufte-like](https://edwardtufte.github.io/tufte-css/) style, with no traces of
bootstrap.

For more details about hosting your own stylesheets, please take a look at the
documentation for the [instructor dashboard](dashboard.md).

### Custom JavaScript

Documents can also include links to custom JavaScript. This can be done using
the `raw_html` pandoc extension to include a `<script>` tag, or by including
the JS in a metadata block. Like a CSS entry, a JS entry entry can include
either a url for a single CSS stylesheet, like so:

    ---
    js: https://carnap.io/shared/myemail@university.edu/myjs.js
    --- 

or for several stylesheets, like so:

    ---
    js:
    - https://carnap.io/shared/myemail@university.edu/myjs1.js
    - https://carnap.io/shared/myemail@university.edu/myjs2.js
    --- 

The scripts can be hosted anywhere, including on the Carnap server. As with
stylesheets, scripts can be uploaded as normal documents so long as they're
given the proper filetype extension (in this case, ".js" rather than ".css")
