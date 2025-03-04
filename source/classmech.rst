Class Mechanics
---------------

.. contents::

Class Github Page & Needed Dev Environment
++++++++++++++++++++++++++++++++++++++++++

All code, Latex sources for notes and other class material is on the
`class Github page
<https://github.com/ammarhakim/ast560-2025>`_. Please feel free to
reuse the material there, including **copying the Latex sources for
homework and projects**.

You need to create a Github account (if you do not have it already)
and fork the class Github, pulling it into your fork
periodically. **Programming homeworks will require you to pull the
code I provide and modify it in your own fork.**

You will need access to a computer that has a dev environment
installed. On it you will need, besides the **git** program, a **C/C++
compiler**, the **make** build system and, of course, a **code
editor**. You can use `Vs Code <https://code.visualstudio.com/>`_ if
you want. I personally use Emacs and sometimes Vim. (If you learn to
use Emacs or Vim your productivity will skyrocket. In general, you
want to pick a tool and learn it well. In particular, avoid using the
mouse while programming and muscle-memory learn various keystrokes to
do everything you need).

**We will update this section with more details as we go along**

Postgkyl Installation Instructions
++++++++++++++++++++++++++++++++++

Postgkyl is a Python-based post processing tool for analyzing and visualizing 
Gkeyll data. Instructions for installing Postgkyl on a range of platforms can be 
found at 
`read the docs <https://gkeyll.readthedocs.io/en/latest/install.html#postgkyl-install>`_ 
or on the 
`github page <https://github.com/ammarhakim/postgkyl?tab=readme-ov-file>`_.

Postgkyl on local Mac/Linux will require you to have Conda. One option is to 
download Anaconda for your specific platform 
`Anaconda docs <https://docs.anaconda.com/anaconda/install/>`_ and test the 
install by opening a terminal and verifying the install was successful with::

  conda --version

Alternatively, if you are working on a cluster such as Stellar or Perlmutter
you can load the Anaconda module (required for stellar only, Perlmutter 
loads this module by default)::

  module load anaconda3/2024.2

Once Conda is setup, install Postgkyl from a terminal with::

  git clone https://github.com/ammarhakim/postgkyl.git
  cd postgkyl
  conda env create -f environment.yml
  conda activate pgkyl     
  pip install -e .
  pytest [-v]

The installation is complete if pytests passes all 28 postgkyl tests. If
pytest fails, ensure you are in the correct enviroment (pgkyl), all dependencies
have successfully installed, and you have pip installed Postgkyl.

The next time you open a terminal, to activate Postgkyl simply reactivate 
the Postgkyl environment with::

  conda activate pgkyl

For Stellar only, you will need you to load Anaconda before activative the 
enviroment::

  module load anaconda3/2024.2 
  conda activate pgkyl

Installing the Simulation Library
+++++++++++++++++++++++++++++++++

.. note::

  You only need a C/C++ compiler and no other dependency to build the
  code. C/C++ compiler suites are available on all operating
  system. On Linux you will likely use GCC or Clang. Mac OSX comes
  with its own suite of developer tools that you must install
  following instruction on the Apple website. On Windows you could use
  the Windows Subsystem for Linux (WSL). You can look up instructions
  on how to get WSL and install a Linux distro (get Ubuntu) at
  numerous places online.

For code homework we will build on top of a stripped-down version of
the `GkeyllZero library <https://github.com/ammarhakim/gkylzero>`_. I
have already checked in this subset of the code we will need in the
class Github repo. You **do not** need to clone or install GkeyllZero.

To install the code needed in the simulations, fork the class repo
and/or pull latest changes into your fork. Then, cd into the `gminus`
directory and install the code on your machine::

  cd code/gminus
  make -j install

The code should build and install install in your home directory::

  ls $HOME/gkylsoft/gminus/

You can run the unit tests to ensure everything has built properly by
doing::

  make check


On use of the Maxima CAS
++++++++++++++++++++++++

When doing computation physics one ends up doing a lot of tedious
calculations. These can be easily automated and streamlined using a
computer algebra system (CAS). There are several excellent CASs, many
of them commercial. The most popular commercial products are
Mathematica and Maple. These are expensive, but I believe the
University may have discounted or corporate license for these.

I prefer to use the `Maxima <http://maxima.sourceforge.net>`_ CAS, a
free and open-source product that is, in some senses, the grand-daddy
of all CASs in existence today. It was originally developed using
Department of Energy (DOE) funding, went through several commercial
versions before being made fully open source. Maxima is old: it's
original developer has passed away to the spiritual realm long ago (I
guess he enjoys constant divine CAS bliss now), and many of hundreds
of authors who contributed have followed him, or have retired or
become senile, presumably. But the program lives on and is very
actively maintained, with extensive documentation and a very lively
mailing list for support.

Maxima is a phenomenal tool. It is mostly written in Common Lisp. (An
interesting archeological exercise is to examine old Lisp code in
Maxima and figure out what it does. Highly non-trivial!).  Maxima is
has a vast amount of features, and it is easy to extend using its own
custom language or Common Lisp.

A pleasant front-end for Maxima is provided by the `wxmaxima
<https://wxmaxima-developers.github.io/wxmaxima/>`_ program. This
provides a "document based" interface to Maxima and one can mix
regular text (and equations) with Maxima interactions.

A very comprehensive physics oriented tutorial is `Maxima by Example
by Edwin Woollett <https://web.csulb.edu/~woollett/>`_.

Maxima can be configured for your use. To do this, create the
directory (if it does not exist already)::

  mkdir $HOME/.maxima

In this create or edit the file called "maxima-init.mac" and add your
configurations to it.

To make plots with Maxima, you can use the excellent `draw2d/3d
<http://www.austromath.at/daten/maxima/zusatz/Graphics_with_Maxima.pdf>`_
packages. Chapter 4 of this manual describes the draw packages. To get
plotting to work you need to install `Gnuplot <http://gnuplot.info/>`_
and set some paths properly. On a Mac, the maxima-init.mac file looks
like::

  load("draw")$
  gnuplot_command: "/Applications/Gnuplot.app/Contents/Resources/bin/gnuplot" $
  set_plot_option([gnuplot_term, "qt"],
    [gnuplot_preamble, "set object rectangle from screen 0,0 to screen 1,1 behind fillcolor rgb 'white' fillstyle solid noborder"]
    )$

  set_draw_defaults(terminal=qt,
    user_preamble="set object rectangle from screen 0,0 to screen 1,1 behind fillcolor rgb 'white' fillstyle solid noborder",
    nticks=200,
    line_width=2
   )$

On Linux or Windows you will need to experiment with paths and
settings to get plots to work. You will at least need to change your
path to Gnuplot above.

Strange (But Useful) Computer Algebra Systems
+++++++++++++++++++++++++++++++++++++++++++++

There are a large number of specialized CAS that are often useful. I
mention a few here. 

`Cadabra <https://cadabra.science/>`_ is a powerful CAS specialized
for use in quantum field theory (QFT). It is particularly useful if
you want to do a lot of tensor manipulations, including on curved
spacetime.

A really interesting CAS is `GiNaC <https://www.ginac.de/>`_, a
computer algebra system written and usable from C++. GiNaC allows you
to embed a powerful CAS into your C++ programs and use the output on
the fly, for example, to evaluate complex expressions, or create C
code that implements those expressions for use in your
simulation. GiNaC was also developed for QFT and is particularly
suitable for Feynman integrals. However, it is very powerful, with
extensive support for General Relativity and Clifford
Algebra. However, it can only integrate polynomials! This may appear
very limiting, but in computational physics we typically only deal
with polynomial expansions anyway.
