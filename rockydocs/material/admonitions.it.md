---
title: Admonitions
---
<!--vale off-->
# Admonitions

## Introduzione

I suggerimenti, le note e le avvertenze sono blocchi di testo formattati per fornire suggerimenti utili, evidenziare potenziali problemi e informare i lettori sulle conseguenze critiche, sono stati concepiti per includere contenuti aggiuntivi cercando di fare in modo che questi non interrompano il flusso della lettura. Il plugin mkdocs-material offre diversi tipi di ammonimenti e permette di includere e annidare al loro interno ulteriori contenuti arbitrari.

## Impostazioni

Per abilitare gli ammonimenti, permettere di renderli richiudibili e di annidarne i contenuti al suo interno è necessario aggiungere le seguenti estensioni a *mkdocs.yml*:

```yaml title="Admonitions setting"
markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
```

Gli ammonimenti hanno una sintassi semplice, il blocco che lo identifica inizia con tre punti esclamativi seguiti da una singola parola chiave che ne determina le caratteristiche. Segue una riga vuota e nella seguente il contenuto dell'ammonimento indentato di quattro spazi.

```text title="Admonitions schema"
!!! note

    Contenuto dell'ammonimento indentato di quattro spazi. L'indentazione 
    come la spaziatura con una riga vuota sono necessari per una corretta
    visualizzazione.
```

!!! note

    Contenuto dell'ammonimento indentato di quattro spazi. L'indentazione come la spaziatura con una riga vuota sono necessari per una corretta visualizzazione.
