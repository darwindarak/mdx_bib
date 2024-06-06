# Bibliography and Citation support for Python-Markdown

This extension to Python Markdown is inspired by the support for citations in [R Markdown][].
It looks for all citation keys with the form `@<citekey>` inside matching square brackets and appends a bibliography to the output.
The references associated with the citation keys can be defined manually or generated from a BibTeX file.

## Installation

Running 

```bash
$ python setup.py build
$ python setup.py install
```

will install a module named `mdx_bib`.

```python
import markdown
from mdx_bib import CitationsExtension

cite = CitationsExtension(bibtex_file='library.bib', order='unsorted')
html = markdown.markdown(text, extensions=[cite])
```

## Syntax

Citation keys are any identifiers inside square brackets with a `@`-prefix

```markdown
Some claim [see @adams98].

Some claim [@adams98; @barney04].
```

The first line will be converted

```html
<p>Some claim [see <a id="cite-adams98" href="#ref-adams98" class="citation>@adams98</a>.</p>
```

This extension will first look for any manually defined bibligraphy entries, for example

```markdown
[@barney04]: Barneby, C.D. *A review of reviews*. Annual Reviews of Something (2104)
```

If a matching reference definition cannot be found, then the extension looks in the BibTeX file for a matching citation key.

[R Markdown]: http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html

## Changelog

### 2023-04-05

- replace from `markdown.util import etree` with `import xml.etree.ElementTree as etree` per this [Python-Markdown 3.2 changelog](https://github.com/Python-Markdown/markdown/blob/master/docs/change_log/release-3.2.md)
