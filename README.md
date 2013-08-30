# General CSS Guidelines Proposal

---

Now that we will be working on large, long running projects with multiple developers, it is essential that we all work in a unified way in order to:

* Write maintainable stylesheets
* Keep code transparent and readable
* Keep stylesheets scalable

## Contents

* [CSS document anatomy](#css-document-anatomy)
	* [General](#general)
	* [Single file vs many files](#single-file-vs-many-files)
	* [Table of Contents](#table-of-contents)
	* [Section Titles](#section-titles)
* [Order and Organization](#order-and-organization)
* [Ruleset Anatomy](#ruleset-anatomy)
* [Naming Conventions](#naming-conventions)
	* [JS hooks](#js-hooks)
* [Comments](#comments)

---

## CSS Document Anatomy

No matter the document, we must always try and keep a common formatting. This
means consistent commenting, consistent syntax and consistent naming.

### General

Limit your stylesheets to a maximum 80 character width where possible.
Exceptions may be gradient syntax and URLs in comments. There’s
nothing we can do about those.

I prefer single-tab indents set to four space size and write multi-line CSS.

### One file vs. many files

Some people prefer to work with single, large files. This is fine, and by
sticking to the proposed guidelines you’ll encounter no problems. Since moving
to Sass I have started splitting up my stylesheets out into lots of tiny includes.
Whichever method you choose, the following rules and guidelines apply. The only 
notable difference is with regards our table of contents and our section titles. 

### Table of contents

At the top of stylesheets, a table of contents will detail the
sections contained in the document, for example:

    /*------------------------------------*\
        $CONTENTS
    \*------------------------------------*/
    /**
     * CONTENTS............It's what you are reading
     * RESET...............Set our reset defaults
     * FONT-FACE...........Import brand font files
     */

This will tell the next developer(s) exactly what they can expect to find in
this file. Each item in the table of contents maps directly to a section title.

If you are working in one big stylesheet, the corresponding section will also be
in that file. If you are working across multiple files then each item in the
table of contents will map to an include which pulls that section in.

### Section titles

The table of contents would be of no use unless it had corresponding section
titles. Denote a section thus:

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/

The `$` prefixing the name of the section allows us to run a find ([Cmd|Ctrl]+F)
for `$[SECTION-NAME]` and **limit our search scope to section titles only**.

If you are working in one large stylesheet, you leave five (5) carriage returns
between each section, thus:

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/
    [Our
    reset
    styles]





    /*------------------------------------*\
        $FONT-FACE
    \*------------------------------------*/

This large chunk of whitespace is quickly noticeable when scrolling quickly
through larger files.

If you are working across multiple, included stylesheets, start each of those
files with a section title and there is no need for any carriage returns.

## Source order

Try and write stylesheets in specificity order. This ensures that you take full
advantage of inheritance and CSS’ first <i>C</i>; the cascade.

A well ordered stylesheet will be ordered something like this:

1. **Reset** – ground zero.
2. **Elements** – unclassed `h1`, unclassed `ul` etc.
3. **Objects and abstractions** — generic, underlying design patterns.
4. **Components** – full components constructed from objects and their
   extensions.
5. **Style trumps** – error states etc.

This means that—as you go down the document—each section builds upon and
inherits sensibly from the previous one(s). There should be less undoing of
styles, less specificity problems and all-round better architected stylesheets.

THis formatting is taken from Jonathan Snook's 
[SMACSS](http://smacss.com), which makes for excellent reading.

## Anatomy of rulesets

I recommend we follow a number of standards when structuring rulesets.

* Use hyphen delimited class names (except for BEM notation,
  [see below](#naming-conventions))
* 4 space indented
* Multi-line
* Declarations in relevance (NOT alphabetical) order
* Indent vendor prefixed declarations so that their values are aligned
* Indent our rulesets to mirror the DOM

A brief example:

    .widget{
        padding:10px;
        background-color:#C0FFEE;
        -webkit-border-radius:4px;
           -moz-border-radius:4px;
                border-radius:4px;
    }
        .widget-heading{
            font-size:1.5rem;
            line-height:1;
            font-weight:bold;
            margin-right:-10px;
            margin-left: -10px;
            padding:0.25em;
        }

We can see that `.widget-heading` must be a child of `.widget` as we have
indented the `.widget-heading` ruleset one level deeper than `.widget`. This is
useful information to developers that can now be gleaned just by a glance at the
indentation of our rulesets.

We can also see that `.widget-heading`’s declarations are ordered by their
relevance; `.widget-heading` must be a textual element so we begin with our
text rules, followed by everything else.

One exception to the multi-line rule might be in cases of the following:

    .t10    { width:10% }
    .t20    { width:20% }
    .t25    { width:25% }       /* 1/4 */
    .t30    { width:30% }
    .t33    { width:33.333% }   /* 1/3 */
    .t40    { width:40% }
    .t50    { width:50% }       /* 1/2 */
    .t60    { width:60% }
    .t66    { width:66.666% }   /* 2/3 */
    .t70    { width:70% }
    .t75    { width:75% }       /* 3/4*/
    .t80    { width:80% }
    .t90    { width:90% }


## Naming conventions

For the most part I simply use hyphen delimited classes (e.g. `.foo-bar`, not
`.foo_bar` or `.fooBar`), however in certain circumstances I use BEM (Block,
Element, Modifier) notation.

<abbr title="Block, Element, Modifier">BEM</abbr> is a methodology for naming
and classifying CSS selectors in a way to make them a lot more strict,
transparent and informative.