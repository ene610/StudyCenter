## Intro
SPARK: Analytics engine for big data processing

SPark execution -> osserva la strategia divide & conquer
![[Spark execution.png]]ACTION: fa iniziare un processo, spawnano dei job, composti da stage composti da task
TASK: running a memory partition on COre within executor
![[Spark cluster execution.png]]
Ogni worker ha ha un esecutore che ha al suo interno dei core che può eseguire un task, questo processo è gestito automaticamente dal driver

Hive metastore: ???

## Functions

[TODO] cancellato per errore
### GroupBy
aaa
### Datetime
aaa
### UDF
aaa

## Architettura & Performance

Trasformation

![[narrow vs wide.png]]

Narrow: può agire direttamente nella propria partizione 
Wide: necessita la ridistribuzione dei dati tra le nuove partizioni

#### Narrow trasformation


![[filter as narrow trasformation.png]]
![[filter as narrow transformation 2.png]]
![[narrow trasformation 1.png]]
![[narrow trasformation 2.png]]![[narrow trasformation 3.png]]
![[narrow trasformation 4.png]]
![[narrow trasformation 5.png]]

#### Wide trasfromation

![[wide 1.png]]

![[wide 2.png]]

![[wide trasformation 1.png]]
la shuffle write è minore in byte rispetto all'input perchè si calcolano i parziali nel primo stage 

![[wide 3.png]]

![[wide trasformation 2.png]]

![[wide trasformation 3.png]]

![[wide trasformation 4.png]]

![[wide trasformation 5.png]]

#### Query optimization

![[Query optimization.png]]

in blu ci sono a quali domande rispondono i vari step

![[explain functions.png]]

COST BASE OPTIMIZATION



![[wide trasformation 6.png]]

#### Query optimization AQE

![[Query optimization AQE.png]]

![[Query optimization AQE with and without.png]]

Con AQE il numero di job incrementa ma diminuiscono il numero di shuffle.

**predicate pushdown** : 

#### Cache
- NON cache se non si usa il dataframe almeno due volte
- ometti sempre le colonne che non usi 
- Ricorda che cache è una lazy trasformation, quindi dopo che richiami cache usa un'action per persistere
- quando non ti serve più fai unpersist

#### Memory partitioning

se le memory partition sono piccole allora si incoorre nel fenomeno di memory spilling (svuoti i dati in memoria centrale) 

si possono settare il numero di shuffle partition (di default sono 200)
**RICORDA AQE può risolvere partition issues**

coalesce(int) return dataframe con esattamente N partition [...]
repartition(int, [coll]) return new DF con esattamente N partition
#### alfa

## Structured Streaming

(28-01-24) IMPORTANTE AQE Query Optimization non funzione su streaming, il numero di partizioni va definito a mano

### Streaming Query

![[batch vs streaming.png]]

bisogna tenere in considerazione quanta latency posso accettare e quanto sono disposto a pagare

![[pro structured streaming.png]]

uno dei vantaggi proncipali del processamento streaming è la possibilità di lavorare solo sui dati nuovi.

![[micro-batch processing.png]]
In Spark, i dati sono processati in Micro-batch, ovvero ad ogni intervallo di trigger abbiamo una esecuzione. 

Abbiamo 3 possibili modalità di output
![[Output modes.png]]

![[trigger type.png]]

---

In structured streaming, la tollerance End to End è garantita da:

- **Checkpointing**: DAG di tutte le DStream trasformation , memorizzate in uno storage affidabile.
- **Write-ahead logs**: to commit offsets (descrivi offset )
- **Idempotent sinks**: il dato viene scritto una sola volta anche a fronte di molte scritture
- **Replayable data source**: Job allowed to poll data again

![[Best pratice streaiming.png]]
### Streaming Aggregation

in streaming possiamo aggregare i dati solo per una ben definita finestra temporale un insieme di micro batch.

- **Tumbling windows**: ogni evento viene aggregato in una finestra temporale (1:00-1:10 am/ 1:10-1:20 am)
- **Sliding windows** (in Azure è segnato come hopping): ogni evento viene aggregato in una finestra temporale (1:00-1:10 am/ 1:05-1:15 am)
- **Session windows**: (Da fare)

![[sliding window example.png]]
#### Windowing & watermarking

Voglio processare processare in base al tempo del evento ma non in base nel tempo di ricezione. come gestisto i dati che sono arrivati tardi (per esempio perchè si è disconesso il device)? con watermark!

![[event-time processing.png]]

nel caso di sotto va bene processare il dato perchè è all'interno della watermark (impostata a 2h)
![[handling data with watermarking.png]]

## Delta lake

Delta lake è uno strato del delta lakehouse platform che definisce il protocollo di lettura e scrittura sdei file su cloud storage, in questo modo si ottengono i benefici sia di architettura data lake che di quelle data warehouse.

![[architettura delta lakehouse.png]]

uno dei benifici è l'abilitazione di transazioni ACID in spark, Time travel, schema evolution (non lanciare fail se lo schema differisce da quello ricevuto prima).

Le componenti di un delta lake sono:
- **Delta lake storage layer**: dove risiedono i dati, deve essere su un cloud storage (Azure, GPC, AWS)
- **Delta table**: suddiviso ulteriormente in due ulteriori componenti
	- Parquet: il è posto dove contente i dati
	- Transaction logs: il log che tiene traccia tutte le transazioni effettuate sul parquet. all'interno ci sono file dei json e  dei crc file, creati 1 per ogni operazione. ogni Json descrive òìoperazione mentre i crc contengono i metadati relativi a quel operazione. 
- **Delta engine**: tratta tutte le ottimizzazioni. queste comprendono
	- file management optimization
	- auto-optimized writes
	- performance optimization via Delta Disk caching (Data skipping, Z-ordering, etc..)

## FINE