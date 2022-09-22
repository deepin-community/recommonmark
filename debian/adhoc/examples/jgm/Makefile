# /usr/share/doc/python-recommonmark-doc/examples/jgm/Makefile
#
# Ad hoc Makefile for building and playing with the sample sources
# distributed within the debian package python-recommonmark-doc.
#
# Recommended usage:
#  create a dedicated folder somewhere in your HOME directory;
#  link all the files in /usr/share/doc/python-recommonmark-doc/examples/jgm
#  in the dedicated folder; launch this Makefile in the dedicated folder:
#  $ make ;
#  for a basic cleanup, consider the clean target:
#  $ make clean ;
#  for an entire cleanup, the maintainer-clean target:
#  $ make maintainer-clean ;
#  for other targets, just read the Makefile.
#
# written for Debian by Jerome Benoit <calculus@rezozer.net>
# on behalf of the Debian Python Modules Team
# copyright: 2016 Jerome Benoit <calculus@rezozer.net>
# distributed under the terms and conditions of the MIT License
#

CMSHEETS = README.md

LISTOF_FORMAT_EXTENSION = \
	-ltx.pdf \
	-xltx.pdf \
	.html \
	.pseudoxml \
	.xml \
	.man

DOCUMENTS = $(foreach _fmtext,$(LISTOF_FORMAT_EXTENSION),$(patsubst %.md,%$(_fmtext),$(CMSHEETS)))

default: all

all: build

build: $(DOCUMENTS)

check: build

clean:
	$(RM) -r pdfbuild
	@$(RM) *.aux *.out *.log

composer-clean: clean
	$(RM) $(DOCUMENTS)

maintainer-clean: clean

%.man : %.md
	cm2man $< $@

%.xml : %.md
	cm2xml $< $@

%.pseudoxml : %.md
	cm2pseudoxml $< $@

%.html : %.md
	cm2html $< $@

%-xltx.tex : %.md
	cm2xetex $< $@

%-ltx.tex : %.md
	cm2latex $< $@

%-xltx.pdf : %-xltx.tex
	$(MKDIR_P) pdfbuild/$(*F)-xltx
	cp -l $< pdfbuild
	$(XELATEX) $(TEXFLAGS) -output-directory pdfbuild/$(*F)-xltx $<
	cp -l pdfbuild/$(*F)-xltx/$@ .

%-ltx.pdf : %-ltx.tex
	$(MKDIR_P) pdfbuild/$(*F)-ltx
	cp -l $< pdfbuild
	$(LUALATEX) $(TEXFLAGS) -output-directory pdfbuild/$(*F)-ltx $<
	cp -l pdfbuild/$(*F)-ltx/$@ .

TEXFLAGS = -interaction batchmode

LUALATEX ?= /usr/bin/lualatex
XELATEX ?= /usr/bin/xelatex

MKDIR_P ?= /bin/mkdir -p
