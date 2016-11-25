TEX = WebContentRenderer.tex 

CLS = acmlarge.cls

STY = acmcopyright.sty

PACKAGE = acmlarge

PDF = ${TEX:%.tex=%.pdf} acm-update.pdf

PWD= ${shell pwd}

all: $(PDF)

%.pdf: %.tex $(CLS) $(STY)
	pdflatex $*
	bibtex $*
	pdflatex $*
	while ( grep -q '^LaTeX Warning: Label(s) may have changed' $*.log)\
	do pdflatex $*; done

acm-update.pdf:  ../documentation/acm-update.tex
	cd ../documentation; ${MAKE}; cd ${PWD}; cp ../documentation/$@ .

acmcopyright.sty:  ../acmcopyright/acmcopyright.dtx
	cd ../acmcopyright; ${MAKE}; cd ${PWD}; cp ../acmcopyright/$@ .

clean:
	$(RM) *.aux *.log  *.blg

distclean: clean
	$(RM) $(PDF) acm-update.pdf *.bbl

zip: all clean
	zip $(PACKAGE).zip * -x '*~' -x '*.tgz' -x '*.zip' -x CVS -x 'CVS/*'
