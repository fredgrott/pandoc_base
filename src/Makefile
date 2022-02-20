all: pdf epub kindle html examples

BOOK_TITLE = A\ React\ Developer’s\ Guide\ to\ Hooks\ -\ Sebastien\ Castiel

dist:
	@mkdir -p dist

pdf: dist/${BOOK_TITLE}.pdf
	@echo '?  PDF'

epub: dist/${BOOK_TITLE}.epub
	@echo '?  ePub'

kindle: dist/${BOOK_TITLE}.mobi
	@echo '?  Kindle'

html: dist/${BOOK_TITLE}.html
	@echo '?  HTML'

examples: dist/Examples.zip
	@echo '?  Examples'

dist/${BOOK_TITLE}.pdf: dist content/*.md images/* resources/dracula.theme resources/header.tex
	@pandoc content/foreword.md content/toc.md content/ch*.md content/resources.md content/solutions.md \
	--output=dist/${BOOK_TITLE}.pdf \
	--highlight-style resources/dracula.theme \
	-H resources/header.tex --filter pandoc-crossref -V fontsize=12pt --number-sections -V documentclass=report

dist/${BOOK_TITLE}.html: dist content/*.md images/* resources/dracula.theme resources/header.html
	@pandoc content/foreword.md content/ch*.md content/resources.md \
	--output=dist/${BOOK_TITLE}.html \
	--highlight-style resources/dracula.theme \
	--standalone \
	-H resources/header.html \
	--metadata title="A React Developer’s Guide to Hooks"

dist/${BOOK_TITLE}.epub: dist content/*.md images/* resources/dracula.theme resources/metadata.xml resources/epub.css
	@pandoc content/foreword.md content/ch*.md content/resources.md \
	--output=dist/${BOOK_TITLE}.epub \
	--highlight-style resources/dracula.theme \
	--standalone \
	--epub-metadata=resources/metadata.xml \
	-c resources/epub.css \
	--epub-cover-image=cover.png \
	--toc --toc-depth=1 \
	--metadata title="A React Developer’s Guide to Hooks"

dist/${BOOK_TITLE}.mobi: dist/${BOOK_TITLE}.epub
	@kindlegen dist/${BOOK_TITLE}.epub -o ${BOOK_TITLE}.mobi >/dev/null 2>&1

dist/Examples.zip: examples/**/*
	@git archive --prefix=examples/ -o dist/Examples.zip HEAD:examples/

clean:
	@rm -rf dist