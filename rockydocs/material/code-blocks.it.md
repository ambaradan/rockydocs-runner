---
title: Blocchi di codice
---
<!--vale off-->
# Blocchi di codice

I blocchi di codice e gli esempi sono una parte essenziale della documentazione tecnica di un progetto.

## Impostazioni

Per attivare tutte le funzionalità dedicate ai blocchi di codice inserire in *mkdocs.yml* le seguenti estensioni markdown:

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

### Bottone Copia

I blocchi di codice possono visualizzare automaticamente un pulsante sul lato destro per consentire all'utente di copiare il contenuto di un blocco di codice negli appunti. Per la sua abilitazione è richiesta l'opzione:

```yaml title="Copy button"
theme:
  features:
    - content.code.copy
```

### Codice di esempio

Una volta inserite è possibile arricchire un blocco di codice della documentazione con un titolo esplicativo o con la numerazione delle righe o evidenziandone alcune parti o solo alcune funzioni.
Per l'esempio utilizzeremo il seguente blocco di codice:

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

## Titolo del blocco

Tutte le personalizzazioni sono inserite nel tag che identifica il blocco di codice (**\```bash** in questo caso). per prima cosa possiamo aggiungere un titolo al blocco per dare un orientamento al suo contenuto:

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

La stringa da aggiungere all'intestazione del blocco di codice è la seguente:

```text title="Title string"
```bash title="Deactivation function"
```

## Numerazione di linea

Possiamo aggiungere la numerazione di linea per identificare in un esempio un particolare da evidenziare:

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

In questo caso viene utilizzata la chiave `linenums` che indica il numero di partenza della numerazione delle righe, in questo esempio dalla prima:

```text title="Linenums string"
```bash title="Linenums option" linenums="1"
```

La numerazione però è indipendente e ad esempio se vogliamo che la numerazione della parte dello script che si vuole descrivere corrisponda con quella del blocco di codice del documento basta inserire il numero di riga corrispondente in *linenums*.  
In questo caso la stringa diventa `linenums="56"`

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

## Evidenziazione del codice

Possiamo inoltre evidenziare una parte del codice per una descrizione più dettagliata del suo funzionamento:

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

In questo caso è stato evidenziato un "range" di righe, dalla 2 alla 4 mediante l'uso del trattino `-` ma si possono evidenziare anche in maniera indipendente separando le righe con una spazio come nell'esempio successivo:

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

## Codice in linea

Mkdocs-material consente inoltre di evidenziare il codice in linea anteponendo alla funzione, chiamata o altro il marcatore `#!` seguito dal linguaggio da utilizzare. In questo esempio è stato utilizzato il linguaggio bash e di conseguenza il marcatore diventa `#!bash`.

Prendendo ad esempio questa frase:

La routine se la variabile `$VIRTUAL_ENV` è vuota stampa a terminale attraverso un comando di `printf` la stringa `"  no virtual environment is currently active.\\n"`

È possibile trasformarla in:

La routine se la variabile `#!bash $VIRTUAL_ENV` è vuota stampa a terminale attraverso un comando di `#!bash printf` la stringa `#!bash "  no virtual environment is currently active.\\n"`

Il codice markdown per la sua realizzazione è il seguente:

```text
La routine se la variabile `#!bash $VIRTUAL_ENV` è vuota stampa a terminale attraverso un comando di `#!bash printf` la stringa `#!bash "  no virtual environment is currently active.\\n"`
```
