# .

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
# Scaffolding progetto

## Se creo prima repo

- clona la repo dentro cartella esercizi
- apro la cartella in vs code
- digitare:
  ```sh
    npm create vue@latest
  ``` 
  alla prima domanda sul nome del progetto mettere un punto ad indicare che il progetto è quello della cartella corrente

  alla seconda domanda 'pacckage-name' inserire il nome del progetto ovvero lo stesso nome della repo

  proseguire rspondndo sempre no

- digitare:
    ```sh
        npm install
    ```
- per controllare che tutto funziona far partire il server
    ```sh
        npm run dev
    ```
- per arrestare il server:
```sh
        ctrl + c
``` 


## Se creo prima progetto

- apro la cartella degli esercizi in vs  code
- digitare:
  ```sh
    npm create vue@latest
  ``` 
  alla prima domanda sul nome del progetto mettere il nome della repo

  proseguire rspondendo sempre no

  mi porto dentro la cartella creata:
  ```sh
        cd  nome repo
        code . -r
    ```
- digitare:
    ```sh
        npm install
    ```
- per controllare che tutto funziona far partire il server
    ```sh
        npm run dev
    ```
- per arrestare il server:
```sh
        ctrl + c
``` 

Se tutto funziona pusho su github

## Pulizia dello scaffolding

- Apro App.vue e cancello tutto e scrivo il mio codice in modalità 'options'
- Apro la cartella components e la svuoto
- Apro la cartella assets svuoto tutto tranne main.css
- Cancello tutto il contenuto del main.css e lo rinomino in main.scss
- creo in assets le cartelle images e styles
- sposto dentro la cartella styles main.scss
- aggiorno il path a main.scss in main.js
- aggiungo eventuale cartella immagini a public
- aggiungo dentro la cartella styles una cartella partials per i file partial scss (es. varibili, animazioni, mixins, ecc) 


## Installare dipendenze

```sh
       npm install -D sass
``` 

```sh
       npm install bootstrap axios @fortawesome/fontawesome-free
``` 

- importo bootstrap dentro main.scss @import 'bootstrap/scss/bootstrap';

## Esercizio di oggi: Vite Yu-Gi-Oh
- nome repo: vite-yu-gi-oh
- # Descrizione:
- Create un nuovo progetto utilizzando Vite e Vue 3 e definite i componenti necessari per strutturare il layout come da screenshot allegato.
- Al caricamento della pagina, effettuate una chiama ajax all'API di Yu Gi Oh: https://db.ygoprodeck.com/api/v7/cardinfo.php
e con i dati restituiti, stampate una card per ogni carta.
- **ATTENZIONE**: l’api restituisce tutti i risultati in un colpo solo. Per evitare attese e/o rallentamenti nelle richieste, potete diminuire il numero di risultati sfruttando i parametri *num* e *offset*
- https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0
- **Bonus:**
Creare un componente loader da visualizzare fintantoché i risultati non sono pronti.

# Documentazione API per esercizio : 
https://ygoprodeck.com/api-guide/