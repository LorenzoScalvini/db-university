# Query sul Database Universitario

## Esercizio Completo

Dopo aver creato un nuovo database nel MySQL Workbench e aver importato lo schema allegato, eseguire le seguenti query.

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
