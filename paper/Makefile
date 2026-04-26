# Build the SciPost Physics Codebases manuscript.
#
# Default target: produce main.pdf via the standard pdflatex + bibtex
# loop. The SciPost.cls and SciPost_bibstyle.bst class/style files are
# vendored in this directory (CC0-licensed by SciPost).

PAPER := main

# Extra latexmk options can be passed via $(LMKOPTS) on the command line.
LMKOPTS ?=

.PHONY: all clean distclean view

all: $(PAPER).pdf

$(PAPER).pdf: $(PAPER).tex refs.bib SciPost.cls SciPost_bibstyle.bst
	@if command -v latexmk >/dev/null 2>&1; then \
	  latexmk -pdf -bibtex -interaction=nonstopmode $(LMKOPTS) $(PAPER).tex; \
	else \
	  pdflatex -interaction=nonstopmode $(PAPER).tex; \
	  bibtex   $(PAPER); \
	  pdflatex -interaction=nonstopmode $(PAPER).tex; \
	  pdflatex -interaction=nonstopmode $(PAPER).tex; \
	fi

view: $(PAPER).pdf
	@command -v xdg-open >/dev/null 2>&1 && xdg-open $(PAPER).pdf || \
	 command -v open     >/dev/null 2>&1 && open     $(PAPER).pdf || \
	 echo "Open $(PAPER).pdf in your viewer of choice."

clean:
	@rm -f $(PAPER).aux $(PAPER).log $(PAPER).out $(PAPER).toc \
	       $(PAPER).bbl $(PAPER).blg $(PAPER).bcf $(PAPER).run.xml \
	       $(PAPER).fdb_latexmk $(PAPER).fls $(PAPER).synctex.gz

distclean: clean
	@rm -f $(PAPER).pdf
