titus!
######

:author: C\. Titus Brown
:date: 2009-03-03
:slug: python-recs
:category: misc

i asked two other friends of mine, [ ... ], for recommendations about
model code and about their work environment.  their feedback was
extremely helpful and i thought you'd be interested to hear the
opinions of other good programmers.  i would also love to hear your
thoughts on these (extracted and scattered) comments:

Re: model code:
---------------

satra:

the nipy folks have actually done some nice things in their package

 - rest/sphinx for documentation
 - unit testing
 - traits

You should make your code based on pynifti. Also look at the code for
pymvpa, pyepl and rpy2.

In terms of structuring code, nipy for code organization and pymvpa for
architecture. Especially in your case, where you might want the ability for
users to compare multiple algorithms easily.

tyler:

I definitely agree with Satra.  I think in general, you'll want to:

1) Follow Python coding conventions (
   http://www.python.org/doc/essays/styleguide.html)
2) Use some sort of documentation generation system (epydoc is also very
   popular: http://epydoc.sourceforge.net/)
3) Have some unit testing, and an easy way to run regression tests whenever
   you make changes (at least on the critical code)

Unfortunately, Python 3 may take a while to mature, and get support
from scipy, numpy, matplotlib, etc., so you'll probably want to target
Python 2.x, but you should probably test the 2to3 tool once in a while
to make sure that your code can be easily converted
(http://docs.python.org/library/2to3.html). The projects that Satra
listed are all really good, and I would add that the python standard
modules are also a good place to dig around (somewhere in `python -c
"import sys;print sys.path"`).

Re: programming environment:
----------------------------

satra:

I would go with 2.6 if the other libraries have updated. I'm still on 2.5
for now and keep a keen eye towards minimizing the usage of the print
statement (probably the most important difference that could break code)!!

@:
it might not be time yet to do work in python 3 as tyler mentions, but i
spent the evening reading cython documentation.  if i understand what i've
read so far, since it is compatible with python 3 as well as Python 2.3 or
later, and works with numpy, this might be a cool way of coding and
compiling an application that works in both python worlds!

...the beauty of the cython route is that you can code in either 2.x or 3.x
(for the cython statements), compile, and i believe you can run it with
either 2.x or 3.x!  if i've got it right, you code your 3.x in cython and
you've got a cool transition.  what do you think?

otherwise, the recommended is as you say.  code in 2.6, use 2to3, and only
modify the 2.6 code until you stop maintaining 2.x, which seems like a pain
to me.

satra:

I'm going to rewrite in cython only when I need speed as opposed to writing
everything in cython. Unfortunately, thats the current problem with python.
Python 3 as you know broke several things to improve Python. I wouldn't
worry about doing 2to3 for now. Most establishments haven't even moved from
2.4. When distributing code, one has to partly care about the largest
userbase and at these large hospitals, things take a while to change. For me
my target is to disseminate to the entire FSL/SPM userbase. Can't be too
cutting edge for that.

I've looked at sagemath. Although neat, too symbolic for my current needs.

tyler:

I agree with everything Satra said.

Cython doesn't seem like the right way to go.

Regarding 2to3, all I'm suggesting there is that you periodically try
running it on your code to see what warnings it gives.  Basically, in theory
2to3 can automatically convert most of your code, but will sometimes find
something quirky that can't be automatically converted, so it might be nice
to know about that.  However, like Satra says, it will be a long time before
3 has a significant userbase, so it should be the least of your worries
right now.

Sagemath is very cool, and I think that underneath it's running fairly stock
python + libraries, but I think you're probably better off developing and
testing with the most vanilla possible python 2.x distribution.  The
enthought distro should be fine though. Arthur has some experience with
Sage, so you may want to ask him about it.

@:

so you're going to write in code that can be run by 2.4 or 2.5?
and you'll 2to3 later when more people use 3?

dependencies
------------

satra and tyler -- what dependencies would you consider reasonable:
numpy, matplotlib, pynifti, traits, cython, and sphinx?

satra:
Yes. Currently I'm writing it for 2.5.
I would add scipy and pyR to the list, but you can add modules easily later
on. I would definitely recommend ipython as your python console.

Re: ide vs. ipython:
--------------------

satra:

ipython has parallel computing options and I can use it interactively with
the -pylab switch. That was sufficiently motivating for me. But
ide's are a personal choice, so going with whatever you find most
convenient. I've also used SPE and komodo and I switch between all of
these according to various irrational whims.
...Emacs of course!! I haven't required an extensive debugger yet. So
ipython's minimal interface has been sufficient.

tyler:

I use vim + ipython.  My typical work cycle is to open a file that I'm
working on in vim, and open ipython in the same directory.  I'll make edits,
and the type "%run <filename> [args]" in ipython whenever I'm ready to test
the code.  That brings the whole file into ipython's namespace, and I can
generally debug sufficiently that way.  Sometimes I'll force a single
breakpoint in my code by putting "raise" on a line by itself, and doing %run
again. I can then inspect the state by doing a %whos, and printing
variables.  If you need more in depth debugging, you can do "%pdb on" in
ipython to cause pdb to be invoked automatically whenever your code raises
an exception (then you can step through the code, etc.).  Ipython can also
more tightly interact with vim and emacs by allowing you to pipe between
(for example) an emacs buffer and ipython (and vice versa), but I've never
felt the need to do that, and I couldn't get it to work exactly right when I
tried (google for emacs ipython integration maybe). I played for a few
minutes with WingIDE, and it seemed nice, but I never put in the time that
would be required to be proficient with it, so I'm happy hacking away with
the ubiquitous vi.  Some things that you might get with a full fledged IDE
that aren't as easy to get with emacs + ipython are: code completion, code
refactoring support, multi-file search and replace, etc..  As Satra said
though, choice of development environment is personal decision, and I can't
say what's right for you.
