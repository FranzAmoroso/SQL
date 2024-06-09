window{
STRINGA DI CONNESSIONE
Server=localhost\SQLEXPRESS01;Database=master;Trusted_Connection=True;

CARTELLA DEI LOG DI ISTALLAZIONE DI SQL SERVER
C:\Program Files\Microsoft SQL Server\160\Setup Bootstrap\Log\20230606_234101

CARTELLA DI FILE MULTIMEDIALI DI ISTALLAZIONE
C:\SQL2022\Express_ITA

CATELLA DELLE RISORSE DI INSTALLAZIONE
C:\Program Files\Microsoft SQL Server\160\SSEI\Resources
}

# Data Types

I tipi di dati supportati in SQL possono variare leggermente a seconda del sistema di gestione del database (DBMS) che stai utilizzando

| Tipo           | Descrizione                                                                     |
| -------------- | ------------------------------------------------------------------------------- |
| INT            | Rappresenta numeri interi.                                                      |
| DECIMAL        | Rappresenta numeri decimali.                                                    |
| CHAR           | Stringhe di lunghezza fissa con una dimensione massima di 255 caratteri.        |
| VARCHAR        | Stringhe di lunghezza variabile con una dimensione massima di 65.535 caratteri. |
| TEXT           | Stringhe con una dimensione massima di 65.535 caratteri.                        |
| DATE           | Rappresenta valori di data nel formato YYYY-MM-DD.                              |
| DATETIME       | Rappresenta valori di data e ora combinati nel formato YYYY-MM-DD HH:MM:SS.     |
| TIMESTAMP      | Rappresenta valori di timestamp.                                                |
| FLOAT          | Rappresenta numeri in virgola mobile.                                           |
| DOUBLE         | Rappresenta numeri in virgola mobile con precisione maggiore rispetto a FLOAT.  |
| TIME           | Rappresenta un'ora, ad esempio 'HH:MM:SS'.                                      |
| BOOL o BOOLEAN | Rappresenta valori di verità, di solito vero o falso.                           |

# COSTREINT

I vincoli `constraints` sono condizioni che possono essere aggiunte alle tabelle di un database per garantire l'integrità dei dati. Esistono diversi tipi di vincoli che possono essere applicati a una colonna o a un insieme di colonne all'interno di una tabella. Di seguito sono elencati i principali tipi di vincoli:

| Tipo di Vincolo | Descrizione                                                                                                                                       |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| NOT NULL        | Il valore in una colonna non può essere nullo.                                                                                                    |
| PRIMARY KEY     | Identifica univocamente ogni riga e garantisce l'unicità dei valori nella colonna specificata.                                                    |
| UNIQUE          | Garantisce che tutti i valori in una colonna o in un insieme di colonne siano univoci.                                                            |
| DEFAULT         | Assegna un valore predefinito a una colonna se nessun valore è specificato durante l'inserimento dei dati.                                        |
| CHECK           | Definisce condizioni che i valori inseriti in una colonna devono soddisfare.                                                                      |
| FOREIGN KEY     | Crea una relazione tra due tabelle, in cui i valori in una colonna devono esistere in un'altra tabella.                                           |
| INDEX           | Struttura utilizzata per migliorare le prestazioni delle query, indicizzando i valori di una o più colonne. Questo non è tecnicamente un vincolo. |
| AUTO_INCREMENT  | Applicato a colonne di tipo numerico per generare automaticamente un valore univoco per ogni riga inserita nella tabella.                         |

# Database

## Creare un Database

La query `CREATE DATABASE` viene utilizzata per creare un nuovo database nel sistema di gestione dei database.

    CREATE DATABASE nome_database;

Questa query crea un nuovo database chiamato `nome_database`.

## Cancellare un Database

La query `DROP DATABASE` viene utilizzata per eliminare un database esistente.

    DROP DATABASE nome_database;

Questa query elimina il database chiamato `nome_database`.

# Tabella

## Creare una Tabella

La query `CREATE TABLE` viene utilizzata per creare una nuova tabella all'interno di un database specificato.

    CREATE TABLE nome_tabella (
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    cognome VARCHAR(50) NOT NULL
    );

Questa query crea una tabella chiamata `nome_tabella `con tre colonne: `id, nome e cognome`.

## Cancellare una Tabella

La query `DROP TABLE` viene utilizzata per eliminare una tabella esistente.

    DROP TABLE nome_tabella;

Questa query elimina la tabella chiamata `nome_tabella`.

## IF NOT EXISTS

La clausola `IF NOT EXISTS` viene utilizzata in molte query SQL, per verificare la presenza di un oggetto nel database prima di eseguire un'azione su di esso, evitando così errori dovuti a duplicati.

## ESEMPIO

    CREATE TABLE IF NOT EXISTS DatabasePHP.dipendenti(
        id_dipendente INT UNSIGNED NOT NULL AUTO_INCREMENT,
        nome VARCHAR(20) NOT NULL,
        cognome VARCHAR(20) NOT NULL,
        data_assunzione DATE NOT NULL,
        stipendio DECIMAL NOT NULL CHECK (stipendio >= 1500 AND stipendio <= 3000),
        telefono VARCHAR(10) NOT NULL UNIQUE,
        mansione VARCHAR(255) NOT NULL DEFAULT 'impiegato',
        PRIMARY KEY(id_dipendente)
    );

    CREATE TABLE IF NOT EXISTS DatabasePHP.clienti(
        id_cliente INT UNSIGNED NOT NULL AUTO_INCREMENT,
        denominazione VARCHAR(50),
        p_iva VARCHAR(16) NOT NULL UNIQUE,
        indirizzo VARCHAR(255) NOT NULL,
        telefono VARCHAR(10) NOT NULL UNIQUE,
        PRIMARY KEY(id_cliente)
    );

    CREATE TABLE IF NOT EXISTS DatabasePHP.rapporto_clienti(
        id_rapporto INT UNSIGNED NOT NULL AUTO_INCREMENT,
        id_cliente INT UNSIGNED NOT NULL,
        id_dipendente INT UNSIGNED NOT NULL,
        PRIMARY KEY(id_rapporto),
        FOREIGN KEY (id_cliente) REFERENCES DatabasePHP.clienti(id_cliente),
        FOREIGN KEY (id_dipendente) REFERENCES DatabasePHP.dipendenti(id_dipendente)
    );

# INSERT INTO

La query `INSERT INTO` viene utilizzata per inserire nuovi dati all'interno di una tabella.

    INSERT INTO clienti (denominazione, p_iva, indirizzo, telefono)
    VALUES
    ("ABC Ristorazione", '3482649736', 'Via Liberazione, Milano', '3379876258');

Questa query inserisce una nuova riga nella tabella clienti con i valori specificati per le colonne `denominazione, p_iva, indirizzo e telefono`.

## Inserimento Multiplo

È possibile inserire più righe di dati in una tabella utilizzando un unico comando `INSERT INTO`.

    INSERT INTO clienti (denominazione, p_iva, indirizzo, telefono)
    VALUES
    ("ABC Ristorazione", '3482649736', 'Via Liberazione, Milano', '3379876258'),
    ("XY PROGRAMMING", '0982735428', 'Via Roma, Cesena', '3372648365'),
    ("Picture Srl", '0029201813', 'Via Umberto, Catania', '3382927223'),
    ("F.lli Concessionaria", '0825173547', 'Via Gabasisi, Bologna', '3373876529');

Questa query inserisce quattro nuove righe nella tabella clienti con i valori specificati per le colonne `denominazione, p_iva, indirizzo e telefono`.

# SELECT

La clausola `SELECT` viene utilizzata per recuperare dati da una o più colonne di una tabella nel database.

    SELECT nome, cognome
    FROM dipendenti;

Questa query restituisce i valori delle colonne "nome" e "cognome" dalla tabella "dipendenti".

In SQL, l'asterisco (\*) è utilizzato per rappresentare tutti i campi di una tabella. Quando viene utilizzato in una query SELECT, seleziona tutte le colonne della tabella specificata.

    SELECT *
    FROM dipendenti;

## SELECT con WHERE

La clausola` WHERE` viene utilizzata per filtrare i risultati della query in base a una specifica condizione.

    SELECT nome, cognome
    FROM dipendenti
    WHERE dipartimento = 'Vendite';

Questa query restituisce i nomi e i cognomi dei dipendenti che appartengono al dipartimento `"Vendite"`.

## SELECT DISTINCT

La clausola `SELECT DISTINCT` viene utilizzata per selezionare valori unici da una colonna o da un insieme di colonne in una tabella.

    SELECT DISTINCT dipartimento
    FROM dipendenti;

Questa query restituisce tutti i valori unici della colonna `"dipartimento"` dalla tabella `"dipendenti"`, eliminando i duplicati.

# AGGIORNARE UNA COLONNA IN UNA TABELLA

L'operazione di aggiornamento di una colonna in una tabella viene eseguita con la sintassi `UPDATE`, permettendo di modificare i valori esistenti.

    UPDATE dipendenti
    SET stipendio = 2000
    WHERE id_dipendente = 1;

# DELETE FROM

Il comando `DELETE FROM` è utilizzato per eliminare righe da una tabella.

    DELETE FROM dipendenti
    WHERE id_dipendente = 1;

Se non avremo la clausola `WHERE` cancelleremo tutti i dati della tabella.

# TRUNCATE TABLE

`TRUNCATE TABLE` viene utilizzato per eliminare tutte le righe da una tabella, ripristinandola al suo stato iniziale.

    TRUNCATE TABLE dipendenti;

## TRUNCATE vs DELETE

- `TRUNCATE` ricrea la tabella con gli identificatori `auto-increment`.
- `DELETE` permette di filtrare le righe da cancellare.
- `TRUNCATE` è un comando di DDL (Data Definition Language).
- `DELETE` è un comando di DML (Data Manipulation Language).

- `TRUNCATE` è più veloce poiché cancella tutti i dati senza scansionare le righe.
- `DELETE` scansiona ogni riga prima di cancellarla.

# ALTER TABLE

Il comando `ALTER TABLE` viene utilizzato per modificare la struttura di una tabella, aggiungendo, modificando o rimuovendo colonne.

### Aggiungere Nuova Colonna

Questo comando aggiunge una nuova colonna alla tabella specificata con il tipo di dati specificato e vincoli opzionali.

    ALTER TABLE table_name
    ADD new_column datatype constraints;

### Cambiare Posizione della Colonna

Consente di modificare la posizione di una colonna nella tabella, specificando se deve essere posta dopo una determinata colonna esistente o come prima colonna.

    ALTER TABLE table_name
    MODIFY column_name column_definition
    AFTER/FIRST column_name;

### Aggiungere Vincoli:

Permette di aggiungere vincoli come chiavi primarie, chiavi esterne o vincoli unici alla tabella.

    ALTER TABLE table_name
    ADD CONSTRAINT constraint_name data_type(column_name,..);

### Rimuovere una Colonna:

Questo comando rimuove una colonna dalla tabella specificata.

    ALTER TABLE table_name
    DROP COLUMN column_name;

### Cambiare Tipo di Dato di una Colonna:

Consente di modificare il tipo di dati di una colonna esistente nella tabella.

    ALTER TABLE table_name
    MODIFY column_name new_data_type;

### Rinominare una Tabella:

Questo comando rinomina una tabella esistente con un nuovo nome specificato.

    ALTER TABLE current_table_name
    RENAME TO new_table_name;

## Legenda

| Comando       | Descrizione                                                                                                             |
| ------------- | ----------------------------------------------------------------------------------------------------------------------- |
| ALTER TABLE   | Comincia una dichiarazione di alterazione per modificare la tabella "table_name".                                       |
| ADD COLUMN    | Aggiunge una nuova colonna alla tabella specificata.                                                                    |
| MODIFY COLUMN | Modifica il tipo di dato o altre proprietà di una colonna esistente.                                                    |
| DROP COLUMN   | Rimuove una colonna dalla tabella.                                                                                      |
| RENAME        | Rinomina la tabella specificata.                                                                                        |
| TRUNCATE      | Elimina tutte le righe dalla tabella, ripristinando eventuali valori di auto-incremento.                                |
| DELETE        | Utilizzato per eliminare le righe specificate dalla tabella basate su determinate condizioni.                           |
| UPDATE        | Utilizzato per modificare i valori delle colonne nelle righe esistenti di una tabella basate su determinate condizioni. |
| SET           | Specifica i valori che devono essere impostati durante l'esecuzione di un comando UPDATE.                               |
| AFTER         | Specifica la posizione in cui una nuova colonna deve essere inserita dopo una colonna esistente.                        |
| FIRST         | Specifica che una nuova colonna deve essere inserita come prima colonna della tabella.                                  |
| TO            | Utilizzato con l'attributo RENAME per specificare il nuovo nome della tabella.                                          |

## CREATE TEMPORANY TABLE

Il comando `CREATE TEMPORARY TABLE name_table` consente di creare una tabella temporanea che esiste solo per la durata della `sessione` di connessione. Quando la sessione viene chiusa, la tabella temporanea viene automaticamente eliminata dal database.

    CREATE TEMPORARY TABLE table_name(column_definitions);

## DROP TEMPORANY TABLE

Il comando `DROP TEMPORARY TABLE nome_table` si utilizza per eliminare una tabella temporanea

    DROP TEMPORARY TABLE temp_table;

## Creare una temporany table con i dati di un altra tabella

Puoi anche creare una tabella temporanea basata sui dati di un'altra tabella.

    CREATE TEMPORARY TABLE temp_table2 SELECT * FROM existing_table;

Questo creerà una tabella temporanea chiamata `temp_table2` che conterrà tutti i dati della tabella esistente `existing_table`.

                                         |

# Operatori logici

| Operatore   | Descrizione                                                                                                                                         |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| =           | L'operatore di uguaglianza (=) viene utilizzato per confrontare se due valori sono uguali.                                                          |
| >           | L'operatore maggiore di (>) viene utilizzato per confrontare se il valore a sinistra è maggiore del valore a destra.                                |
| <           | L'operatore minore di (<) viene utilizzato per confrontare se il valore a sinistra è minore del valore a destra.                                    |
| >=          | L'operatore maggiore uguale di (>=) viene utilizzato per confrontare se il valore a sinistra è maggiore o uguale al valore a destra.                |
| <=          | L'operatore minore uguale di (<=) viene utilizzato per confrontare se il valore a sinistra è minore o uguale al valore a destra.                    |
| !=          | L'operatore diverso da (!= o <>) viene utilizzato per confrontare se due valori non sono uguali.                                                    |
| AND         | L'operatore logico AND viene utilizzato per combinare due o più condizioni e restituire solo le righe che soddisfano tutte le condizioni.           |
| OR          | L'operatore logico OR viene utilizzato per combinare due o più condizioni e restituire le righe che soddisfano almeno una delle condizioni.         |
| LIKE        | L'operatore LIKE viene utilizzato per confrontare se una stringa di testo corrisponde a un modello specificato utilizzando caratteri jolly.         |
| NOT LIKE    | L'operatore NOT LIKE viene utilizzato per confrontare se una stringa di testo non corrisponde a un modello specificato utilizzando caratteri jolly. |
| IN          | L'operatore IN viene utilizzato per verificare se un valore si trova in un elenco di valori specificato.                                            |
| NOT IN      | L'operatore NOT IN viene utilizzato per verificare se un valore non si trova in un elenco di valori specificato.                                    |
| BETWEEN     | L'operatore BETWEEN viene utilizzato per confrontare se un valore si trova all'interno di un intervallo specificato.                                |
| NOT BETWEEN | L'operatore NOT BETWEEN viene utilizzato per verificare se un valore non si trova all'interno di un intervallo specificato.                         |
| IS NULL     | L'operatore IS NULL viene utilizzato per verificare se un valore in una colonna è vuoto o nullo.                                                    |
| IS NOT NULL | L'operatore IS NOT NULL viene utilizzato per verificare se un valore in una colonna non è vuoto o non nullo.                                        |

# AND, OR, NOT e !=

Questi operatori logici consentono di costruire condizioni complesse nelle query SQL, combinando più condizioni di filtro. Di seguito sono forniti il titolo, la descrizione e degli esempi con tabelle descrittive delle query:

### AND

La sintassi `AND` definisce la condizione in cui tutte le condizioni specificate devono essere vere affinché una riga sia inclusa nel risultato della query.

    SELECT colonna1, colonna2, colonna3, ecc..
    FROM tabella
    WHERE condizione1 AND condizione2 AND condizione3;

### OR

La sintassi `OR` definisce la condizione in cui almeno una delle condizioni specificate deve essere vera affinché una riga sia inclusa nel risultato della query.

    SELECT colonna1, colonna2, colonna3, ecc..
    FROM nometabella
    WHERE condizione1 OR condizione2;

### NOT

La sintassi `NOT` definisce la condizione di esclusione, indicando che le righe che soddisfano la condizione specificata non devono essere incluse nel risultato della query.

    SELECT colonna1, colonna2, colonna3, ecc..
    FROM nometabella
    WHERE NOT condizione1;

### !=

La sintassi `!=` (diverso da) è un operatore di confronto che restituisce `TRUE` se i due valori non sono uguali.

    SELECT colonna1, colonna2, colonna3, ecc..
    FROM nometabella
    WHERE colonna1 != valore;

### Esempio di utilizzo

    SELECT *
    FROM dipendenti
    WHERE (stipendio >= 1750 AND stipendio <= 2000)
        AND data_assunzione BETWEEN '2020-01-01' AND '2024-01-31'
        AND (mansione = 'Ingegnere Meccanico' OR mansione = 'Ingegnere Informatico')
        AND NOT (reparto = 'Amministrazione')
        AND data_nascita != '1990-01-01';

Questa query seleziona tutte le righe dalla tabella `"dipendenti"` in cui lo `stipendio` è compreso tra `1750` e `2000,` la `data di assunzione` è compresa tra il `1 gennaio 2020` e il `31 gennaio 2024`, la mansione è `"Ingegnere Meccanico"` o "`Ingegnere Informatico"`, il reparto `non è "Amministrazione"` e `la data di nascita non è il 1 gennaio 1990`.

# IN e BETWEEN

`IN` e `BETWEEN` sono due clausole comuni utilizzate nelle query SQL per filtrare i risultati basati su valori specifici o su un intervallo di valori. Di seguito sono fornite le descrizioni e gli esempi di entrambe le clausole:

### IN

La clausola `IN`permette di selezionare le righe in cui il valore di una colonna si trova tra una serie di valori specificati.

    SELECT *
    FROM table_name
    WHERE column_name IN (value1, value2, ...);

### NOT IN

La clausola NOT IN permette di selezionare le righe in cui il valore di una colonna non si trova tra una serie di valori specificati.

    SELECT *
    FROM employees
    WHERE department_id NOT IN (101, 102);

#### IN e NOT IN

| Query SQL                                                        | Descrizione                                                                                                    |
| ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `SELECT * FROM employees WHERE department_id IN (101, 102);`     | Restituisce le righe dalla tabella "employees" in cui il valore nella colonna "department_id" è 101 o 102.     |
| `SELECT * FROM employees WHERE department_id NOT IN (101, 102);` | Restituisce le righe dalla tabella "employees" in cui il valore nella colonna "department_id" non è 101 o 102. |

### BETWEEN

La clausola `BETWEEN` permette di selezionare le righe in cui il valore di una colonna si trova all'interno di un intervallo specificato.

    SELECT *
    FROM table_name
    WHERE column_name BETWEEN min_value AND max_value;

### NOT BETWEEN

La clausola NOT BETWEEN permette di selezionare le righe in cui il valore di una colonna non si trova all'interno di un intervallo specificato.

    SELECT *
    FROM table_name
    WHERE column_name NOT BETWEEN min_value AND max_value;

#### BETWEEN e NOT BETWEEN

| Query SQL                                                   | Descrizione                                                                                                      |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `SELECT * FROM products WHERE price BETWEEN 10 AND 50;`     | Restituisce le righe dalla tabella "products" in cui il valore nella colonna "price" è compreso tra 10 e 50.     |
| `SELECT * FROM products WHERE price NOT BETWEEN 10 AND 50;` | Restituisce le righe dalla tabella "products" in cui il valore nella colonna "price" non è compreso tra 10 e 50. |

# LIKE

La clausola `LIKE `viene utilizzata per cercare pattern di testo all'interno dei dati delle colonne.

    SELECT columns
    FROM table_name
    WHERE condition LIKE pattern;

### Pattern (non è case sensitive)

| Pattern                                     | Descrizione                                                                        |
| ------------------------------------------- | ---------------------------------------------------------------------------------- |
| COMINCIA CON 'C%'                           | Restituisce tutte le condizioni che iniziano con la lettera "C".                   |
| FINISCE CON 'C%'                            | Restituisce tutte le condizioni che terminano con la lettera "C".                  |
| CONTIENE '%C%'                              | Restituisce tutte le condizioni che contengono la lettera "C".                     |
| Caratteri fissi e comincia con 'C\*'        | Restituisce le condizioni che iniziano con "C" e hanno caratteri fissi dopo.       |
| Caratteri fissi e finisce con la '\_C'      | Restituisce le condizioni che terminano con "C" e hanno caratteri fissi prima.     |
| Caratteri fissi e contiene la '\_C\*'       | Restituisce le condizioni che contengono "C" e hanno caratteri fissi prima e dopo. |
| Contiene la stringa e inizia la '%C\_'      | Restituisce le condizioni che contengono "C" e finiscono con "\_" dopo.            |
| Contiene la stringa e finisce con la '\_C%' | Restituisce le condizioni che contengono "C" e iniziano con "\_" prima.            |

# ORDER BY

L'istruzione ORDER BY viene utilizzata per ordinare i risultati della query in base ai valori di una o più colonne. Le opzioni `ASC` e `DESC` definiscono l'ordine ascendente o discendente.

### ASC

`ASC` significa ascendente. Ordina i risultati in ordine crescente.

    SELECT *
    FROM table_name
    ORDER BY column1 ASC;

### DESC

`DESC` significa discendente. Ordina i risultati in ordine decrescente.

    SELECT *
    FROM table_name
    ORDER BY column1 DESC;

## Ordinare Colonne Multiple

Possiamo ordinare su più colonne in sequenza, dall'alto verso il basso o viceversa, utilizzando `ASC` o `DESC`. Questo è utile quando abbiamo valori uguali nelle diverse colonne.

    SELECT *
    FROM table_name
    ORDER BY column1, column2 ASC;

    SELECT *
    FROM table_name
    ORDER BY column1, column2 DESC;

### ORDER BY ASC e DESC

| Query SQL                                                                      | Descrizione                                                                                                                              |
| ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `SELECT * FROM employees ORDER BY last_name ASC;`                              | Restituisce tutti i dipendenti ordinati per cognome in ordine alfabetico crescente.                                                      |
| `SELECT * FROM products ORDER BY price DESC;`                                  | Restituisce tutti i prodotti ordinati per prezzo in ordine decrescente.                                                                  |
| `SELECT * FROM students ORDER BY grade ASC, last_name DESC;`                   | Restituisce tutti gli studenti ordinati per voto in ordine crescente, e in caso di parità, per cognome in ordine alfabetico decrescente. |
| `SELECT * FROM customers WHERE city = 'Rome' ORDER BY registration_date DESC;` | Restituisce tutti i clienti di Roma ordinati per data di registrazione in ordine decrescente.                                            |

# LIMIT e LIMIT OFFSET

Le clausole `LIMIT` e `LIMIT OFFSET` vengono utilizzate per limitare il numero di righe restituite da una query e per specificare da quale riga iniziare a restituire i risultati.

### LIMIT

La clausola `LIMIT` viene utilizzata per limitare il numero di righe restituite dalla query.

    SELECT *
    FROM dipendenti
    ORDER BY stipendio DESC
    LIMIT 3;

### LIMIT OFFSET

La clausola `LIMIT OFFSET` viene utilizzata per saltare un certo numero di righe e restituire un numero specificato di righe dopo il salto.

    SELECT *
    FROM table_name
    ORDER BY id
    LIMIT 1, 3;

Questa query salta la prima riga e restituisce le righe da 2 a 4.

### Limit e Limit offset

| Query SQL                                                                                            | Descrizione                                                                                       |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `SELECT * FROM dipendenti ORDER BY stipendio DESC LIMIT 3;`                                          | Restituisce i primi 3 dipendenti con lo stipendio più alto.                                       |
| `SELECT * FROM ordini WHERE cliente_id = 123 ORDER BY data_ordine DESC LIMIT 10;`                    | Restituisce gli ultimi 10 ordini effettuati da un cliente specifico, ordinati per data di ordine. |
| `SELECT * FROM articoli ORDER BY prezzo ASC LIMIT 5;`                                                | Restituisce i primi 5 articoli con il prezzo più basso.                                           |
| `SELECT * FROM prodotti WHERE categoria = 'Elettronica' ORDER BY data_inserimento DESC LIMIT 0, 10;` | Restituisce i primi 10 prodotti della categoria 'Elettronica', ordinati per data di inserimento.  |

JOIN
-cosa sono
-INNER JOIN
sintassi INNER JOIN:
andiamo a prendere i dati della tabella A che combaciano con la tabella B
SELECT campitable_name1, campitable_name2
FROM table_name1
INNER JOIN table_name2 ON condizione;
-LEFT JOIN
Andiamo a prendere tutti i dati della tabella di A, e quei dati della tabella di B che combaciano con la tabella A.
-RIGHT JOIN
Andiamo a prendere tutti i dati della tabella B e quei dati della tabella di A che sono uguali alla tabella di B.
-FULL JOIN(non disponibili in MSQl -->union)

-CROSS JOIN

ALIAS
Con alias possiamo rinominare le clausole, i dati, ecc..
sintassi alias
SELECT column1 AS x
FROM table_name AS y
where y.x;
in questo caso column1 prende il nome di x e table_name prende il nome di y.
esempio :
SELECT x.nome, DATE_FORMAT(data_assunzione, '%e %M, %Y') AS Data_assunzione
FROM dipendenti AS x;
Con questo andremo a vedere nella tabella dipendenti(x) le colonne:
nome e DATE_FORMAT(data_assunzione, '%e %M, %Y') rinominata Data_assunzione con AS(Alias)

GROUP BY
-con GROUP BY andiamo a mostrare un gruppo di dati, senza che si ripetino se vi sono dati uguali.
-con GROUP BY possiamo usare questa sintassi:
SELECT x.column1,count(elemento_da_contare) AS ABCcount
FROM table_name1 AS x
LEFT JOIN table_name2 AS y
ON x.id = y.id;
GROUP BY x.column1;
HAVING ABCcount = 'value da mostrare'
così facendo con count andrà a contare i dati B ripetuti in A e con GROUP BY non ripeterà più volte le righe di A.
-HAVING
HAVING = 'value';
having serve per mostrare gli agreggati di GROUP BY dove il conteggio che abbiamo fatto e uguale al value di HAVING

CREATE VIEW
-cosa sono le view
le view o viste in italiano, sono una scorciatoia sulle tabelle, cioè,
sono delle query salvate.
-perchè usarle
-esempio pratico
creare view: CREATE VIEW nome_view AS
chiamare view: SELECT \* FROM nome_view;
-sostituire una view esistente
CREATE OR REPLACE VIEW nome_view AS

-aggiornare dati attraverso view

-rimuovere view
DROP view_nome;

# Alcuni tipi di dati relativi al tempo


| Tipo di Dato | Descrizione                                                                                                                                | Esempio               |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | --------------------- |
| DATE         | Rappresenta una data nel formato YYYY-MM-DD. L'intervallo supportato è da '1000-01-01' a '9999-12-31'.                                     | '2023-02-15'          |
| TIME         | Rappresenta un'ora nel formato HH:MM:SS o HHH:MM:SS. L'intervallo supportato è da '-838:59:59' a '838:59:59'.                              | '14:30:00'            |
| DATETIME     | Rappresenta una data e un'ora nel formato YYYY-MM-DD HH:MM:SS. L'intervallo supportato è da '1000-01-01 00:00:00' a '9999-12-31 23:59:59'. | '2023-02-15 14:30:00' |
| TIMESTAMP    | Rappresenta una data e un'ora nel formato YYYY-MM-DD HH:MM:SS. L'intervallo supportato è da '1970-01-01 00:00:00' a '2037-12-31 23:59:59'. |
| YEAR         | Rappresenta un anno Rappresenta un anno nel formato YYYY. L'intervallo supportato è da '1901' a '2155'.                                    | '2023'                |

## Proprietà di aggiornamento automatico

- DEFAULT CURRENT_TIMESTAMP: Imposta automaticamente la data corrente come valore predefinito per la colonna quando non viene specificato alcun valore.
- ON UPDATE CURRENT_TIMESTAMP: Imposta automaticamente la data corrente ogni volta che viene aggiornata una riga della tabella.

## Operazioni su date e tempo

### Estrarre parti delle date

È possibile estrarre parti specifiche da una data utilizzando funzioni come YEAR(), MONTH(), DAYOFMONTH(), MONTHNAME(), DAYNAME(), HOUR(), MINUTE(), SECOND().

        SELECT YEAR('2023-02-15') AS Year;   -- Output: 2023
        SELECT MONTH('2023-02-15') AS Month; -- Output: 2

Per restituire i nomi dei dipendenti e l'anno di assunzione corrispondente per ciascun dipendente dalla tabella "dipendenti"

        SELECT nome, YEAR(data_assunzione) AS year FROM dipendenti;

### DATE_SUB():

Consente di sottrarre un intervallo di tempo da una data. Ad esempio, `DATE_SUB(CURRENT_DATE(), INTERVAL 18 YEAR)` restituirà la data per gli studenti che avranno 18 anni.

    SELECT email FROM studenti WHERE data_nascita <= DATE_SUB(CURRENT_DATE(), INTERVAL 18 YEAR);

### NOW()

Utilizzando now() all'interno di una clausola DATE, DATETIME, TIMESTAMP, ecc., si ottiene la data e l'ora correnti

    INSERT INTO table_name (date_column, datetime_column) VALUES (NOW(), NOW());

Questa query inserisce la data e l'ora correnti nelle colonne date_column e datetime_column rispettivamente.

Queste operazioni sono essenziali per la manipolazione e la formattazione delle date e degli orari nei database.

### date_format()

La funzione DATE_FORMAT() consente di formattare le date in base a un formato specifico.

    SELECT DATE_FORMAT('2023-02-15', '%M %e %Y') AS FormattedDate; -- Output: 'February 15 2023'

### Personalizzazione del Formato della Data nella Visualizzazione SELECT

Supponiamo di avere una tabella dipendenti con le seguenti righe:

| id_dipendente | nome  | cognome | data_assunzione | stipendio |
| ------------- | ----- | ------- | --------------- | --------- |
| 1             | Mario | Rossi   | 2023-01-15      | 1500      |
| 2             | Laura | Bianchi | 2022-08-20      | 1600      |
| 3             | Luca  | Verdi   | 2023-03-10      | 1750      |
| 4             | Anna  | Neri    | 2022-11-05      | 1500      |

##### Seleziona la data di assunzione, il nome e lo stipendio dei dipendenti con uno stipendio maggiore o uguale a 1600, formattando la data di assunzione nel formato giorno Mese Anno.

    SELECT DATE_FORMAT(data_assunzione, '%d %M %Y') AS data_assunzione, nome, stipendio
    FROM dipendenti
    WHERE stipendio >= 1600;

- SELECT DATE_FORMAT(data_assunzione, '%d %M %Y') AS data_assunzione, nome, stipendio:

  - Utilizza la funzione DATE_FORMAT per formattare la colonna data_assunzione nel formato giorno Mese Anno (%d %M %Y).
  - L'alias AS data_assunzione viene utilizzato per rinominare la colonna formattata nei risultati della query.
  - Insieme a nome e stipendio, queste colonne vengono selezionate per essere mostrate nei risultati.

| data_assunzione | nome  | stipendio |
| --------------- | ----- | --------- |
| 20 August 2022  | Laura | 1600      |
| 10 March 2023   | Luca  | 1750      |

Ecco le varie forme di formattazione che è possibile utilizzare con DATE_FORMAT():

| Formato | Descrizione                   | Esempio            |
| ------- | ----------------------------- | ------------------ |
| %Y      | Anno a quattro cifre          | 2024               |
| %y      | Anno a due cifre              | 24                 |
| %M      | Nome completo del mese        | February           |
| %m      | Numero del mese con zero      | 02                 |
| %b      | Abbreviazione del mese        | Feb                |
| %D      | Giorno del mese con suffisso  | 1st, 2nd, 3rd, 4th |
| %d      | Giorno del mese con zero      | 01, 02, 03         |
| %a      | Abbreviazione del giorno      | Mon                |
| %W      | Nome completo del giorno      | Monday             |
| %H      | Ora (formato 24 ore) con zero | 00, 01, ..., 23    |
| %h      | Ora (formato 12 ore) con zero | 01, 02, ..., 12    |
| %i      | Minuti con zero iniziale      | 00, 01, ..., 59    |
| %s      | Secondi con zero iniziale     | 00, 01, ..., 59    |
| %p      | AM o PM                       | AM, PM             |

## Modifica del Formato della Data nel Database

Per cambiare direttamente il formato di una data nel database, è necessario prima modificare l'attributo della colonna da `DATE` a `VARCHAR`, e successivamente cambiare il formato della data.

##### Modifica il tipo di dato della colonna a `VARCHAR` per riflettere il nuovo formato della data.

    ALTER TABLE dipendenti
    MODIFY COLUMN data_assunzione VARCHAR(20);

##### Utilizzando la funzione `DATE_FORMAT`, puoi convertire le date esistenti nel formato desiderato.

    UPDATE dipendenti
    SET data_assunzione = DATE_FORMA(data_assunzione, '%d %M %Y');

## Modifica del Formato VARCHAR a DATE nel Database

La prima query UPDATE aggiorna la colonna "data_assunzione" nella tabella "dipendenti" utilizzando la funzione STR_TO_DATE() per convertire la data dal formato testuale '%y-%m-%d' al formato di data nativo. Successivamente, la seconda query ALTER TABLE modifica la struttura della colonna "data_assunzione" per utilizzare il tipo di dato DATE.

    UPDATE dipendenti
    SET data_assunzione = STR_TO_DATE(data_assunzione, '%y-%m-%d');

    ALTER TABLE dipendenti MODIFY COLUMN data_assunzione DATE;

# Real Escape String

Il metodo `real_escape_string` viene utilizzato per evitare l'hacking di tipo `SQL injection` quando si manipolano dati provenienti dall'input dell'utente prima di inserirli in una query SQL.

- Sintassi:

        $escaped_string = $connessione->real_escape_string($_REQUEST['valore']);

Questo metodo prende in ingresso un valore e restituisce una versione del valore con tutti i caratteri speciali `"escaped"` (ovvero con un carattere di escape anteposto). Ciò significa che i caratteri che potrebbero essere interpretati come parte di una query SQL, come virgolette singole o doppie, sono preceduti da un carattere di escape per renderli sicuri all'interno della query.

    $nome = $connessione->real_escape_string($_REQUEST['nome']);

    $cognome = $connessione->real_escape_string($_REQUEST['cognome']);

    $email = $connessione->real_escape_string($_REQUEST['email']);
    
    $password = $connessione->real_escape_string($_REQUEST['password']);

In questo esempio, stiamo proteggendo le variabili `$nome`, `$cognome,` `$email` e `$password` dalle possibili vulnerabilità di `SQL injection` utilizzando il metodo `real_escape_string` della connessione al database.
