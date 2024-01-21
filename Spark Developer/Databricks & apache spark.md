SPARK: Analytics engine for big data processing

SPark execution -> osserva la strategia divide & conquer
![[Spark execution.png]]ACTION: fa iniziare un processo, spawnano dei job, composti da stage composti da task
TASK: running a memory partition on COre within executor
![[Spark cluster execution.png]]
Ogni worker ha ha un esecutore che ha al suo interno dei core che può eseguire un task, questo processo è gestito automaticamente dal driver

Hive metastore: ???