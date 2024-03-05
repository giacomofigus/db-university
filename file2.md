# EX CON JOIN

#### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
    SELECT `students`. `name` AS nome_studente, `students`. `surname` AS cognome_studente, `degrees` . `name` AS corso
    FROM `students`
    JOIN `degrees`
    ON `students`.`degree_id` = `degrees`. `id`
    WHERE `degrees`. `name` = 'Corso di Laurea in Biologia';
```

#### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
    SELECT degrees.name AS nome_corso, departments.name AS nome_dipartimento , `degrees`. `level` AS level
    FROM `degrees`
    JOIN `departments`
    ON `degrees`. `department_id` = `departments` . `id`
    WHERE `degrees`. `department_id` = 7
    AND `degrees`. `level` = 'magistrale';
```

#### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
    SELECT *
    FROM course_teacher
    JOIN teachers 
    ON course_teacher.teacher_id = teachers.id
    WHERE teachers.id = 44;
```

#### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
    SELECT students.name AS nome_studente, students.surname AS cognome_studente, degrees.name AS corso_laurea, departments.name AS nome_dipartimento
    FROM `students`
    JOIN `degrees`
    ON `students`.`degree_id` = degrees.id 
    JOIN `departments`
    ON `degrees`.`department_id` = departments . id
    WHERE students.name LIKE '%A'
    ORDER BY students.name;
```

#### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
    SELECT teachers.name AS nome_insegnante, teachers.surname AS cognome_insegnante, degrees.name AS nome_corso_laurea, courses.name AS nome_corso 
    FROM degrees
    JOIN courses ON degrees.id = courses.degree_id
    JOIN course_teacher ON courses.id = course_teacher.course_id
    JOIN teachers ON teachers.id = course_teacher.teacher_id;
```

#### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
    SELECT teachers.*
    FROM teachers
    JOIN course_teacher ON teachers.id = course_teacher.teacher_id
    JOIN courses ON courses.id = course_teacher.course_id
    JOIN degrees ON degrees.id = courses.degree_id
    JOIN departments ON departments.id = degrees.department_id
    WHERE departments.id = 5
    GROUP BY teachers.id;
```

#### 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql
    SELECT students.name, students.surname, exams.date, exams.hour, exam_student.vote
    FROM students
    JOIN `exam_student` ON students.id = exam_student.student_id
    JOIN `exams` ON exam_student.exam_id = exams.id
    WHERE (exam_student.student_id, exam_student.vote) IN (
        SELECT student_id, MAX(vote) AS max_vote
        FROM exam_student
        GROUP BY student_id
    )
    AND exam_student.vote > 18
    ORDER BY students.name;
```