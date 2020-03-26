# CWL Format

![Tests](https://github.com/rabix/cwl-format/workflows/Tests/badge.svg)

CWL Format is a specification and a reference implementation for
a very opinionated CWL code formatter.

It outputs CWL in a standardized YAML format. It has no settings or
options because you have better things to do with your time. And because
CWL Format is always correct.

This repository lists the formatting rules and also contains a Python
implementation of the formatter.

```
pip install cwlformat
cwl-format unformatted.cwl > formatted.cwl
```

Use programmatically in Python by doing

```python

from cwlformat.formatter import cwl_format

formatted_text = cwl_format(unformatted_text)
```


## Rules

- Only comment lines at the top of the file, including blank lines,
  before the actual CWL code are preserved. All other comments are lost.
  **Do not use this if all comments in the YAML are important to you**. 

- All CWL fields are ordered systematically. The field order for specific 
  fields have a defined precedence ("pinned fields"). Any fields not 
  present in this file ("free fields") are printed after the pinned fields 
  and ordered alphabetically.

- The pinned fields are defined in [this YAML file][spec]. 

- Specific pinned field orderings are available for CommandLineTool, 
  ExpressionTool and Workflow processes. All other types follow a generic
  pinned field list.
 
- All strings that fit within 80 columns are expressed in flow style.
  Longer strings or strings with new lines are expressed in block style.

- All lists and maps are expressed in block style

- The ordering of all lists are preserved

- Indentation is 2 spaces, including for lists

[spec]: https://raw.githubusercontent.com/rabix/cwl-format/master/cwlformat/keyorder.yml

## Conformance tests

A series of documents are found in the [`tests`][tests] directory that can be used
to check correctness of a formatter. The files named `original-*` are the input files
and the files named `formatted-*` are the corresponding formatted documents. There
are a mixture of YAML and JSON input files. Formatted files are always YAML.

[tests]: https://github.com/rabix/cwl-format/tree/master/tests/cwl
