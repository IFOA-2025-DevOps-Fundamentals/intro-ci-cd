## Documento Strutturato su GitHub Actions per Corso CI/CD

Questo documento riassume e spiega passo dopo passo i concetti e i passaggi pratici presentati nel video tutorial su GitHub Actions, con l'obiettivo di fornire materiale didattico ben strutturato per un corso su CI/CD di circa 8 ore.

### 1. Introduzione a GitHub Actions

**GitHub Actions è una piattaforma per automatizzare i flussi di lavoro degli sviluppatori software**. Contrariamente a quanto spesso si pensa, non è semplicemente un altro strumento di CI/CD (Continuous Integration/Continuous Delivery). La CI/CD è solo uno dei numerosi flussi di lavoro che è possibile automatizzare con GitHub Actions.

L'obiettivo principale di GitHub Actions è quello di **ridurre le attività manuali, ripetitive e potenzialmente soggette a errori** che i team di sviluppo affrontano quotidianamente. Automatizzando queste attività, gli sviluppatori possono concentrarsi maggiormente sulla programmazione e sullo sviluppo di nuove funzionalità.

### 2. Flussi di Lavoro degli Sviluppatori e Necessità di Automazione

I flussi di lavoro degli sviluppatori comprendono tutte le attività che un team o un singolo sviluppatore svolge durante il ciclo di vita del software. In particolare, per i **progetti open source ospitati su GitHub**, i maintainer si trovano a gestire numerose **attività organizzative**, tra cui:

*   **Gestione delle Issue:** Verifica, classificazione (minor, major, urgente), assegnazione, verifica della riproducibilità.
*   **Gestione delle Pull Request:** Revisione del codice, verifica della risoluzione dell'issue, merge nella branch principale.
*   **Processo di Release:** Avvio di pipeline di build, test e creazione dell'artefatto, preparazione delle note di rilascio, aggiornamento del tag o del numero di versione.
*   **Gestione dei Contributori:** Accoglienza di nuovi contributori.

Queste attività, specialmente in progetti di grandi dimensioni con molti contributori, possono diventare **time-consuming, soggette a errori e tediosi**. L'automazione di queste attività tramite GitHub Actions permette di:

*   **Aumentare l'efficienza:** Ridurre il tempo dedicato a compiti ripetitivi.
*   **Migliorare la qualità:** Standardizzare i processi e ridurre gli errori umani.
*   **Liberare risorse:** Permettere agli sviluppatori di concentrarsi sullo sviluppo.

### 3. Concetti Fondamentali di GitHub Actions

GitHub Actions automatizza i flussi di lavoro tramite l'interazione di tre concetti chiave: **Eventi**, **Azioni** e **Workflow**.

*   **Eventi (Events):** Un evento è **qualcosa che accade nel tuo repository GitHub o che lo riguarda**. Questi eventi possono essere generati da attività degli utenti (ad esempio, la creazione di una pull request, l'apertura di un'issue, il push di codice, il merge di una pull request) o da integrazioni con altri strumenti. **Ogni volta che si verifica un evento configurato, è possibile attivare automaticamente un workflow**. Esiste un elenco completo degli eventi disponibili nella documentazione di GitHub Actions.

*   **Azioni (Actions):** Un'azione è un **singolo compito automatizzato**. Un workflow è composto da una o più azioni. Le azioni possono includere operazioni come:
    *   Scrivere un commento su un'issue o una pull request.
    *   Aggiungere un'etichetta (label) a un'issue.
    *   Assegnare un'issue a un membro del team.
    *   Eseguire test del codice.
    *   Compilare un'applicazione.
    *   Creare e pubblicare artefatti.
    *   Effettuare il deployment di un'applicazione.

    GitHub ospita un marketplace di **azioni pre-create e predefinite** (accessibili tramite `github.com/actions`) che possono essere riutilizzate nei propri workflow. Queste azioni sono repository che contengono codice e un file `action.yml` che definisce la logica dell'azione. È possibile anche utilizzare azioni create dalla community o dal proprio team. Quando si utilizza un'azione, si specifica la sua posizione (solitamente `organizzazione/repository@versione`) tramite l'attributo `uses`.

*   **Workflow:** Un workflow è un **file configurabile (solitamente in formato YAML) che definisce un processo automatizzato**. Un workflow è costituito da uno o più **job**, che a loro volta contengono una sequenza di **step**. Ogni step esegue una singola azione o uno script. I workflow vengono **attivati da uno o più eventi** definiti nel file YAML. I file di workflow vengono memorizzati nella directory `.github/workflows` all'interno del repository.

### 4. CI/CD Pipeline con GitHub Actions

Uno dei flussi di lavoro più comuni che vengono automatizzati con GitHub Actions è la **pipeline di Continuous Integration e Continuous Delivery (CI/CD)**.

**Vantaggi di utilizzare GitHub Actions per la CI/CD:**

*   **Integrazione nativa:** Se il codice è già ospitato su GitHub, è possibile utilizzare lo stesso strumento per la CI/CD, **senza dover configurare e gestire separatamente strumenti di terze parti**.
*   **Facilità di configurazione:** GitHub Actions è progettato per essere **facile da usare anche per gli sviluppatori**, senza la necessità di un team DevOps dedicato alla configurazione e manutenzione della pipeline.
*   **Ampia integrazione con strumenti:** GitHub Actions facilita l'integrazione con diversi strumenti utilizzati nel processo di sviluppo (Node.js, Java, Docker, servizi cloud come AWS, Azure, Google Cloud, ecc.). Invece di configurare manualmente ogni integrazione, è possibile utilizzare azioni pre-esistenti che semplificano notevolmente il processo.

**Semplicità nella creazione di pipeline:**

GitHub Actions offre un'interfaccia utente integrata nel repository GitHub, accessibile tramite la tab **"Actions"**. Qui è possibile trovare una vasta libreria di **workflow templates** preconfigurati per diversi linguaggi di programmazione, framework e scenari di deployment. Questo permette di **non dover partire da zero** nella creazione di un workflow.

### 5. Demo Pratica: Configurazione di una Pipeline CI per un Progetto Java Gradle

La demo presentata nel video mostra come configurare una pipeline CI di base per un progetto Java che utilizza Gradle come sistema di build.

**Passaggi Pratici:**

1.  **Creazione di un Repository:** Viene creato un nuovo repository pubblico su GitHub chiamato "my-project-public".
2.  **Push del Codice Locale:** Il codice di un'applicazione Java Gradle locale viene caricato nel repository remoto.
3.  **Accesso alla Tab "Actions":** Nella pagina principale del repository, si seleziona la tab **"Actions"**.
4.  **Esplorazione dei Workflow Templates:** Nella sezione "Actions", vengono mostrati diversi workflow templates raggruppati per categoria (Deployment, Continuous Integration, Build and test, Publish, ecc.).
5.  **Selezione del Template "Java with Gradle":** Viene scelto il template specifico per progetti Java che utilizzano Gradle.
6.  **Visualizzazione e Modifica del File di Workflow (YAML):** Selezionando il template, GitHub crea automaticamente un file YAML precompilato nella directory `.github/workflows` (ad esempio, con il nome `gradle.yml`). Questo file contiene la logica del workflow.
7.  **Analisi della Sintassi del File YAML:**
    *   **`name`:** Definisce il nome del workflow, che viene visualizzato nell'interfaccia di GitHub Actions.
    *   **`on`:** Specifica gli eventi che attiveranno l'esecuzione del workflow. Nell'esempio, il workflow viene attivato in caso di `push` sulla branch `master` o di creazione di una `pull_request` con la branch target `master`.
    *   **`jobs`:** Definisce uno o più job che verranno eseguiti. Ogni job viene eseguito su un nuovo server virtuale fornito da GitHub.
        *   **`<job_id>` (es. `build`):** Un nome arbitrario per identificare il job.
        *   **`runs-on`:** Specifica il tipo di ambiente (sistema operativo) in cui verrà eseguito il job. Nell'esempio iniziale, è `ubuntu-latest`, indicando l'ultima versione di Ubuntu.
        *   **`steps`:** Una sequenza di azioni che verranno eseguite all'interno del job. Ogni step ha un `name` (opzionale) per descrivere l'azione e può utilizzare `uses` per richiamare un'azione predefinita o `run` per eseguire comandi shell.
            *   **`uses: actions/checkout@v3`:** Utilizza l'azione predefinita `checkout` per scaricare il codice del repository sul server virtuale.
            *   **`uses: actions/setup-java@v3`:** Utilizza l'azione predefinita `setup-java` per configurare l'ambiente Java con la versione specificata (nell'esempio, `java-version: '11'`).
            *   **`run: chmod +x ./gradlew`:** Esegue un comando shell per rendere eseguibile lo script Gradle wrapper.
            *   **`run: ./gradlew build`:** Esegue il comando Gradle per compilare il progetto.
8.  **Commit del File di Workflow:** Il file YAML viene committato nel repository.
9.  **Trigger del Workflow:** Creando una nuova branch, apportando modifiche e aprendo una pull request verso la branch `master`, l'evento `pull_request` definito nel file YAML viene attivato e il workflow inizia la sua esecuzione. È anche possibile attivare il workflow direttamente con un push sulla branch `master`.
10. **Monitoraggio dell'Esecuzione:** Nella tab "Actions", è possibile visualizzare lo stato di esecuzione del workflow (in corso, completato, fallito) e i dettagli di ogni step (log, comandi eseguiti).
11. **Ambiente di Esecuzione:** I workflow su GitHub Actions vengono eseguiti su **server gestiti da GitHub**. Non è necessario configurare o mantenere server propri. Per ogni job all'interno di un workflow, viene **preparato un nuovo server virtuale**.
12. **Esecuzione Parallela di Job:** Per impostazione predefinita, più job definiti in un workflow vengono eseguiti in parallelo. È possibile definire dipendenze tra job utilizzando la parola chiave `needs`.
13. **Scelta del Sistema Operativo:** L'attributo `runs-on` può specificare diversi sistemi operativi forniti da GitHub: `ubuntu-latest`, `windows-latest`, `macos-latest`. È possibile utilizzare una **strategia (strategy) e una matrice (matrix)** per eseguire lo stesso job su più sistemi operativi o con diverse configurazioni (ad esempio, diverse versioni di Java).

### 6. Estensione della Pipeline CI: Build e Push di un'Immagine Docker

Il video mostra come estendere la pipeline CI per **creare un'immagine Docker dell'applicazione Java ePusharla su un repository Docker Hub privato**.

**Passaggi Pratici:**

1.  **Creazione di un Account Docker Hub e di un Repository Privato:** Viene mostrata la creazione di un account gratuito su Docker Hub e la disponibilità di un repository privato gratuito.
2.  **Aggiunta di uno Step per la Build e il Push dell'Immagine Docker:** Viene aggiunto un nuovo step al job `build` nel file YAML.
3.  **Utilizzo di un'Azione Docker Predefinita:** Invece di scrivere manualmente tutti i comandi Docker (`docker login`, `docker build`, `docker tag`, `docker push`), viene utilizzata un'**azione preesistente dal marketplace di GitHub Actions** (nell'esempio, `docker/build-push-action@v4`).
4.  **Configurazione dei Parametri dell'Azione Docker:** L'azione Docker accetta diversi parametri per configurare la build e il push dell'immagine. I parametri importanti includono:
    *   **`registry`:** L'URL del registry Docker (per Docker Hub è `docker.io`).
    *   **`repository`:** Il nome del repository Docker (solitamente `<docker_id>/<repository_name>`).
    *   **`username`:** Il nome utente per l'accesso al registry Docker.
    *   **`password`:** La password per l'accesso al registry Docker.
    *   **`push`:** Un valore booleano per indicare se l'immagine deve essere effettivamente pushata (impostato su `true`).
5.  **Gestione delle Credenziali con GitHub Secrets:** Per evitare di memorizzare credenziali sensibili direttamente nel file YAML, vengono utilizzati i **GitHub Secrets**. I secrets possono essere creati nelle impostazioni del repository (Settings -> Secrets -> Actions) con nomi specifici (ad esempio, `DOCKER_USERNAME` e `DOCKER_PASSWORD`).
6.  **Referenziare i Secrets nel Workflow:** Nel file YAML, le credenziali vengono referenziate utilizzando la sintassi `secrets.<nome_del_secret>` (ad esempio, `secrets.DOCKER_USERNAME`).
7.  **Modifica dell'Attributo `runs-on` (Opzionale):** Poiché Docker è preinstallato sugli agenti Ubuntu forniti da GitHub Actions, l'esempio si concentra sull'utilizzo di `ubuntu-latest` per questo step.
8.  **Commit del File di Workflow Aggiornato:** Le modifiche al file YAML vengono committate.
9.  **Trigger del Workflow Aggiornato:** Un nuovo push sulla branch `master` (nell'esempio, commit diretto) attiva l'esecuzione del workflow aggiornato, che ora include la build e il push dell'immagine Docker.
10. **Verifica su Docker Hub:** Al termine dell'esecuzione del workflow, viene mostrato come verificare che la nuova immagine Docker sia stata effettivamente pushata nel repository Docker Hub privato. L'azione `docker/build-push-action` aggiunge di default un tag all'immagine Docker che include il nome della branch. È possibile personalizzare il tag tramite il parametro `tags` dell'azione.

### 7. Conclusioni e Ulteriori Possibilità

Il video dimostra come GitHub Actions sia uno strumento potente e flessibile per automatizzare non solo pipeline CI di base per la compilazione e il test di applicazioni, ma anche per estendere queste pipeline includendo la containerizzazione con Docker e la pubblicazione di immagini su registry privati.

Il tutorial menziona che GitHub Actions offre molte altre possibilità di automazione, tra cui:

*   Deployment di immagini Docker su ambienti cloud o Kubernetes.
*   Test e build di applicazioni Node.js.
*   Automazione di altri flussi di lavoro di sviluppo.

Questi argomenti potrebbero essere approfonditi in sezioni successive del corso, sfruttando la flessibilità e l'ampia gamma di azioni disponibili in GitHub Actions.

Questo documento fornisce una base solida e strutturata per spiegare i concetti fondamentali e i passaggi pratici introdotti nel video, adatta a un corso su CI/CD. La durata di 8 ore permetterebbe di approfondire ulteriormente ciascun concetto, di eseguire esercizi pratici e di esplorare scenari più avanzati di automazione con GitHub Actions.