<!-- Consegna

Modellizzare la struttura di una tabella per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;

- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. -->

# Database Università

## Departments <!--sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.); -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
name: VARCHAR(40), NOTNULL
address: VARCHAR(40), NOTNULL
website: VARCHAR(150), NULL
country: DEFAULT("it-IT"), NOTNULL
description: TEXT, NULL
?course_id? : FK, NOTNULL, SMALLINT, UNIQUE

## Degree <!-- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..) -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
title: VARCHAR(40), NOTNULL
date: YEAR NOTNULL
type: VARCHAR(50), NOTNULL
desc: TINYINT, NOTNULL
?course_id? : FK, NOTNULL, AUTOINCREMENTAL, SMALLINT, UNIQUE
?student_id?: FK, NOTNULL, AUTOINCREMENTAL, SMALLINT, UNIQUE

## Courses <!-- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.) -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
title: VARCHAR(50), NOTNULL
cfu: TINYINT, NOTNULL
price: FLOAT(7,2), NOTNULL
type: VARCHAR(50), NOTNULL
calendar: YEAR, NOTNULL
desc: TEXT, NOTNULL
?student_id?: FK, NOTNULL, AUTOINCREMENTAL, SMALLINT, UNIQUE
?teacher_id?: FK, NOTNULL, AUTOINCREMENTAL, SMALLINT, UNIQUE

## Teachers <!-- ogni Corso può essere tenuto da diversi Insegnanti; -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
name: VARCHAR(50), NOTNULL
lastname: VARCHAR(50), NOTNULL
email: VARCHAR(40), NULL
qualify: VARCHAR(40), NOTNULL
serial_number: VARCHAR(50), NOTNULL, UNIQUE,
age: TINYINT, NOTNULL
genre: VARCHAR(30), NULL
salary: FLOAT(7,2), NULL
email: VARCHAR(50), NOTNULL
cell_number: VARCHAR(15) NULL

## Appeal <!-- ogni Studente può iscriversi a più appelli di Esame -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
title: VARCHAR(50), NOTNULL
date: DATETIME NOTNULL
cfu: TINYINT, NOTNULL
type: VARCHAR(50), NOTNULL
notes: SMALLINT, NOTNULL
?student_id?: FK, NOTNULL, AUTOINCREMENTAL, SMALLINT, UNIQUE
?teacher_id?: FK, NOTNULL, AUTOINCREMENTAL, SMALLINT, UNIQUE

## Students <!-- ogni Studente -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
name: VARCHAR(50), NOTNULL
lastname: VARCHAR(50), NOTNULL
serial_number: VARCHAR(50), NOTNULL, UNIQUE,
total_cfu: SMALLINT, NOTNULL
age: TINYINT, NOTNULL
genre: VARCHAR(30), NULL
taxes: FLOAT(7,2), NOTNULL
email: VARCHAR(50), NOTNULL
cell_number: VARCHAR(15) NULL
