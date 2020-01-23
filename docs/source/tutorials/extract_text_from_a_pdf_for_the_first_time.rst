.. _tutorials_first_time:

Extract text from a pdf for the first time
******************************************

This tutorial is specifically written for first-time users of pdfminer.six.
It will get you started with pdfminer.six and learn you how to install
pdfminer.six,
extract the text from a PDF and optimize the result. If you have any
questions or problems, consider raising an
`issue <https://github.com/pdfminer/pdfminer.six/issues/new/choose>`_.

Before you get started: make sure that you have a working installation of
Python 3.4 or higher and pip. Checkout this
`guide <https://realpython.com/installing-python/>`_
if you are not sure how to install Python and pip. After you did this you
should be able to run it on your commandline.

::

    $ python --version
    Python 3.7.5
    $ pip --version
    pip 18.1 from /usr/lib/python3/dist-packages/pip (python 3.7)

The output on your commandline can be slightly different, depending on the
Python version you are using and where it is installed.

Install pdfminer.six
====================

You need to install pdfminer.six before you can use it. This can be done on
the commandline using pip.

::

    $ pip install pdfminer.six
    Collecting pdfminer.six
      Downloading https://files.pythonhosted.org/packages/9f/75/d3e8067234872a30b6ca4cc38a26c13c76f1927c1d78bb807da7b4abc6b6/pdfminer.six-20200121-py3-none-any.whl (5.6MB)
        100% |████████████████████████████████| 5.6MB 8.0MB/s
    Collecting pycryptodome (from pdfminer.six)
      Downloading https://files.pythonhosted.org/packages/a9/49/146fe46dee2c79585e68f491b3ac5065bb2db1be191cb43a444961b12e8b/pycryptodome-3.9.4-cp37-cp37m-manylinux1_x86_64.whl (9.7MB)
        100% |████████████████████████████████| 9.7MB 6.5MB/s
    Collecting sortedcontainers (from pdfminer.six)
      Downloading https://files.pythonhosted.org/packages/13/f3/cf85f7c3a2dbd1a515d51e1f1676d971abe41bba6f4ab5443240d9a78e5b/sortedcontainers-2.1.0-py2.py3-none-any.whl
    Requirement already satisfied: chardet; python_version > "3.0" in /usr/lib/python3/dist-packages (from pdfminer.six) (3.0.4)
    Installing collected packages: pycryptodome, sortedcontainers, pdfminer.six
    Successfully installed pdfminer.six-20200121 pycryptodome-3.9.4 sortedcontainers-2.1.0

Again, the output on your commandline might have different details. The
important part is the confirmation that pdfminer.six is successfully installed.

Using pdf2txt to extract text from a pdf
========================================

Pdfminer.six includes several tools to work with PDF's. In this
tutorial you are going to use the pdf2txt commandline tool. After installing
pdfminer.six it is available on your commandline.

::

    $ pdf2txt --help
    usage: pdf2txt.py [-h] [--debug] [--disable-caching]
                      [--page-numbers PAGE_NUMBERS [PAGE_NUMBERS ...]]
                      [--pagenos PAGENOS] [--maxpages MAXPAGES]
                      [--password PASSWORD] [--rotation ROTATION] [--no-laparams]
                      [--detect-vertical] [--char-margin CHAR_MARGIN]
                      [--word-margin WORD_MARGIN] [--line-margin LINE_MARGIN]
                      [--boxes-flow BOXES_FLOW] [--all-texts] [--outfile OUTFILE]
                      [--output_type OUTPUT_TYPE] [--codec CODEC]
                      [--output-dir OUTPUT_DIR] [--layoutmode LAYOUTMODE]
                      [--scale SCALE] [--strip-control]
                      files [files ...]
    ...


Before you can use pdf2txt, you need a PDF file that you can extract text
from. For example, download the
:download:`"Hello World" PDF <../_static/hello_world.pdf>`.

Now you can use the pdf2txt command to extract the text from any PDF. In order
to run it you must know where the PDF is located on your filesystem.
This tutorial assumes that your current working directory is
the same as where the PDF file is located.

Run the pdf2txt command on the PDF file.

::

    $ pdf2txt hello_world.pdf
    Hello

    World

    Hello

    World

    H e l l o

    W o r l d

    H e l l o

    W o r l d


The text from the pdf is printed on the commandline. Notice that the order
of the text is intuitive, but that there are a lot of extra spaces and
enters in the text.


Removing intermediate spaces by changing the word-margin
========================================================

Pdfminer.six applies layout analysis to group characters into words and
words into lines. This layout analysis is governed by parameters that you can
adjust.

To improve the output you want to remove the spaces in the last two "Hello
World"'s. Pdfminer.six inserts these spaces because it considers the
characters to far apart to be part of the same word. You can change this
behaviour by adjusting the word-margin parameter. This parameter
specifies the maximum distance between characters of the same word. The default
value is 0.1. With this setting to few characters are grouped. To improve
the output you should increase the word-margin parameter.

::

    $ pdf2txt hello_world.pdf --word-margin 0.5
    Hello

    World

    Hello

    World

    Hello

    World

    Hello

    World


Remove intermediate newlines by changing the char-margin
========================================================

To improve the output further you should remove the newline characters
between "Hello" and "World". Increase the char-margin parameter to do this.

::

    $ pdf2txt hello_world.pdf --word-margin 0.5 --char-margin 5
    Hello  World

    Hello  World

    Hello  World

    Hello  World


This output looks a lot like the original!
