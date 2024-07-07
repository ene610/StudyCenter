cluster: group of computers che comunicano tra di loro (nodi)
Spark è veloce perchè distribuisce l'esecuzione tra i nodi
Distribuited computing significa più potenza ma maggiore complessità (Debugging non è facile)

# Understanding the Spark Cluster
## Cluster components

![[Cluster architecture.png]]

**Driver**: è il guidatore degli esecutori, contiene il codice e delega i compiti agli esecutori 
**Esecutori**: esegue i compiti, più esecutori abbiamo più possiamo dividere i compiti
**Cluster manager**: è il responsabile della gestione del cluster e mette in collegamento gli esecutori con il driver. Quando il driver decide cosa deve esser fatto e come, richiede le risorse al cluster manager che riserverà un numero di esecutori in base al workload.
**Spark session**: inizializzato da un driver rappresenta il punto di contatto con un workload. rappresenta l'interfaccia con cui il driver comunica con un cluster.

![[Cluster components.png]]

Quando un driver ha necessità di eseguire un workload allora richiede al cluster manager le risorse necessarie. Il Cluster manager allora alloca gli esecutori allo specifico workload. 

Spark session e esecutori si scambiano dati, se dobbiamo fare un operazione in una tabella questa viene inviata in parti a 1 o più esecutori. quando gli esecutori hanno finito con i calcoli questi inviano i risultati al driver. Anche gli esecutori tra di loro si scambiano i dati in base alle esecuzioni che devono completare.

Questa suddivisone non è fisica ma virtuale. un worker node può contenere più esecutori.



**Executors**

![[Executors.png]]

Un worker node ha 1 o più executors (tipicamente 1) che non è un programma runnato in una JVM, viene creato quando l'applicazione spark viene iniziata e appartiene a una specifica applicazione. Un executor può lavorare sia in sequenza che in parallelo in base alla configurazione. Un executors è de-commissionato quando finisce l'applicazione Spark oppure quando va in failure.

**Dynamic Resource allocation**

Se attivata, permette di bilanciare il numero di executors in base al carico di lavoro, ottimizzando le performance in scenari in cui il carico di lavoro varia nel tempo.
Quando è attivata , Spark osserva il carico che deve essere eseguito e crea un numero di esecutori esponenziale (1,2,4,8) in base al carico di lavoro rimanente per poi rimuovere automaticamente quelli che rimangono in idle.

## Execution modes

(Spark's execution/deployment mode determines where the driver and executors are physically located when a Spark application is run)
descrive l'infrastruttura computazionale usata da spark, in particolare, il network e i nodi.
(deployement mode vs execution mode spesso sono la stessa cosa).

- **Local mode**: tutte le componenti sono eseguite in una singola JVM. driver, executor e "cluster manager" sono eseguiti sulla stessa macchina per testing purpose. Il cluster manager non fa molto poichè le risorse si trovano tutte in un punto.![[Local mode.png]]
- **Standlone mode**: le componenti girano su un singolo cluster. Il cluster manager e il driver possono girare su un nodo in cui gira già un esecutore.![[Standlone mode.png]]
- **Client mode**: Il driver (edge node) è eseguito al di fuori del cluster, il cluster manager è eseguito su un nodo a parte.![[Client mode.png]]
- **Cluster mode:** il driver viene eseguito all'interno del cluster in un nodo dedicato.![[Cluster mode.png]]


# Spark Data APIs
# The Power of Partitions

### Panoramica introduttiva
partitions è la motivazione delle performance in spark è legata all'utilizzo delle partitions

una partitions non è altro che un pezzo di dati, pensa a data frame, questo è splittato in tante partizioni (1 o +). Di default, un esecutore può processare una partizione ma attraverso la modifica dei settings può processarne di più. 

![[Parallelismo in spark.png]]

nel caso ci siano più partizioni che esecutori allora bisognerà attendere che un esecutore si libera, creando una inefficienza (bisognerà aspettare la fine di un esecutore e successivamente gli esecutori senza partizioni da calcolare rimarranno idle).

![[Limits of parallel processing.png]]

Ci sono diversi meccanismi di partizionamento:
- HASH: si splitta in base a un valore discreto
- RANGE: si splitta in base a valori continui
- ROUND ROBIN
- SINGLE

![[Hash Partition.png]]

La grandezza delle partizioni o la loro numerosità è fissa e definita nelle configurazioni di spark, l'importante è che le partizioni siano di una dimensione tale per cui possano rientrare nella memoria degli esecutori. (TODO cosa succede in caso contrario?)

### Shuffle

La shuffle è l'operazione di scambiare i dati tra esecutori durante una esecuzione, sono le operazioni più pesanti, quindi cerchiamo di evitarle. Per farlo gli esecutori sono costretti a scrivere i dati, abbiamo due tipi di shuffle:
 - full shuffle: tutti i dati sono coinvolti 
 - partial shuffle: solo alcuni dati sono coinvolti

le motivazioni perchè faccciamo delle shuffle sono per lo più due: 
- comparazione di dati tra le partizioni (sorting data, grouping & aggregating) 
- forzata (repartition)

### Data skew

Per data skew intendiamo il fenomeno per cui le partizioni hanno una dimensioni diverse, gli executor potrebbero mantenere in stallo esecutori che invece hanno completato.

i sintomi di data skew possono essere ricondotti a 3:
- slow-running workloads
- underutilization of resources: perchè gli esecutori sono fermi
- Out-of-memory error: quando un esecutore cade perchè non ha la memoria necessaria per 

per evitare i data skew si può utilizzare una o più colonne come chiave che abbiano una cardinalità alta e nessun valore nullo.

#### Salting
è il processo di creazione artificiale di una chiave in grado di evitare gli out of memory errors (Group by column + random number)

![[Salting.png]]

### Spark config per le partitions

spark.sql.files.maxPartitionBytes: definisce il numero di byte per partition
spark.sql.shuffle.partitions: definsice il numero di partizioni RISULTANTI dalle operazioni (TIPO JOIN) [RIVEDI]
spark.default.parallelism:  [RIVEDI]


# Executor Memory management

### Storage layout

![[Executor Memory Layout.png]]

- Execution: memorizza i dati per i task (shuffle & joins) 
- Storage: memorizza i dati in cache
- User: memorizza le qui le UDF
- Reserved: memorizza gli oggetti
Off-heap
- Execution
- Storage
Overhead
Pyspark Memory

In generale non c'è un confine tra storage & execution e questo permette di usare la memoria in modo più efficente (nello schema è tratteggiato il confine). La priorità sulla memoria comune è per la parte di execution.

![[On-Heap vs Off-heap.png]]

La prima differenza è tra on-Heap e off-heap, di default è disabilitata off-heap ma può essere utile in contesti in cui i dati devono esser condivisi con applicazioni al di fuori della Spark application oppure quando il JVM Garbage collector rallenta le operazioni che avvengono nellal parte on-heap

![[Spark configuration memory.png]]
#### Data serialization/desirialization

Serialization/Deserizalizarion è il processo di comprimere/decomprimere i dati in modo da inviare i dati in modo veloce agli altri nodi di un cluster 

![[Data storage comparison.png]]

### Caching & Storage levels

Caching significa persistere i dati nel esecutore. utile quando devi usare dati o risultati frequnetemente, affinchè i dati sono disponibili se richiesti nuovamente.
i dati sono memorizzati in diversi Storage levels:

![[Caching & storage levels.png]]

Nel caso del memory level "Memory only" i dati sono salvati in cache, permettendo un più veloce accesso mentre nel caso di "Memory And Disk" i dati sono salvati in prima battuta sulla cache, quelli che eccedono la memoria sono salvati sul disco del executor.

![[Caching eviction.png]]

In scala invece possono essere salvati anche in formato serializzato, in pyspark non è possbili scegliere questa opzione (sono sempre serializzati).
![[Code4Caching.png]]

### Partition functions

**repartition** e **coalesce** sono le funzioni che partizionamento il dataframe.
La differenza tra le due funzioni sono:

- repartition incrementa e diminuisce le partizioni, coalesce riduce il numero di partizioni
- repartition è una wide trasformation (causa una shuffle), coalesce è una narrow transformation, repartition è più lenta della coalesce
- repartition distribuisce bene i dati rispetto a una coalesce, che può risultare in una data skew

se usiamo coalesce(8) da un dataframe con 4 partizioni, il comando non ritorna errore ma non cambia il numero di partizioni.

Se invece invece vogliamo partizionare per colonna usiamo **df.repartition(4, "colonna")**

### Memory in action
(TODO!)

# Actions vs Trasformation
### Overview

Actions triggera l'esecuzione di un esecutore. si distinguono in :
- view data - tipo display, head, tail
- collect data - tipo collect()
- write
trasformation sono operazioni lazily evaluation, sono eseguite solo se seguite da un azione. si distinguono in:
- narrow: i dati non si spostano dal esecutore (Esempio  select)
- wide: bisogna fare una shuffle e i dati 

![[Narrow vs wide Transformation.png]]

![[Mappa azioni, trasformazioni.png]]

# Execution Hierarchy
Rappresenta la struttura con cui rappresentare i workload

![[Execution hierarchy.png]]
![[Execution hierarchy schema 2.png]]
![[Execution hierarchy schema.png]]
La gerarchia di esecuzione è descritta come:
- **Jobs**: Generato da una singola action (se ha la capacità altrimenti piuù job)
- **Stage**: insieme di tasks che possono essere eseguite in parallelo, tra uno stage e un altro abbiamo una shuffle
- **Task**: processa una singola partizione   

Inoltre ci sono gli Slot, ovvero, l'unita di processamento un singolo task, fa parte degli esecutori. Generalmente sono 1 slot per core/threads.
Application è la parte in cui i job vengono creati

# Code Execution

# Cross-Cluster Communication

### Accumulators & broadcast variables
Accumulators variable servono per somme e row wise counting.
ci sono 2 tipi di accumulators:
- Unamed: 
- Named:

Broadscast variable servono per distribuire dei dati su tutti gli esecutori in un cluster, utile se la tabella è piccola e utilizzata in una join con una tabella più grande. La distribuzione non avviene direttamente dal driver node ma data ad alcuni esecutori che distribuiranno a loro volta la tabella in una forma di P2P. l'importante e che le broadcast variables possano entrare in memoria degli esecutori 

![[Broadcast variables.png]]

### Join

![[Tipi di join.png]]
### AAAA