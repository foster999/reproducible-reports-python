# Reproducible Reports in Python

This repo contains [a minimal example reproducible analytical report](./example.md) written as a [Markedly Structured Text (MyST) Notebook](https://github.com/executablebooks/MyST-NB)). This document can be used to create a HTML report by installing the [Python dependencies](./requirements.txt) (`pip install -r requirements.txt`) and running `make html` from the root of the project.

Below, the syntax for MyST Notebooks is compared with that of [Rmarkdown](https://rmarkdown.rstudio.com/). This aims to provide a reference for Python users, looking for an R-independent equivalent to Rmarkdown. The [default Rmarkdown template](./example.Rmd) is included for reference.

## Comparison of MyST Notebooks with Rmarkdown

Both document types use similar code cells or chunks to separate code from Markdown content. Key differences between MyST `.md` and Rmarkdown `.Rmd` files are detailed below. 

These examples only scratch the surface of functionality available in each tool, so please do get in touch or add any other differences in commonly used syntax.

### Document options (front matter)

Both formats offer document-level options, which are written at the start of the document as YAML enclosed within `---` markers:

```
---
key: value
---
```

| Option | MyST-NB | Rmarkdown |
|---|---|---|
| Document title (displayed in browser tab) | `title:`| `title:`|
| Output format | Specified when building with `sphinx`, for example `make html`| `output:` |
| Formats for conversion to/from `.ipynb` notebook files |`jupytext:`| Doesn't require conversion to be executed |
Kernel to be used to execute notebook code |`kernelspec:`| specified on cell by cell basis (see below) |

### Cell metadata (chunk options)

MyST Notebooks include these at the start of the cell, as options for the `code-cell` directive:
````markdown
```{code-cell} ipython3
:key: val

```
````

Rmarkdown includes these in the curly braces of the code chunk definition:
````r
```{r key=value}
```
````

Alternatively, Rmarkdown chunk options can be set document-wide using the following syntax within a code chunk:
```r
knitr::opts_chunk$set(key=value)
```


| Option | MyST-NB | Rmarkdown |
|---|---|---|
| Hide code cell input | `:tags: [remove-input]` | `echo=FALSE`|
| Hide code cell output| `:tags: [remove-output` | `results='hide'` |
| Hide code cell input and output | `:tags: [remove-cell]`| `echo=FALSE, results='hide'` |
| Allow an exception and display error | `:tags: [raises-exception]` | `error=TRUE` |

With MyST-NB, using "hide" instead of "remove" will cause content to be hidden, but allow it to be toggled into view. For example, `:tags: [hide-input]`.

### Inline code outputs

MyST Notebooks [use `myst_nb.glue()` to store variables under a text key](https://myst-nb.readthedocs.io/en/latest/use/glue.html), within a code cell:

````markdown
```{code-cell} ipython3
from myst_nb import glue
my_number_variable = 2 + 2
glue("my_number", my_number_variable)
```
````

These keys can then be referenced in markdown content using the glue role:

```markdown
Two plus two equals {glue:}`my_number`.
```

By default, inserted textual content is formatted as inline code (`like this`). [Using `{glue:text}` formats the inserted text in **bold**](https://github.com/executablebooks/MyST-NB/issues/308).


Rmarkdown allows you to evaluate and insert code outputs inline using back ticks with the letter r, for example:

```r
Two plus two equals `r 2 + 2`.
```

Text inserted inline in Rmarkdown inherits the formatting of the surrounding content.

This Rmarkdown syntax can directly reference variables from previous code chunks, while this is [not currently supported in MyST Notebooks](https://github.com/executablebooks/MyST-NB/issues/186).
