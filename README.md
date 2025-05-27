# db-university
Ciao a tutti
Esercizio di oggi: Db University
nome repo: db-university
Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.
Utilizzare https://www.drawio.com/ per la creazione dello schema. Esportare quindi il diagramma in jpg e caricarlo nella repo.
Buon lavoro!

esercizio n2:

1.Selezionare tutti gli studenti nati nel 1990 (160)

SELECT * 
FROM `db-university`.students
WHERE YEAR(date_of_birth) = 1990;

2.Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT * 
FROM `db-university`.courses
WHERE `cfu` > 10;

3.Selezionare tutti gli studenti che hanno più di 30 anni

SELECT * 
FROM `db-university`.students
WHERE YEAR(CURRENT_TIMESTAMP) - YEAR(date_of_birth) > 30;

4.Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

SELECT * 
FROM `db-university`.courses
WHERE year='1' AND `period`='I semestre';

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT * 
FROM `db-university`.exams
WHERE hour > '14:00' AND date = '2020/06/20';

6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT * 
FROM `db-university`.degrees 
WHERE name LIKE '%Magistrale%';

7. Da quanti dipartimenti è composta l'università? (12)

SELECT COUNT(id) 
FROM `db-university`.departments;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT COUNT(*) 
FROM `db-university`.teachers
WHERE phone IS NULL;

Esercizio 1 del 27/05/2025

1. Contare quanti iscritti ci sono stati ogni anno

SELECT
    YEAR(enrolment_date) AS `year`,  -- Estrai l'anno dalla colonna della data di iscrizione
    COUNT(*) AS `1000`  -- Conta tutti i record per ogni anno
FROM
     `db-university`.students  -- Sostituisci con il nome della tua tabella
GROUP BY
    `year`  -- Gruppa i dati per anno
ORDER BY
    `year`;  -- Ordinare i risultati per anno 

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT
    COUNT(office_address) AS `1000`  
FROM
     `db-university`.teachers  
GROUP BY
    `office_address`
ORDER BY `office_address`;

3. Calcolare la media dei voti di ogni appello d'esame

SELECT student_id, AVG(vote) AS media_voti
FROM `db-university`.exam_student
GROUP BY student_id;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT `db-university`.departments `name`,
    COUNT(*) AS `1000`
FROM 
   `db-university`.courses
GROUP BY 
    `db-university`.departments;

Esercizio 2 del 27/05/2025

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18