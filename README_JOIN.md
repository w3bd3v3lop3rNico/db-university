1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `degrees`.`name`, `students`.`name` 
FROM `students` 
INNER JOIN `degrees` 
ON `degrees`.`id`=`students`.`degree_id` 
WHERE `degrees`.`name` LIKE 'Corso di Laurea in Economia'

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

    SELECT `departments`.`name`, `degrees`.`name` FROM `departments` 
    INNER JOIN `degrees` 
    ON `departments`.`id`=`degrees`.`department_id` 
    WHERE `degrees`.`name` LIKE 'Corso di Laurea Magistrale%' 
    AND `departments`.`id`= 7;

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

    SELECT `courses`.`name`, `courses`.`id`
    FROM `teachers`
    INNER JOIN `course_teacher`
    ON `teachers`.`id`=`course_teacher`.`teacher_id`
    INNER JOIN `courses`
    ON `course_teacher`.`course_id`=`courses`.`id`
    WHERE `teachers`.`id`= 44;

    SELECT `teachers`.`name`, `courses`.`name`
    FROM `teachers`
    INNER JOIN `course_teacher`
    ON `teachers`.`id`=`course_teacher`.`teacher_id`
    INNER JOIN `courses`
    ON `course_teacher`.`course_id`=`courses`.`id`
    WHERE `teachers`.`id`= 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

    SELECT `students`.`surname`,`students`.`name`, `students`.`id`, `degrees`.`name`, `departments`.`name`
    FROM `students`  
    INNER JOIN `degrees`
    ON `students`.`degree_id`=`degrees`.`id`
    INNER JOIN `departments`
    ON `degrees`.`department_id`=`departments`.`id`
    ORDER BY `students`.`surname` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

    SELECT `degrees`.`name`, `courses`.`name`, `teachers`.`name`
    FROM `degrees`
    INNER JOIN `courses`
    ON `degrees`.`id`=`courses`.`degree_id`
    INNER JOIN `course_teacher`
    ON `courses`.`id`=`course_teacher`.`course_id`
    INNER JOIN `teachers`
    ON `course_teacher`.`teacher_id`=`teachers`.`id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

    SELECT DISTINCT `teachers`.`name`
    FROM `teachers`
    INNER JOIN `course_teacher`
    ON `teachers`.`id`=`course_teacher`.`teacher_id`
    INNER JOIN `courses`
    ON `course_teacher`.`course_id`= `courses`.`id`
    INNER JOIN `degrees`
    ON `courses`.`degree_id`=`degrees`.`id`
    INNER JOIN `departments`
    ON `degrees`.`department_id`=`departments`.`id`
    WHERE `departments`.`id`= 5;

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.