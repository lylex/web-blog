Id: 229002
Title: Converting PartCover results to html
Tags: .net
Date: 2010-07-23T16:51:34-07:00
Format: Markdown
--------------
What is PartCover
=================

[PartCover](http://sourceforge.net/projects/partcover/) is a code
coverage tool for .NET. The original sourceforge project seems to be
inactive but there’s a [fork on
github](http://github.com/sawilde/partcover.net4) with a bit more recent
work.

You can read my [short
tutorial](/article/Introduction-to-PartCover-a-short-manual.html) for
basics of PartCover usage.

Why use code coverage?
======================

Recently I started working on improving [an object-oriented
database](http://github.com/kjk/volante) for Java and .NET. The code
wasn’t written by me, it’s quite mature but it doesn’t have many tests,
so I’m quite apprehensive about modifying subtle code and clearly would
like to avoid introducing bugs.

A test suite is a good way to detect newly introduced regressions but
sadly while the code is quite brilliant, its tests are rudimentary. I
decided that the first thing I will work on is improving and extending
test suite.

However, the space of all possible tests is infinite and since I don’t
have infinite amount of time to write tests, I should write a minimal
amount of tests that cover maximum amount of code. Writing duplicate
tests is not productive.

Code coverage can be used to guide creation of new tests. Code coverage
tools can tell you which parts of the code where executed so the
algorithm for generating new tests is as follows:

-   run current tests suite under code coverage tool
-   check the results to see which parts of the code are not yet
    exercised by current tests
-   devise a test that exercise those parts
-   re-run the test suite under code coverage tool to verify that the
    new test really causes the code to be executed
-   repeat until yet get close to 100% code coverage

Why use PartCover
=================

PartCover isn’t that great but all other alternatives (code coverage
built into more expensive editions of Visual Studio and NCover) are
expensive. PartCover is at least free (and open-source).

Examining PartCover results
===========================

PartCover produces an XML file with the results of code coverage. There
is a PartCover.Browse GUI app that shows the results but it’s rather
clunky. Here’s how it looks like:

![PartCover GUI browser](http://kjkpub.s3.amazonaws.com/blog/img/partcover-browse.png "PartCover GUI browser")

There’s also XSLT files to convert XML to html file, but the result is
very basic and not very useful.

Since built-in options were slim, I decided to write a [python
script](http://github.com/kjk/volante/blob/master/csharp/partcover-to-html.py)
that converts XML file to a set of HTML files with easy to browse
results of code coverage.

Take a look at [example results](/articles/coverhtml/index.html).

I took me a day to write so I decided to share it to hopefully save
others some effort.

Using partcover-to-html.py
==========================

Usage: `partcover-to-html.py <partcover-output.xml> <outdir>`

`<partcover-output.xml>` is an XML file with code coverage information
generated by PartCover.

`<outdir>` is a directory where the output will be stored. A new
directory `coverhtml-${NNN}` will be created and html files put there,
with `index.html` being the starting point.

The reason for creating a new directory is to not overwrite results of
previous analysis, so that it’s possible to compare coverage before and
after a change in the code. \${NNN} is a unique, increasing integer
(i.e. 000, 001, 002 etc.)

The script generates files that [look like
this](/articles/coverhtml/index.html)

Note: when adapting for your own purpose, you’ll need to modify\
`File._calc_names()`.