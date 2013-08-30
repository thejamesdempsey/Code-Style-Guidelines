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

Try and write stylesheets in specificity order. 

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

For the most part I recommend simply use hyphen delimited classes (e.g. `.widget-heading`, not
`.widget_heading` or `.widgetHeading`), however in certain circumstances we should use BEM (Block,
Element, Modifier) notation.

<abbr title="Block, Element, Modifier">BEM</abbr> is a methodology for naming
and classifying CSS selectors in a way to make them a lot more strict,
transparent and informative.

The naming convention follows this pattern:

    .block{}
    .block__element{}
    .block--modifier{}

* `.block` represents the higher level of an abstraction or component.
* `.block__element` represents a descendent of `.block` that helps form `.block`
  as a whole.
* `.block--modifier` represents a different state or version of `.block`.

An **analogy** of how BEM classes work might be:

    .person{}
    .person--woman{}
        .person__hand{}
        .person__hand--left{}
        .person__hand--right{}

BEM looks a little uglier, and is a lot more verbose, but it grants us a lot of
power in that we can glean the functions and relationships of elements from
their classes alone. Also, BEM syntax will typically compress (gzip) very well
as compression favors/works well with repetition.

Regardless of whether we need to use BEM or not, always ensure classes are
sensibly named; keep them as short as possible but as long as necessary. Ensure
any objects or abstractions are very vaguely named (e.g. `.ui-list`, `.media`)
to allow for greater reuse. Extensions of objects should be much more explicitly
named (e.g. `.user-avatar-link`). Don’t worry about the amount or length of
classes; gzip will compress well written code _incredibly_ well.

### Classes in HTML

In order to make things easier to read, separate classes in HTML with two
(2) spaces, thus:

    <div class="block--modifier  block__element">

This increased whitespace should hopefully allow for easier spotting and reading
of multiple classes.

### JS hooks

**Never use a CSS _styling_ class as a JavaScript hook.** Attaching JS behavior
to a styling class means that we can never have one without the other.

If we need to bind to some markup use a JS specific CSS class. This is simply a
class with `.js-`, e.g. `.js-toggle`, `.js-drag-and-drop`. This means
that we can attach both JS and CSS to classes in our markup but there will never
be any troublesome overlap.

    <span class="is-sortable  js-is-sortable">
    </span>

## Comments

For the sake of uniformity, I propose a docBlock-eque commenting style which will be 
limited to 80 characters in length:

	/**
	    * This is a docBlock style comment
	    *
	    * This is a longer description of the comment, describing the code in more
	    * detail. We limit these lines to a maximum of 80 characters in length.
	    *
	    * We can have markup in the comments, and should be encouraged to do so:
	    *
	      <div class="Bacon">
	          <p>Ipsum</p>
	      </div>
	    *
	    */


---

## Writing CSS

The previous section dealt with how we structure and form our CSS; they were
very quantifiable rules. The next section is a bit more theoretical and deals
with our attitude and approach.

## Building new components

When building a new component write markup **before** CSS. This means you can
visually see which CSS properties are naturally inherited and thus avoid
reapplying redundant styles.

By writing markup first we will can focus on data, content and semantics and then
apply only the relevant classes and CSS _afterwards_.

## OOCSS

I work in an OOCSS manner; I split components into structure (objects) and
skin (extensions). As an **analogy** (note, not example) take the following:

    .room{}

    .room--kitchen{}
    .room--bedroom{}
    .room--bathroom{}

We have several types of room in a house, but they all share similar traits;
they all have floors, ceilings, walls and doors. We can share this information
in an abstracted `.room{}` class. However we have specific types of room that
are different from the others; a kitchen might have a tiled floor and a bedroom
might have carpets, a bathroom might not have a window but a bedroom most likely
will, each room likely has different colored walls. OOCSS teaches us to
abstract the shared styles out into a base object and then _extend_ this
information with more specific classes to add the unique treatment(s).

So, instead of building dozens of unique components, try and spot repeated
design patterns across them all and abstract them out into reusable classes;
build these skeletons as base ‘objects’ and then peg classes onto these to
extend their styling for more unique circumstances.

If you have to build a new component split it into structure and skin; build the
structure of the component using very generic classes so that we can reuse that
construct and then use more specific classes to skin it up and add design
treatments.

## Layout

All components you build should be left totally free of widths; they should
always remain fluid and their widths should be governed by a parent/grid system.

Heights should **never** be be applied to elements. Heights should only be
applied to things which had dimensions _before_ they entered the site (i.e.
images and sprites). Never ever set heights on `p`s, `ul`s, `div`s, anything.
You can often achieve the desired effect with `line-height` which is far more
flexible.

Grid systems should be thought of as shelves. They contain content but are not
content in themselves. You put up your shelves then fill them with your stuff.
By setting up our grids separately to our components you can move components
around a lot more easily than if they had dimensions applied to them; this makes
our front-ends a lot more adaptable and quick to work with.

You should never apply any styles to a grid item, they are for layout purposes
only. Apply styling to content _inside_ a grid item. Never, under _any_
circumstances, apply box-model properties to a grid item.

## Sizing UIs

I use a combination of methods for sizing UIs. Percentages, pixels, ems, rems
and nothing at all.

Grid systems should, ideally, be set in percentages. Because I use grid systems
to govern widths of columns and pages, I can leave components totally free of
any dimensions (as discussed above).

Font sizes can be set in rems with a pixel fallback. This gives the accessibility
benefits of ems with the confidence of pixels. Here is a handy Sass mixin to
work out a rem and pixel fallback for you (assuming you set your base font
size in a variable somewhere):

    @mixin font-size($font-size){
        font-size:$font-size +px;
        font-size:$font-size / $base-font-size +rem;
    }

I only use pixels for items whose dimensions were defined before the came into
the site. This includes things like images and sprites whose dimensions are
inherently set absolutely in pixels.


## More to Come...