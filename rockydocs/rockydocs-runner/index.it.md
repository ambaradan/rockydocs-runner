<!--vale off-->

# Material runner

## Introduzione

Il progetto nasce dalla necessità di avere a disposizione una anteprima *reale* del risultato del codice markdown "Material Flavoured".  
Il plugin **mkdocs-material** per il generatore di documentazione *MkDocs* oltre a gestire l'aspetto grafico del sito introduce molti tag markdown non standard che consentono ulteriori personalizzazioni per la formattazione dei contenuti.  
Questi tag ovviamente non vengono interpretati nei plugin comuni per l'anteprima dei documenti markdown e per visualizzarli correttamente è indispensabile una istanza di MkDocs in esecuzione con il plugin mkdocs-material installato.
Questo progetto intende fornire una soluzione automatizzata al problema, mediante l'inserimento (source) di una serie di funzioni e di un menù è possibile gestire tutti gli aspetti della creazione, installazione e avvio di un ambiente virtuale Python dove è possibile verificare la correttezza del codice scritto.

## Installazione

NOTA: Per la sua installazione di esempio utilizziamo una cartella `lab` presente nella home dell'utente, adattare le istruzioni secondo esigenza se si intende utilizzare un altro percorso.

Per prima cosa clonare il repository:

```bash
git clone https://github.com/ambaradan/material-run.git ~/lab/material-run
```

All'interno della cartella appena clonata troviamo due file, mkdocs.yml e run. Il primo è il file di configurazione di MkDocs che verrà utilizzato nella fase finale della installazione (avvio di 'mkdocs serve') mentre il secondo è lo script che contiene tutte le funzioni e il menù necessari alla gestione della istanza **python venv + mkdocs + material**.  
Viene inoltre fornito un file *.gitignore* che nasconde eventuali installazioni `.venv` e collegamenti `docs` presenti localmente.

NOTA: Lo script come detto in precedenza deve essere inserito (sourced) in bash e non eseguito per funzionare correttamente ed è presente un controllo per evitare che questo accada.

Portarsi quindi nella cartella clonata ed eseguire il source:

```bash
cd ~/lab/material-run
source run
```

```text
  Installed Python version: Python 3.9.21
  .venv directory is missing.

  Select an option:
       1. Create a new virtual environment
       2. Install mkdocs-material
       3. Create a symbolic link to an external docs folder
       4. Activate the virtual environment and run mkdocs serve
       5. Exit
  Enter your choice [1-5]: 
```

### Creazione dell'ambiente virtuale

Per prima cosa è necessario creare l'ambiente virtuale (opzione 1) dove installare MkDocs e il plugin mkdocs-material. La creazione di un ambiente python separato dall'installazione di sistema permette di eseguire mkdocs senza interferire con l'installazione globale. Per la sua realizzazione è utilizzato il plugin venv che si occupa in maniera del tutto automatica della sua creazione. Una volta terminata la copia dei file necessari viene emesso un messaggio di conferma e una verifica di eventuali ambienti attivi.

```text
  Creating a new virtual environment...
  Virtual environment created successfully.
  No virtual environment is currently active.
```

### Installazione mkdocs-material

Creato l'ambiente è il momento di installare i pacchetti necessari (opzione 2) , lo script si occupa di controllare, ed eventualmente aggiornare pip (il plugin manager di python) e di scaricare ed installare tutti i plugin richiesti.

```text
  Activated the virtual environment.
  ...
  ...
  mkdocs-material installed successfully.
  Deactivated the virtual environment.
```

### Collegamento cartella docs

L'ambiente per visualizzare l'anteprima del codice markdown scritto per il "material flavour" è ora completo e quello che manca è una cartella con i contenuti da visualizzare. È necessario creare un collegamento simbolico (opzione 3) alla cartella `docs` che MkDocs utilizzerà per il parsing dei file.
Il progetto fornisce una cartella `material-docs` con esempi e spiegazioni dei tag utilizzati da mkdocs-material per la visualizzazione arricchita del codice markdown, per iniziare si può collegare la cartella di esempio.

```text
  Enter the path of the external folder to link: material-docs/
  Removed old symbolic link 'docs'.
  Symbolic link 'docs' created pointing to 'material-docs/'.
```

NOTA: lo script fornisce la funzione di auto completamento ma non l'uso delle variabili d'ambiente (`~` e `$HOME`) per la costruzione del percorso.

### Esecuzione di MkDocs serve

Ora è tutto pronto per visualizzare l'anteprima dei contenuti (opzione 5) della cartella `docs` nel browser, verrà attivato l'ambiente virtuale python ed eseguito `mkdocs serve`. L'istanza di MkDocs utilizza per la sua configurazione il file mkdocs.yml, presente nella cartella, preparato all'occorrenza con tutte le estensioni richieste.  
Aprire il browser preferito all'indirizzo `http://127.0.0.1:8000/` e sarà possibile visualizzare quello che mkdocs-material può fare per arricchire e particolareggiare la documentazione scritta con il supporto di questo plugin.

```text
  Activated the virtual environment.
  Starting mkdocs serve...
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.32 seconds
INFO    -  [15:09:22] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [15:09:22] Serving on http://127.0.0.1:8000/
```

Terminati i test per chiudere l'istanza di MkDocs digitare `Ctrl + C`

```text
^CINFO    -  Shutting down...
  Deactivated the virtual environment.
```

## Uso regolare

Il progetto è stato pensato per scrivere principalmente documentazione per Rocky Linux che utilizza questo plugin nella configurazione di MkDocs ma può essere usata per qualsiasi documentazione che utilizzi il codice standard.
Per usarlo per la propria documentazione è sufficiente sostituire il collegamento alla cartella `docs`, utilizzando l'opzione 3 del menu, collegandola a quella che si sta utilizzando per lo sviluppo. Avviando nuovamente MkDocs (opzione 4) si avrà questa volta all'indirizzo sopra citato l'anteprima della vostra documentazione.

NOTA: Il motore MkDocs controlla costantemente le modifiche ai file contenuti nella cartella `docs` permettendo così di avere in tempo reale la visualizzazione del documento finale, in questo modo tutte le modifiche fatte al file markdown verranno immediatamente rese disponibili per la loro visualizzazione.

## Conclusioni

L'intero sviluppo si svolge in un ambiente separato ed indipendente che consente una esecuzione senza interferenze, è stato pensato per essere uno strumento da affiancare al proprio editor preferito per lo sviluppo di documentazione Rocky fornendo le estensioni proprie dell'editor senza le altre funzionalità del sito di documentazione (supporto multilingua, revisione git e altro), che lo rendono particolarmente pesante da processare.
