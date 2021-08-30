---
title: Reproducible Reports in Python
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Reproducible Reports in Python

This is a Markdown document, written using the Markedly Structured Text (MyST) flavour. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. See the documentation for [more details on using MyST](https://myst-parser.readthedocs.io/en/latest/syntax/syntax.html).

## Building

This example [uses `sphinx` to build HTML from the document](https://myst-parser.readthedocs.io/en/latest/sphinx/intro.html). To build the document, run `make html` from the root of the project.

## Embedding code and outputs

When you build with `sphinx`, HTML will be generated that includes both content as well as the output of any embedded code chunks within the document. You can embed a Python code cell like this:

```{code-cell} ipython3
import numpy as np
import pandas as pd

some_data = pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]),
                   columns=['a', 'b', 'c'])
some_data
```

When building, the `jupytext` library converts this to a notebook for execution. As with notebook outputs, dataframes are displayed here as tables.

You can dynamically insert, or `glue`, variables from code into content:

```{code-cell} ipython3
from myst_nb import glue
my_variable = "here is some text!"
glue("glued_text", my_variable)
```

Here is an example using `glue` to insert text into content: {glue:text}`glued_text`

Glueing can more generally be used to store any code output and then insert it within the documents content.

You can also embed plots, for example:

```{code-cell} ipython3
:tags: [remove-input]

from matplotlib import pyplot as plt
%matplotlib inline
some_data["a"].plot()
plt.show()
```

Note that the the code cell tag `remove-input` was added to prevent printing the code input for this cell.

## Executable code

Static tables and plots are shown here, however, it's also possible to [embed executable and interactive content in documents using Jupyter Book](https://jupyterbook.org/interactive/interactive.html).
