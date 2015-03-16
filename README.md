Overview
========
An acceptably pythonic bayesian natural language processing / discrete
machine learning library.

Goals
=====
Key goals are simplicity, speed, elegance, and conciseness of user
code. This project is mainly intended as a research platform - something
really simple to use to build a quick model of language while the math
is being derived. Since so much time is spent in this discovery phase,
the runtime hit of python (obviated a bit by transparent
optimizations) shouldn't be too much of a burden.

Status
======
A naive bayes, a maximum entropy classifier, and an exact (as-in,
viterbi-decoded) hidden markov model are implemented. All rely on a mixture of C and
python, with rough cython alternatives.

Core code is mostly restricted to python, although inner loops are
optimized in C (see maxent.c for an example). Fallbacks to python are
possible although they currently do not happen gracefully. If you
don't feel like compiling the c code (simple as running setup.py
build!), you can edit the first line of counter.py to change to the
python counter type. This doesn't work for the maximum entropy model,
nor any other model that accesses an optimized C API the c counters export.

My current focus is on fleshing out chain models and generalizing some
of the shared code (higher-order class code could be designed to be
generic, as would the viterbi decoder and any future approximate
inference schemes). Following that, I'm hoping to start tackling some
real datasets and see if I can dig up anything cool

I'm also looking at porting the c layer to cython,
which appears, so far, to lead to a 2-3x slowdown (still hundreds of
times faster than python) with very little total effort (compared to
the moderately optimized, from a python module standpoint,
C). Porting to cython would also buy better 3.0 compatibility (I
think), but I haven't looked at this one bit.

Parallel computation, through map-reduce paradigm or the
multi-processing module would be interesting (and very nice for
slow-as-hell POS tagger testing), but I haven't really seen a huge
enough reason for it to write it. If I ever get a machine with more
than 2 cores this will be priority #1.
