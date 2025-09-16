Esercizio di oggi:
nome repo: db-university

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

Utilizzare https://www.drawio.com/ per la creazione dello schema.
Esportare quindi il diagramma in jpg e caricarlo nella repo.

//////////////////////////////////////////////////////////////////////////////////////////////

Esercizio di oggi:
nome repo: db-university

Dopo aver creato un nuovo database nel vostro MySQL Workbench e aver importato lo schema allegato, eseguite le query del file allegato.

Cosa consegnare?
Dopo aver testato le vostre query con MySQL Workbench, riportatele in un file txt e caricatelo nella vostra repo.

Guida all’installazione

Installazione SQL e MySQL Workbench (Windows)
Scarichiamo il https://dev.mysql.com/downloads/installer/ e gestiamo tutto col Wizard.
Scegliamo la versione Full installando anche MySQL Workbench e MySQL Shell
Impostiamo l’avvio di MySQL all’avvio del PC
Impostiamo una password per l’utente root
Installazione SQL MySQL Workbench (Mac)
Scarichiamo il bundle DMG per macOS dalla pagina MySQL ufficiale .
Lanciamo anche lì l’installer e facciamo il setup
Impostiamo una password per l’utente root (richiede almeno 8 lettere)
Scarichiamo anche MySQL Workbench https://dev.mysql.com/downloads/workbench/

//////////////////////////////////////////////////////////////////////////////////////////////

1. Selezionare tutti gli studenti nati nel 1990 (160)

   SELECT `date_of_birth`
   FROM `students`
   WHERE `date_of_birth` BETWEEN '1990-01-01' AND '1990-12-31';

/////////////////////////////////////////////////////////////////////////////////////////////////  
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT `cfu`
FROM `courses`
WHERE `cfu` > 10;

//////////////////////////////////////////////////////////////////////////////////////////////////// 3. Selezionare tutti gli studenti che hanno più di 30 anni

SELECT (\*)
FROM `students`
WHERE TIMESTAMPDIFF(YEAR,`date_of_birth`,CURDATE()) > 30;

//////////////////////////////////////////////////////////////////////////////////////////////////// 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)

SELECT `period`,`year`
FROM `courses`
WHERE `year` = 1 AND `period` = 'I semestre';

///////////////////////////////////////////////////////////////////////////////////////////////// 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)

SELECT `date`,`hour`
FROM `exams`
WHERE `date` = '2020-06-20' AND `hour` > '14:00';

///////////////////////////////////////////////////////////////////////////////////////////////// 6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT `level`
FROM `degrees`
WHERE `level` = 'magistrale';

////////////////////////////////////////////////////////////////////////////////////////////////// 7. Da quanti dipartimenti è composta l'università? (12)

SELECT COUNT(`name`)
FROM `departments`

///////////////////////////////////////////////////////////////////////////////////////////////// 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT COUNT(\*)
FROM `teachers`
WHERE `phone` IS NULL;

////////////////////////////////////////////////////////////////////////////////////////////////////
EX-Query con GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno

   SELECT YEAR(`enrolment_date`) AS `year`, COUNT(\*) AS `number_students`
   FROM `students`
   GROUP BY YEAR(`enrolment_date`);

///////////////////////////////////////////////////////////////////////////////////////////////// 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT `office_address`, COUNT(\*) AS `numbers_teachers`
FROM `teachers`
GROUP BY `office_address`;

///////////////////////////////////////////////////////////////////////////////////////////////// 3. Calcolare la media dei voti di ogni appello d'esame

SELECT `exam_id`, AVG(`vote`) AS `media_voti`
FROM `exam_student`
WHERE `vote` IS NOT NULL
GROUP BY `exam_id`;

///////////////////////////////////////////////////////////////////////////////////////////////// 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
