# Query sul Database Universitario

## Esercizio Completo

Dopo aver creato un nuovo database nel MySQL Workbench e aver importato lo schema allegato, eseguire le seguenti query.

### Query SELECT

## 1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql
SELECT * 
FROM students 
WHERE YEAR(date_of_birth) = 1990;
```

## 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
SELECT * 
FROM courses 
WHERE cfu > 10;
```

## 3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT * 
FROM students 
WHERE YEAR(CURDATE()) - YEAR(date_of_birth) > 30;
```

## 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```sql

```

## 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```sql
SELECT * 
FROM exams 
WHERE date = '2020-06-20' AND TIME(hour) > '14:00:00';
```

## 6.  Selezionare tutti i corsi di laurea magistrale (38)

```sql

```

## 7. Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT COUNT(*) AS numero_dipartimenti 
FROM departments;
```

## 8. Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT COUNT(*) AS insegnanti_senza_telefono 
FROM teachers 
WHERE phone IS NULL;
```

## 9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)

```sql

```

## 10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

```sql
UPDATE teachers SET office_number = 126 WHERE name = 'Pietro' AND surname = 'Rizzo';
```

## 11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

```sql

```

### Query GROUP BY

## 1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT YEAR(enrolment_date) AS anno_iscrizione, COUNT(*) AS numero_iscritti
FROM students
GROUP BY YEAR(enrolment_date)
ORDER BY anno_iscrizione;
```

## 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT office_address, COUNT(*) AS numero_insegnanti
FROM teachers
GROUP BY office_address
HAVING numero_insegnanti > 1
ORDER BY numero_insegnanti DESC;
```

## 3. Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT exam_id, AVG(vote) AS media_voti
FROM exam_student
GROUP BY exam_id
ORDER BY exam_id;
```

## 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT departments.name AS dipartimento, COUNT(degrees.id) AS numero_corsi
FROM departments
LEFT JOIN degrees ON departments.id = degrees.department_id
GROUP BY departments.id, departments.name
ORDER BY numero_corsi DESC;
```

### Query JOIN

## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT students.*
FROM students
JOIN degrees ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di Laurea in Economia'
ORDER BY students.surname, students.name;
```

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql

```

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT courses.*
FROM courses
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON course_teacher.teacher_id = teachers.id
WHERE teachers.id = 44;
```

## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT students.*, degrees.name AS 'corso_laurea', departments.name AS 'dipartimento'
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.surname, students.name;
```

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT degrees.name AS 'corso_laurea', courses.name AS 'corso', 
       teachers.name AS 'nome_docente', teachers.surname AS 'cognome_docente'
FROM degrees
JOIN courses ON degrees.id = courses.degree_id
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON course_teacher.teacher_id = teachers.id
ORDER BY degrees.name, courses.name;
```

## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql

```

## 7. Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql

```
