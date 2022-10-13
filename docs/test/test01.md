[TOC]

# Test01

## AdrianTest1

Some text just testing if the br tag works properly. Let me place one here <br> in the middle of the sentence.

## AdrianTest2

Now test blockquote with the guide info

> Release 5.26
>
> Document number: TP_OpenL_DG_3.6_LSh
> 
> Revised: 10-13-2022
> 
> OpenL Tablets Documentation is licensed under a Creative Commons Attribution 3.0 United States License.

And here is another pgf

Now lets see if it is better as code

```
Release 5.26

Document number: TP_OpenL_DG_3.6_LSh

Revised: 10-13-2022

OpenL Tablets Documentation is licensed under a Creative Commons Attribution 3.0 United States License.
```

And here is another pgf

Now test admonitions

!!! note
    You should note that the title will be automatically capitalized.

!!! danger "Don't try this at home"
    ...
    
!!! important ""
    This is an admonition box without a title.
    
    
 NOW SOME NUMBERED HEADING TESTS
 
 First I used Pandoc to make html with numbered headings. Then I reversed it to make markdown.
 
 here is the result:
 
 # [1]{.header-section-number} Welcome to Writage! {#welcome-to-writage number="1"}

Note that you can do all these things from the Writage menu.

## [1.1]{.header-section-number} Inline Formatting {#inline-formatting number="1.1"}

Only the following styles are supported:

-   **Bold**
-   *Italic*
-   **BoldItalic**
-   ~~strike~~

Note

## [1.2]{.header-section-number} Footnotes {#footnotes number="1.2"}

Notes can be placed anywhere[\^1](Yes,%20right%20here.) in the document,
press **References/Insert Footnote** (or Alt+Ctrl+F) to insert one.
Footnotes are displayed at the bottom of the corresponding page.

## [1.3]{.header-section-number} Quotes {#quotes number="1.3"}

To style some text as a quote apply style "Quote" from the styles.
Quotes are displayed inside the document with the left margin.

## [1.4]{.header-section-number} Hyperlinks {#hyperlinks number="1.4"}

Press **Insert/Link/ Insert Link** (or Ctrl+K) to insert a hyperlink. It
can be either literal URL (<http://www.google.com/>) or have some
[text](http://www.google.com/). Click URL with Ctrl key pressed to open
it in web browser.

## [1.5]{.header-section-number} Code blocks {#code-blocks number="1.5"}

Inline `code` gets monospaced font.

`Verbatim blocks use monospaced font as well and preserve line breaks`

In order to apply code block style from Word a "Source Code" style
should be created first.

## [1.6]{.header-section-number} Lists {#lists number="1.6"}

-   First bulleted item.
-   Second bulleted item.
-   

Lists can be styled via pressing **Bullets** or **Numbering** button or
using autoformatting: type minus and space for bulleted item or "1",
point and space for numbered item.

1.  First numbered item.
2.  Second numbered item.

## [1.7]{.header-section-number} Tables {#tables number="1.7"}

Press **Insert/Table** to create a table of required size, or use pop-up
menu to add more columns or rows. Here is a sample table.

\| From insert menu \| \| \|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\--\|
\| \| \| \| \| \|

\| From writage \| \| \| \| \|
\|\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\--\|\-\--\|\-\--\|\-\--\| \| \| \| \|
\| \|

\| **Features** \| **Editable in Word** \|
\|\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|
\| Basic Styles \| Yes \| \| Footnotes \| Yes \| \| Images \| Yes \| \|
Tables \| Yes \|

## [1.8]{.header-section-number} Image {#image number="1.8"}

Test

# [2]{.header-section-number} Happy writing! {#happy-writing number="2"}

Got a question? Drop us a line: <support@writage.com>.

