Compiling Universal Binaries under Mac OS X -- My Experience
############################################################

:author: C\. Titus Brown
:tags: cartwheel,macs
:date: 2007-03-28
:slug: compiling-x-platform-on-macs
:category: misc


I've spent a few months (on and mostly off) trying to get my C++/FLTK
program, `FamilyRelationsII <http://family.caltech.edu/>`__, to build
*on* my MacBook *for* both old and new Macs.

I was helped immensely by Mando Rodriguez and Diane Trout, both of whom
contributed various snippets.  Getting it all to play nice together was
still painful enough that I think it's time to contribute something back
to the lazyweb/googleplex.

Problem 1: Compiling FLTK cross-platform
----------------------------------------

I didn't actually keep notes for this, but basically I generated an X code project for FLTK and then selected "build cross-platform".

1. In your fltk-1.1.x directory, generate an Xcode project with
   ``cmake -G Xcode .``

2. ``open FLTK.xcodeproj``

3. Select "FLTK" in the "Groups and Files" pane (left)

4. Double-click, select 'Build'.  Double-click on Architectures.  Pick 'em both.

5. Assuming the build works, you should see something like 'bin/Debug/libfltk.a'.  These are the libraries you want.

I haven't figured out how to have them installed correctly yet; presumably
that's yet another click away.  At this point I just copy them into /usr/local/lib ;).

Problem 2: Compiling Xerces C++ cross-platform
----------------------------------------------

Substitute ::

   ./runConfigure -p macosx -n native -t native \
        -z -arch -z i386 -z -arch -z ppc \
        -l -arch -l i386 -l -arch -l ppc \
        -l -Wl,-syslibroot,/Developer/SDKs/MacOSX10.4u.sdk

for the default runConfigure command in the Xerces C documentation.
Then make, make install.

(I guess I'll contact the Xerces C people about adding this to their
docs...)

Problem 3(a): Linking /usr/local in properly
--------------------------------------------

Because FLTK and Xerces-C++ are installed into /usr/local/lib by default,
the ``-isysroot /Developer/SDKS/MacOSX10.4u.sdk`` stuff will not work
unless you also do this: ::

   % ln -fs /usr/local /Developer/SDKS/MacOSX10.4u.sdk/usr

Apparently you need to do this because ``-isysroot`` adds the
``/Developer/SDSKS/MacOSX10.4u.sdk/`` prefix on to all library and
header filename lookups; this lets Mac OS X know that universal libraries
etc can be found under /usr/local as well.

Problem 3(b): Compiling your own code properly
----------------------------------------------

The following CMake snippet (courtesy of Diane Trout) does the job well: ::

  if(APPLE)
    set(APPLE_COMPILE
        "-isysroot /Developer/SDKS/MacOSX10.4u.sdk -arch i386 -arch ppc")

    set(APPLE_LINK
         "-Wl,-syslibroot,/Developer/SDKs/MacOSX10.4u.sdk -arch ppc -arch i386")

    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${APPLE_COMPILE}")
    set(LINK_FLAGS "${LINK_FLAGS} ${APPLE_LINK}")
  endif(APPLE)

Then a standard 'cmake .' will put the right magic into your compilation
flags.

Problem 3(c): Distributing dylibs with your Mac app
---------------------------------------------------

If you're planning to *distribute* your universal binary, and it
depends on Xerces-C++ libraries, read `this very helpful Qt doc
<http://doc.trolltech.com/qq/qq09-mac-deployment.html>`__; look
esp at the Shared Libraries section.  This worked beautifully for me.

Briefly, you need to use install_name_tool on both the Xerces-C++ dylib
files *and* your compiled applications, to change the location in
which they will be looking for libxerces-c.27.dylib.  See
`my build-dist script diff <http://cartwheel.idyll.org/changeset/201>`__
for exactly what I do.

Conclusion: Double-checking stuff
---------------------------------

If at any point you run into trouble compiling with both the '-arch
ppc' and '-arch i386' flags, run 'file' on required libraries and
other binaries to make sure they're universal: ::

   % file FRII/app/FRII
   FRII/app/FRII: Mach-O universal binary with 2 architectures
   FRII/app/FRII (for architecture i386):  Mach-O executable i386
   FRII/app/FRII (for architecture ppc):   Mach-O executable ppc

Well, I hope this helps someone!  It was painful to learn, and AFAIK
the correct Xerces-C++ incantations are not available elsewhere on the
Web ;).

cheers,
--titus
