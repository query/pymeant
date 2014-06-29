# PyMEANT

PyMEANT is a proof-of-concept Python implementation of a simplified
version of the MEANT machine translation evaluation metric presented
in Lo et al. (2012).
It was originally submitted as a final course project for [the Machine
Translation class][mt-class] at Johns Hopkins University in spring 2014.
You may wish to read [the project writeup][writeup] for more details.

[mt-class]: http://mt-class.org/jhu/
[writeup]: https://github.com/query/mt-submissions/raw/master/project/writeup.pdf


## Caveats

Before using PyMEANT, please note the following:

* PyMEANT is an unoptimized pure-Python implementation, and as a result
  can be very slow even on modest data sets.

* Predicate and argument weighting are not implemented.
  Thus, PyMEANT's results cannot be directly compared with MEANT's.

* Jaccard similarity is used as the lexical similarity measurement, as
  described in Tumuluru et al. (2012), instead of the MinMax-MI metric
  outlined in the original paper.


## Usage

To install, use `setup.py`:

    $ python setup.py install

Before scoring translation hypotheses, you will need to train a lexical
similarity model using `python -m pymeant train`.
A parser for Gigaword corpus files is included for convenience:

    $ python -m pymeant.formats.gigaword nyt199504.gz | python -m pymeant train - lexsim.pkl

To perform the actual scoring, use `python -m pymeant score`, passing in
the hypotheses and reference sentences as both plain text (one per line)
and [ASSERT][assert]-tagged parse files:

    $ python -m pymeant score lexsim.pkl hypotheses.{txt,parse} reference.{txt,parse}

For further information, pass the `--help` option.

[assert]: http://cemantix.org/software/assert.html


## References

* Chi-kiu Lo, Anand Karthik Tumuluru, and Dekai Wu.
  2012.
  [Fully automatic semantic MT evaluation][W12-3129].
  In _Proceedings of the 7th Workshop of Statistical Machine
  Translation_, pages 243–252.
  Association for Computational Linguistics.

* Anand Karthik Tumuluru, Chi-kiu Lo, and Dekai Wu.
  2012.
  Accuracy and robustness in measuring the lexical similarity of
  semantic role fillers for automatic semantic MT evaluation.
  In _26th Pacific Asia Conference on Language, Information and
  Computation_, pages 574–581.

[W12-3129]: http://anthology.aclweb.org/W/W12/W12-3129.pdf
