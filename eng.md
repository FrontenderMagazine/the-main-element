# The main element

Recently `<main>` was formally added to the W3C HTML specification. Now that
the dust has settled, it’s about time we dive in to find out where and when
it’s appropriate to use `<main>`. Let’s get started.

## History

The inclusion of a main element (or similar) has long been debated in the
working groups with authors and others often questioning why we had new
elements such as `<header>`, `<article>`, and `<footer>` but no element to
accurately describe the primary content of a page.

[Steve Faulkner][1], an accessibility consultant and new doctor in residence,
undertook the hard graft of carrying out research, gathering data and use
cases, and speaking to implementers to get them interested. As Steve explains,
he talked to:

> as many implementers (both general browser implementers and accessibility
> implementers), developers, authors and users as I could and got advice and
> input from them. I went where the various people hung out; on IRC, mailing
> lists, twitter, blogs, conferences — anywhere.
> [Steve Faulkner][1]

This led to his writing an [extension specification for `<main>`][2] and a thorough
[use case rationale][3].

The proposal [was accepted in November 2012][4], and `<main>` was then rolled into
the HTML5.1 specification. Recently, it was added to the HTML5 specification
following no objections. Lets have a look at how the spec describes `<main>`.

## W3C Specification

*You should still use the ARIA role until all browsers map the role to the
`<main>` element.*

The primary purpose of `<main>` is to map ARIA’s landmark role main to an
element in HTML. This will help screen readers and other assistive
technologies understand where the main content begins. The W3C spec describes
`<main>` as representing:

> The main content of the body of a document or application. The main content
> area consists of content that is directly related to or expands upon the
> central topic of a document or central functionality of an application. W3C
> [HTML Editors Draft][5]

Since the `<main>` element is now included in the HTML specification, the `<body>`
element has reverted to its HTML4 definition:

> The body element represents the content of the document.
> [W3C HTML Editors Draft][6]

## More Details

One important facet of `<main>` is that it can only be used once per page.
[Jeremy Keith wrote to the working group][7] to understand why this is the case
(rather than allowing multiple `<main>`s). Although I won’t go into detail, the
discussion is an interesting read.

As per the spec, the [W3C validator][8] throws an error if you attempt to use
multiple `<main>` elements per document.

Another stipulation of `<main>` is that it can’t be used as a descendant of an
`<article>`, `<aside>`, `<footer>`, `<header>`, or `<nav>` element.

Because `<main>` isn’t [sectioning content][9], it doesn’t affect the document
outline in the same way `<article>`, `<nav>`, or `<section>` do.

## Getting Going

Just as with the introduction of many other new HTML5 elements, not all
browsers recognise `<main>` or have preset styles for it. You’ll need to ensure
it displays as a block level element in your CSS:

    main {display:block;}

For the time being, you'll also need to use JavaScript to create the element
for older versions of IE:

    <script>document.createElement('main');</script>

Of course, if you use the [html5shiv][10], `<main>` is now baked in directly.

## Implementing `<main>` on HTML5 Doctor

The easiest way to implement `<main>` is to replace that `<div>` that you've
likely got with an id or class of something like main or content.

So what does that look like in practice? Well, here's our pre-`<main>` markup on
HTML5 Doctor:

    <body>
    <header role="banner">
    [...]
    </header>

    <div id="content" class="group" role="main">
    [...]
    </div>

    <footer role="contentinfo">
        [...]
    </footer>
    </body>

And here's what it's like now:

    <body>
    <header role="banner">
    [...]
    </header>

    <main id="content" class="group" role="main">
    [...]
    </main>

    <footer role="contentinfo">
        [...]
    </footer>
    </body>

*We'll get around to removing the `id="content"` at some point too.*

Yes it's really that simple. With any luck, it'll take you less than five
minutes to implement.

## The WHATWG Version

The WHATWG definition of `<main>` differs from the W3C version in that the
element has no meaning. It's merely a styling hook (like a `<div>` with a new
name) and represents its children.

> The main element can be used as a container for the dominant contents of
> another element. It represents its children.
> [WHATWG HTML][11]

We recommend using the W3C version of `<main>` as described above.

## Browser Support

[Firefox 21][12], Chrome 26, and a [WebKit r140374][13] have all implemented basic support
for `<main>`.

They have all mapped the ARIA `role="main"` to the `<main>` element so assistive
technologies can now recognise the `<main>` element without issue.

## Summary

As you've seen, it's super easy to get up and running with `<main>`. It only
takes a few minutes, so now really is the time to start adding it to the sites
you're developing.

If you aren't sure when or where to use `<main>`, be sure to ask us in the
comments and one of us will try to help you out.

## Further reading

* [Sitepoint — HTML5 Main Element][14]
* [MDN — main][15]
* [Ian Devlin — The main element][16]
* [Bruce Lawson — Using the main element][17]
* [Filament Group — The main element][18]
* [W3C — main element use cases][19]
* [Web Monkey — The main element lands a starring role in html][20]
* [Web Monkey — The main element would help HTML get to the point][21]

[1]: http://html5doctor.com/interview-steve-faulkner-html5-editor-new-doctor/
[2]: https://dvcs.w3.org/hg/html-extensions/raw-file/tip/maincontent/index.html
[3]: http://www.w3.org/html/wg/wiki/User:Sfaulkne/main-usecases#Introduction
[4]: http://lists.w3.org/Archives/Public/public-html/2012Nov/0232.html
[5]: http://www.w3.org/html/wg/drafts/html/master/grouping-content.html#the-main-element
[6]: http://www.w3.org/html/wg/drafts/html/master/sections.html#the-body-element
[7]: http://lists.w3.org/Archives/Public/public-html/2013Jan/0230.html
[8]: http://validator.w3.org/nu/
[9]: http://www.w3.org/html/wg/drafts/html/master/dom.html#sectioning-content-0
[10]: https://github.com/aFarkas/html5shiv
[11]: http://www.whatwg.org/specs/web-apps/current-work/multipage/grouping-content.html#the-main-element
[12]: http://www.mozilla.org/en-US/firefox/21.0/releasenotes/
[13]: http://nightly.webkit.org/builds/trunk/mac/14
[14]: http://www.sitepoint.com/html5-main-element/
[15]: https://developer.mozilla.org/en-US/docs/HTML/Element/main
[16]: http://www.iandevlin.com/blog/2013/01/html5/the-main-element
[17]: http://www.brucelawson.co.uk/2013/the-main-element/
[18]: http://filamentgroup.com/lab/the_main_element/
[19]: http://www.w3.org/html/wg/wiki/User:Sfaulkne/main-usecases#Introduction
[20]: http://www.webmonkey.com/2013/02/main-element-lands-a-starring-role-in-html/
[21]: http://www.webmonkey.com/2012/12/proposed-main-element-would-help-html-get-to-the-point/
