# EX CON GROUP BY

#### 1. Selezionare tutti gli studenti nati nel 1990 (160):
```sql
    SELECT * 
    FROM `students` 
    WHERE date_of_birth LIKE '1990%'
    GROUP BY id;
```

#### 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
```sql    
    SELECT * 
    FROM `courses`
    WHERE cfu > 10
    GROUP BY course_id;
```

#### 3. Selezionare tutti gli studenti che hanno più di 30 anni
```sql
    SELECT * 
    FROM `students`
    WHERE CURRENT_DATE() - YEAR(`date_of_birth`) > 30
    GROUP BY id;
```

#### 4. Selezionare tutti i corsi del primo semestre del primo anno di un    qualsiasi corso di laurea (286)
```sql
    SELECT * 
    FROM `courses` 
    WHERE period = "I semestre" AND year = "1"
    GROUP BY course_id;
```

#### 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
```sql
    SELECT * 
    FROM `exams`
    WHERE date ='2020-06-20'AND hour >= '14:00'
    GROUP BY exam_id;
```

#### 6. Selezionare tutti i corsi di laurea magistrale (38)
```sql
    SELECT * 
    FROM `degrees`
    WHERE level = "magistrale"
    GROUP BY degree_id;
```

#### 7. Da quanti dipartimenti è composta l'università? (12)
```sql
    SELECT COUNT(id) 
    FROM `departments`
    GROUP BY department_id;
```

#### 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
```sql
    SELECT COUNT(id) FROM `teachers` WHERE phone IS NULL GROUP BY teacher_id;
    
```

# EX CON SELECT

#### 1. Contare quanti iscritti ci sono stati ogni anno

```sql
    SELECT COUNT(id) AS enrolment_count, YEAR(enrolment_date) AS enrolment_year
    FROM students
    GROUP BY YEAR(enrolment_date);
```
#### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

 ```sql
    SELECT COUNT(id) 
    FROM teachers
    WHERE office_address = "Contrada Penelope 73";
```
#### 3. Calcolare la media dei voti di ogni appello d'esame

```sql
    SELECT exam_id, AVG(vote) AS average_grade
    FROM exam_student
    GROUP BY exam_id;
```
#### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
    SELECT COUNT(id) 
    FROM `departments`;
```

