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
website: VARCHAR(150), NOTNULL
country: DEFAULT("it-IT"), NOTNULL
description: TEXT, NULL
?course_id? : FK, NOTNULL, AUTOINCREMENTAL, TINYINT

## Degree <!-- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..) -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
title: VARCHAR(40), NOTNULL
date: DATETIME NOTNULL
type: VARCHAR(50), NOTNULL
?course_id? : FK, NOTNULL, AUTOINCREMENTAL, TINYINT
?student_id?: FK, NOTNULL, AUTOINCREMENTAL, TINYINT

## Courses <!-- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.) -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
name: VARCHAR(50), NOTNULL
cfu: TINYINT, NOTNULL
price: FLOAT(7,2), NOTNULL
type: VARCHAR(50), NOTNULL
calendar: YEAR, NOTNULL
desc: TEXT, NOTNULL
?student_id?: FK, NOTNULL, AUTOINCREMENTAL, TINYINT
?teacher_id?: FK, NOTNULL, AUTOINCREMENTAL, TINYINT

## Teachers <!-- ogni Corso può essere tenuto da diversi Insegnanti; -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
name: VARCHAR(50), NOTNULL
lastname: VARCHAR(50), NOTNULL
email: VARCHAR(40), NULL
qualify: VARCHAR(40), NOTNULL

## Exams <!-- ogni Studente è iscritto ad un solo Corso di Laurea -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
title: VARCHAR(50), NOTNULL
cfu: TINYINT, NOTNULL
?student_id?: FK, NOTNULL, AUTOINCREMENTAL, TINYINT
?teacher_id?: FK, NOTNULL, AUTOINCREMENTAL, TINYINT

## Appeal <!-- ogni Studente può iscriversi a più appelli di Esame -->

id: PK, NOTNULL, INDEX, UNIQUE, AUTOINCREMENTAL
date: DATETIME NOTNULL
cfu: TINYINT, NOTNULL
type: VARCHAR(50), NOTNULL
?student_id?: FK, NOTNULL, AUTOINCREMENTAL, TINYINT
?teacher_id?: FK, NOTNULL, AUTOINCREMENTAL, TINYINT

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
