The Future of Bioinformatics (in Python), part 1 (a)
####################################################

:author: C\. Titus Brown
:tags: python,bioinformatics
:date: 2008-09-14
:slug: the-future-of-bioinformatics-part-1a
:category: science


Chris Lasher wrote a `nice blog post
<http://igotgenes.blogspot.com/2008/08/not-biopythonista-i-thought-id-be.html>`__
naming me as a rabble rouser in the area of "Python in
bioinformatics".  His post raised a number of interesting points, some
of which I'd like to discuss here on my blog.

First, why is Python not more dominant in bioinformatics?  I really
lay this at the feet of Lincoln Stein, who (from what I can tell) was
the dominant force behind BioPerl in the early days.  So it worked
really well and attracted all sorts of attention and users and actual
use. However, I think the tide is shifting away from Perl: from the
not-so-imminent release of a complex, backwardsly-incompatible Perl 6,
to the massive quantities of completely non-reusable Perl code that
have been flung in every direction, people are starting to get sick of
Perl.  also, a lot of people in academia are moving towards Python for
bioinformatics, if not in a very coordinated way: when I left Caltech,
two of the three heavy bioinformatics groups were using Python, and
when I arrived at MSU I found several groups doing bioinformatics in
Python and only one using Perl (and, at that, mainly because they rely
on GMOD).

Heck, there are a lot of Python-in-bio sightings these days.  I just
went to a talk by Rob Knight, who works on the human microbiome
project, and he mentioned developing `PyCogent
<http://sourceforge.net/projects/pycogent>`__ with some collaborators.
A lab on campus uses `TAMO
<http://bioinformatics.oxfordjournals.org/cgi/content/full/21/14/3164>`__
for motif searching.  `Cistematic <http://cistematic.caltech.edu/>`__
and a variety of tools from the Wold Lab use Python.  James Taylor is
working hard on developing `Galaxy
<http://genome.cshlp.org/cgi/doi/10.1101/gr.4086505>`__ into a general
purpose tool.  So I don't despair for Python's presence in biology.

I think the world is moving, medium-to-long-term, towards the use of
Perl for scripting-level work, Python for frameworks and re-usable
software, and R for statistical analysis of data sets (BioConductor is
also popping up a lot these days).  Personally I think this is the
right approach and bodes well in the long term.

--

Second, Chris says, 

  I think I have not worked with Biopython because I am not encouraged
  to do so, and am actually discouraged, because of research, and the
  current culture of academia.

I, too, am struggling with the problem that research scientists,
somewhat shockingly, are more interested in doing (and funding) novel
research than in building re-usable software.  OK, I'm being a bit
sarcastic, but that's only a mildly sarcastic statement, really; while
it's understandable that researchers want to *do research*, the rise
of large-scale data and computational methods in biology unambiguously
argues for computational competence in the next generation of
researchers.  Part of computational competence is knowing how to get
stuff done *effectively* and *correctly*, not to mention with
*reusable software* when possible.  I **am** actually shocked that
there's so little focus on `Software Carpentry
<http://www.swc.scipy.org/>`__-like skills in science and education,
and I'm doing my best to push on that front here at MSU (see `my very
first course here <http://ged.msu.edu/courses/2008-fall-cse-491/>`__,
which is introducing Python, Subversion and automated testing to CSE
undergrads).

That computing in biology sucks is not by any means a novel
observation; see this nice article, `Computational Biology Resources
Lack Persistence and Usability
<http://www.ploscompbiol.org/article/info:doi%2F10.1371%2Fjournal.pcbi.1000136>`__,
for example.  My take on things is that the funding bodies simply need
to recognize the utility of software maintenance, which is `slowly
happening
<http://grants.nih.gov/grants/guide/pa-files/par-05-057.html>`__, and
that the undergrad and graduate departments need to adapt to the
future by teaching this stuff.  But there's no question it's going to
be Darwinian out there -- as Stewart Brand says, "Once a new
technology starts rolling, if you're not part of the steamroller,
you're part of the road."  Hopefully some of us can be the steamroller
and not the road, yeh?

So what's my solution, you might ask?  Well, now that I'm a `bigshot
professor <http://ged.msu.edu/>`__, I'm going to be encouraging (well,
demanding where possible) that my students and collaborators use good
software development techniques and release their source code and
data.  But my real "secret" -- and please steal it if you can :) -- is
that I hope to continue building a real infrastructure that can
underlie solutions to my various research problems.  If I can build a
re-usable core of well-tested tools on top of a solid framework, I
*should* be able to do research faster, better, smarter, and more
reliably than my colleagues and competitors.  That *should* translate
into more publications, more grants, and more problems actually
solved.  (I'll let you know how that goes; it's early days still.)

That, incidentally, is why you should ignore people who tell you not
work on your coding or on general-purpose libraries: because if it's
useful to you, it's worth doing right and making it useful to yourself
in the future.

This is also one of the reasons why I'm investing a substantial amount
of my scarcest resource (time) in `pygr
<http://code.google.com/p/pygr>`__.  pygr is a solution for scalable
storage, retrieval, and named persistence of sequence-associated data,
and it works fantastically well.  The real problem with pygr is the
high barrier to entry, and that's what we're working on lowering, if
only so that my own students will have less trouble learning it.

Some other time I'll talk about why pygr and pygr-like solutions are
the *right* solution to reusability in bioinformatics.

So, in summary: don't worry, be happy, Python is coming to
bioinformatics one way or another.  And don't worry, just work hard at
becoming the steamroller (and not the road) by improving your coding
skills and becoming a general-purpose computational scientist, or at
least general-purpose bioinformatician.  You won't regret it.

Heck, you can always come work for me, right? ;)

--titus


----

**Legacy Comments**


Posted by Gregg Lind on 2008-09-15 at 09:34. 

::

   In addition to the general "I get a paper out of it if I rebuild it
   myself, and nothing but headaches if I work on someone else's project"
   that plagues all academic software dev, there are a few python
   specific problems at work.    1.  RPy is a little stale, and could
   probably use some updating, to make graphics easier to use.    2.
   There exists tension between Numpy and R about which is the proper
   tool for analysis.      In the lab I worked in at the U of MN, we
   switched over to python in 2005, away from perl.

