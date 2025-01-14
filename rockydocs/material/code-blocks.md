---
title: Code Blocks
---
<!--vale off-->
# Code blocks

Code blocks and examples are an essential part of a project's technical documentation.

To enable all features dedicated to code blocks, insert the following markdown extensions in *mkdocs.yml*:

```yaml title="code blocks settings"
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
```

Once entered, it is possible to enrich a block of documentation code with an explanatory title or line numbering or by highlighting certain parts or only certain functions.
We will use the following block of code for the example:

````bash
```bash
# function to deactivate the virtual environment if active
deactivate_venv() {
    if [[ "$VIRTUAL_ENV" != "" ]]; then # check system variable
        deactivate
        printf "  deactivated the virtual environment.\\n"
    else
        printf "  no virtual environment is currently active.\\n"
    fi
    }
```
````

All customizations are placed in the tag that identifies the code block (**\```bash** in this case). first we can add a title to the block to give orientation to its content:

```bash title="Deactivation function"
# function to deactivate the virtual environment if active
deactivate_venv() {
    if [[ "$VIRTUAL_ENV" != "" ]]; then # check system variable
        deactivate
        printf "  deactivated the virtual environment.\\n"
    else
        printf "  no virtual environment is currently active.\\n"
    fi
    }
```

The string to be added to the header of the code block is as follows:

```text title="Title string"
```bash title="Deactivation function"
```

We can add line numbering to identify in an example a detail to be highlighted:

```bash title="Linenums option" linenums="1"
# function to deactivate the virtual environment if active
deactivate_venv() {
    if [[ "$VIRTUAL_ENV" != "" ]]; then # check system variable
        deactivate
        printf "  deactivated the virtual environment.\\n"
    else
        printf "  no virtual environment is currently active.\\n"
    fi
    }
```

In this case the `linenums` key is used, which indicates the starting number of the row numbering, in this example from the first:

```text title="Linenums string"
```bash title="Linenums option" linenums="1"
```

The numbering, however, is independent, and for example, if we want the numbering of the part of the script we want to describe to match the numbering of the code block in the document, we need only enter the corresponding line number in *linenums*.  
In this case the string becomes `linenums="56"`

```bash title="Linenums option" linenums="56"
# function to deactivate the virtual environment if active
deactivate_venv() {
    if [[ "$VIRTUAL_ENV" != "" ]]; then # check system variable
        deactivate
        printf "  deactivated the virtual environment.\\n"
    else
        printf "  no virtual environment is currently active.\\n"
    fi
    }
```

We can also highlight a part of the code for a more detailed description of its operation:

```bash title="hl_lines option" linenums="56" hl_lines="2-4"
# function to deactivate the virtual environment if active
deactivate_venv() {
    if [[ "$VIRTUAL_ENV" != "" ]]; then # check system variable
        deactivate
        printf "  deactivated the virtual environment.\\n"
    else
        printf "  no virtual environment is currently active.\\n"
    fi
    }
```

```text title="hl_lines string"
```bash title="Linenums option" linenums="56" hl_lines="2-4"
```

In this case a "range" of rows was highlighted, from 2 to 4 through the use of the dash `-` but they can also be highlighted separately by separating the rows with a space as in the following example:

```bash title="hl_lines option" linenums="56" hl_lines="5 7"
# function to deactivate the virtual environment if active
deactivate_venv() {
    if [[ "$VIRTUAL_ENV" != "" ]]; then # check system variable
        deactivate
        printf "  deactivated the virtual environment.\\n"
    else
        printf "  no virtual environment is currently active.\\n"
    fi
    }
```

```text title="hl_lines string"
```bash title="Linenums option" linenums="56" hl_lines="5 7"
```

Mkdocs-material also allows inline code to be highlighted by placing the marker `#!` followed by the language to be used in front of the function, call or otherwise. In this example, the bash language was used and consequently the marker becomes `#!bash`.

Taking this sentence as an example:

The routine if the variable `$VIRTUAL_ENV` is empty prints to terminal through a `printf` command the string `" no virtual environment is currently active.\n"`

It is possible to turn it into:

The routine if the variable `#!bash $VIRTUAL_ENV` is empty prints to terminal through a command of `#!bash printf` the string `#!bash " no virtual environment is currently active.\n"`

The markdown code for its implementation is as follows:

```text
The routine if the variable `#!bash $VIRTUAL_ENV` is empty prints to terminal through a command of `#!bash printf` the string `#!bash " no virtual environment is currently active.\n"`
```
