## Parametry uruchomieniowe<br/>
- spark.ui.enabled: "true"  - pwoinno sie uruchamiac sporadycznie tylko do testow lub debug <br/>
- spark.executor.instances: 4 - liczba executorow do wykonania zadania , ilosc zbiorow (cpu i pamieci)<br/>
- spark.executor.cores: 4<br/>
- spark.executor.memory: "4G"<br/>
- spark.driver.memory: "8G"<br/>

Jezli mamy 32 taski i 16 core = 2 cykle zostana wykonane<br/>
Zmiana z 30GB na 60GB nic nie zmieni<br/>

Tylko zmiana core z 4 na 8 w 4 intancjach daje 32 - szybciej sie juz nie da <br/>
Jezeli w tym ukladzie 32 zadania 32 cory zaczynaj czkac to znaczy ze ilosc danych jest wieksza niz przydzielona pamiec <br/>
Jezeli moj dataset na jednej partycji ma wiecej niz 4G - to zacznie swapowac spearowac - jak zacznie zapisywac na dysk to wtedy zwolni wykonanie<br/>
I wtedy dokladamy RAMu zeby uniknac zrzucania danych na dysk <br/>
Jezeli jest wysoka wartosc na driverze - tzn ze dokonujecie obliczenia na driverze a nie do tego driver sluzy <br/>
Tzn ze cos robicie w pythonie co jest rozproszone <br/>

Np jezeli w Pythonie uzywamy Pandas to dzialamy na driverze w tym przypadku od razu bedzie widac przez brak jobow <br/>
1 - zwiekszyc RAM lub przypisac szybsze procek<br/>
2 - przerzucic obliczenia na executory a nie drivery (a jezeli sie upierasz ze przeslanie tego executory zajmie wiecej czasu to ok Twoja sprawa jak jestes zadowolony)<br/>

DOdatkowo przepelniona pamiec bedzie powodowala czestsze uruchamianie i czyszczenie GC <br/>

Driver zwykle jest mniejszy niz executiry <br/>

Jak włączyć wyższy poziom logowania pyspark <br/>

[Jacek SPark Query](https://jaceklaskowski.github.io/spark-workshop/slides/spark-sql-internals-of-structured-query-execution.html#/home)<br/>
[Jacek SPark Buckets](https://jaceklaskowski.github.io/spark-workshop/slides/spark-sql-bucketing.html#/home)<br/>

```bash
./bin/pyspark - uruchomienie interaktywnej wersji 
	Na porcie 4040 tworzy się UI 
```	
	
Wydajność to nie przeglądanie kodów źródłowych. OPtymalizacja aplikacji ostatnim krokiem powinno być przeglądanie kodów źródłowych. 
W celu optymalizacji prosimy o to co widzi Spark. 
	
Jak zrobić zrzut wszystkiego 
	
More > Monitoring > Viewing after the Fact - ustawiamy parametry 
```bash
spark.eventLog.enabled true
spark.eventLog.dir hdfs://namenode/shared/spark-logs 

./bin/pyspark -c spark.eventLog.enabled=true -c spark.eventLog.dir=/tmp/jobik (katalog musi istnieć)
```	
W UI > Environment mamy spis wszystkich ustawień dla JOBa

# Jak zaimportować ?
[Spark monitoring](https://spark.apache.org/docs/latest/monitoring.html)
Zakładka Executors - wyświetlenie executorów 

SQL - zapytanie SQL <br/>
Wchodzimy do joba iw idzimy Graph wykonania - u góry są wejścia danych <br/>
	FileScan - skanujemy plik o formacie text <br/>
	value#2 - schema <br/>
	Batched - wsadowe czy strumieniowe<br/>
	DataFilters - nie było żadnych filtrów <br/>
	Format - Format danych wejściowych text<br/>
	Location - wykorzystwyane przez Sparka do indeksowania jobów - z plików hdfs lub HiveMetastore, jak uruchamiamy spark to tworzony jest zuborzony hivemetastore w katalogu spark-warehouse w lokalizacji sparka <br/>
			spark-warehouse<br/>
	PartitionFilters<br/>
	PushedFilters<br/>
	ReadSchema <br/>

Jeżeli jest używany goły Pandas to wtedy nie widać tego w UI <br/>
	
Log<br/>
	DAGScheduler - byt planowanie naszych <br/>
	TaskSetManager 0.0 - pojedynczy task uruchomiony do realizacji zadania <br/>
		
		
Analizy zaczynamy od SQL - JOBS jest o wiele bardziej zaawansowany 	<br/>

spark.range(5).write.saveAsTable("cb") - zapytanie z 5 wierszowego DatFramu stworzył tabele i zapisał ją do lokalnego hive metastore <br/>
```bash
spark-warehouse/cb/part-00000-cba69d18-1a53-4c7e-bb9b-02f512bdf2f8-c000.snappy.parquet 297
spark-warehouse/cb/part-00003-cba69d18-1a53-4c7e-bb9b-02f512bdf2f8-c000.snappy.parquet 472
spark-warehouse/cb/part-00006-cba69d18-1a53-4c7e-bb9b-02f512bdf2f8-c000.snappy.parquet 472
spark-warehouse/cb/part-00012-cba69d18-1a53-4c7e-bb9b-02f512bdf2f8-c000.snappy.parquet 472
spark-warehouse/cb/part-00015-cba69d18-1a53-4c7e-bb9b-02f512bdf2f8-c000.snappy.parquet 472
```	
5 wierszy -> 6 plików 1 plik pusty - optymalizator sparka stwierdził że zapisze to w 6 partycjach. 1 plik jest pusty <br/>
```
Odczyt plik 						spark.read.parquet("spark-warehouse/cb/part-00000-cba69d18-1a53-4c7e-bb9b-02f512bdf2f8-c000.snappy.parquet").show()
Odczyt plik wyrażenie regularne 	spark.o.parquet("spark-warehouse/cb/part-000[0-1][1-6]-cba69d18-1a53-4c7e-bb9b-02f512bdf2f8-c000.snappy.parquet").show()
```
	
Na podstawie pliku możemy odczytać oznaczenie operacji cba69d18-1a53-4c7e-bb9b-02f512bdf2f8 <br/>

spark.table("cb").show()<br/>

```pyspark
from pyspark.sql.functions import input_file_name
df.withColumn("filename", input_file_name())

spark.table("cb").withColumn("filename", input_file_name()).show(100000, false) - wyłączenie 
```	
Domyślny format plików 

Zebranie logow z dzialania Sparka
```bash
/tmp/jabik/local-1639042398382
	
./sbin/start-history-server.sh - uruchomienie history servera i zaladowanie poprzedniej sesji 
	
WholeStageCodegen - kod wygenerowany w JAVA 
Range w srodku - output rows 
|
V
CreateDataSourceTableAsSelectCOmmand
```

Jak najedziemy na CreateDataSourceTableAsSelectCOmmand mamy informacje 
```
Execute CreateDataSourceTableAsSelectCOmmand `cb`.ErrorIfExists,[id] - argumenty ktre przyjmuje funkcja 
```
W Intelij Ctrl+o wyszukiwanie klas funckji w projekcie

W kodzie są funkcje tj Range które mają swoję reprezentacje 
```
Range - logiczna
RaneExec - fizyczna - ta która jest wykonywana
doProduce - funkcja ktora produkuje dane 

./bin/spark-shell
spark.range(5).quertExecution.debug.codegen
```
generowanie kodów które są odpwoiedzzialne za generowanie kodów 	

Wchodzimy w joba 
- patrzymy dalej na DAG (DAG Visualisation) 
- Patrzymy w link Associated SQL Query: <1>
- Patrzymy w link Completed jobs: <1>
- Duration
- Stages 

Kazde zapytanie SQL - sklada sie 0 lub wiecej JOBOW 
Kazdy job skalda sie z 1 lub wiecej stage (napewno 1)


Przy operacjach shuffle bedzie wiecej stage conajmniej 2 
Shuffle wystepuje przy group by, join kazda operacja ktora wymaga ulozenia danych 

A każdy stage składa się z Tasków - 1 lub wiele 

Taski są najmniejszymi jednostkami które odpowiadają za fizyczną realizację wykonują fizycznie kod i przetwarzają fizycznie dane 

Wykonano 16 completed task - wykonywane na 8 rdzeniach czyli 16 vCorach 

Czas wykonania stage to jest najdłuższy czas wykonania zdania 

Dlatego bardzo uważnie patrzymy na statystyki Stage

Wyliczenie 75 percentyla czasami = max - to wynikac moze z tego ze mamy małą próbkę danych i dlatego statystyka nie odzwierciedla 
Mala wartosc MIN moze oznaczac ze mamy duzo pustych przebiegow 
Na 16 taskow mamy tylko 5 rekordow

Dlaczego tak sie dzieje bo Spark tego nie wie i nie chce wiedziec. Nie chce ingerowac 


AQEShuffleRead - optymalizacja Shuffle read 

Analiza linika po linijce uruchamianie i sprawdzanie co sie dzieje

ANaliza z formatki SQL wykonania kodu 

W scali pokazana jest dokładna nazwa funkcji show() w PySpark bedziemy mieli showString bo Python jest przerabiany na kod Scala Java 

### Techniki

- Partycjonowanie - Jak ladowac dane do partycji w oparciu o wartosci w Oraclu mamy create partition YYYYMM jak to zrobic w Sparku. Proces Sparka dziala tymczasowo - Oracle caly czas. Na czas wykonania zadania mozemy sterowac iloscia partycji i podzialem danych potem nie mamy wplywu jezeli pojdzie na tym inny kod
- Bucketing - may gwarancje rownoleglego rozloenia danych 	
- BroadCastJoin - tabele faktow lub dimention - najszybszy join szybciej sie juz nie da 
- Adaptive Query Execution - bardzo nowa rzecz 
	