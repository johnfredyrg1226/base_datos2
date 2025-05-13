
# Base de datos Universidad

```sql

-- Crear la base de datos
CREATE DATABASE universidad;
USE universidad;

-- Crear tabla de carreras
CREATE TABLE carreras (
    id_carrera INT PRIMARY KEY,
    nombre_carrera VARCHAR(100)
);

-- Crear tabla de estudiantes
CREATE TABLE estudiantes (
    id_estudiante INT PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT,
    carrera_id INT,
    FOREIGN KEY (carrera_id) REFERENCES carreras(id_carrera)
);

-- Crear tabla de materias
CREATE TABLE materias (
    id_materia INT PRIMARY KEY,
    nombre_materia VARCHAR(100),
    carrera_id INT,
    FOREIGN KEY (carrera_id) REFERENCES carreras(id_carrera)
);

-- Crear tabla de notas
CREATE TABLE notas (
    id_nota INT PRIMARY KEY,
    estudiante_id INT,
    materia_id INT,
    nota INT,
    FOREIGN KEY (estudiante_id) REFERENCES estudiantes(id_estudiante),
    FOREIGN KEY (materia_id) REFERENCES materias(id_materia)
);

-- Insertar datos en carreras
INSERT INTO carreras (id_carrera, nombre_carrera) VALUES
(1, 'Ingeniería'),
(2, 'Psicología'),
(3, 'Administración');

-- Insertar datos en estudiantes
INSERT INTO estudiantes (id_estudiante, nombre, edad, carrera_id) VALUES
(1, 'Ana Torres', 21, 1),
(2, 'Luis Gómez', 22, 2),
(3, 'Carla Fernández', 20, 1),
(4, 'Mario Pérez', 23, 3),
(5, 'Sofia Ramírez', 24, 2);

-- Insertar datos en materias
INSERT INTO materias (id_materia, nombre_materia, carrera_id) VALUES
(1, 'Matemáticas I', 1),
(2, 'Psicología Social', 2),
(3, 'Finanzas', 3),
(4, 'Programación', 1),
(5, 'Neurociencia', 2);

-- Insertar datos en notas
INSERT INTO notas (id_nota, estudiante_id, materia_id, nota) VALUES
(1, 1, 1, 85),
(2, 1, 4, 92),
(3, 2, 2, 78),
(4, 3, 1, 88),
(5, 3, 4, 91),
(6, 4, 3, 72),
(7, 5, 5, 89);

```


## ¿Cuál es el nombre del estudiante que tiene la nota más alta en toda la base de datos?

```sql
select e.nombre
from estudiantes e, notas n
where e.id_estudiante = n.estudiante_id
and n.nota = (
    select max(nota)
    from notas);
```

## ¿Cuál es el nombre del estudiante que ha obtenido el promedio más alto de notas en todas las materias?

```sql
SELECT e.nombre
FROM estudiantes e
WHERE e.id_estudiante = (
    SELECT n.estudiante_id
    FROM notas n
    GROUP BY n.estudiante_id
    ORDER BY AVG(n.nota) DESC
    LIMIT 1
);

```

## ¿Qué estudiantes tienen una nota mayor al promedio general de su carrera?

```sql
select avg(n.nota) as promedio_nota, ca.nombre_carrera
from estudiantes es
inner join carreras ca on ca.id_carrera = es.carrera_id
inner join notas n on n.estudiante_id = es.id_estudiante
group by ca.nombre_carrera;



respuesta;

SELECT DISTINCT e.nombre
FROM estudiantes e
JOIN notas n ON e.id_estudiante = n.estudiante_id
JOIN carreras c ON e.carrera_id = c.id_carrera
WHERE n.nota > (
    SELECT AVG(n2.nota)
    FROM estudiantes e2
    JOIN notas n2 ON e2.id_estudiante = n2.estudiante_id
    WHERE e2.carrera_id = e.carrera_id
);

```

## ¿Qué estudiantes están inscritos en la carrera de “Ingeniería”?

```sql
select e.nombre
from estudiantes e, carreras c
where c.nombre_carrera = 'Ingeniería';
```

## ¿Cuáles son los nombres y edades de los estudiantes que pertenecen a la carrera de Ingeniería?

```sql
select e.nombre, e.edad 
from estudiantes e,carreras c
where e.carrera_id = c.id_carrera
and c.nombre_carrera = "ingenieria";

select e.nombre, e.edad
from estudiantes e
inner join carreras c on e.carrera_id = c.id_carrera
where c.nombre_carrera = "ingenieria";

+-----------------+
| nombre          |
+-----------------+
| Ana Torres      |
| Carla Fern�ndez |
+-----------------+
```

## ¿Qué materias se dictan en la carrera de Psicología?

```sql
select m.nombre_materia 
from materias m, carreras c
where m.carrera_id = c.id_carrera 
and c.nombre_carrera = "Psicologia";

select m.nombre_materia
from materias m
inner join carreras c on m.carrera_id = c.id_carrera
where c.nombre_carrera = "Psicologia";

+-------------------+
| nombre_materia    |
+-------------------+
| Psicolog�a Social |
| Neurociencia      |
+-------------------+
```

## ¿Qué estudiantes tienen al menos una nota mayor a 90?

```sql
select e.nombre, n.nota
from notas n, estudiantes e
where n.estudiante_id = e.id_estudiante
and n.nota > 90;

select e.nombre, n.nota
from notas n 
inner join estudiantes e on n.estudiante_id = e.id_estudiante
where n.nota > 90;

+-----------------+------+
| nombre          | nota |
+-----------------+------+
| Ana Torres      |   92 |
| Carla Fern�ndez |   91 |
+-----------------+------+

```

## Subconsulta en SELECT, Muestra el nombre de cada estudiante junto con su promedio de notas.

```sql
select e.nombre, avg(n.nota) as promedio_notas
from notas n, estudiantes e
where n.estudiante_id = e.id_estudiante
group by e.nombre;

SELECT 
    e.nombre, 
    (SELECT AVG(n.nota) 
     FROM notas n 
     WHERE n.estudiante_id = e.id_estudiante) AS promedio_notas
FROM estudiantes e;


+-----------------+----------------+
| nombre          | promedio_notas |
+-----------------+----------------+
| Ana Torres      |        88.5000 |
| Luis G�mez      |        78.0000 |
| Carla Fern�ndez |        89.5000 |
| Mario P�rez     |        72.0000 |
| Sofia Ram�rez   |        89.0000 |
+-----------------+----------------+
```

## Subconsulta en FROM
**Pregunta:**

### ¿Cuáles son los estudiantes que tienen un promedio de notas superior a 85?

```sql
select e.nombre, avg(n.nota) as promedio
from notas n
inner join estudiantes e on e.id_estudiante = n.estudiante_id
group by e.nombre
having promedio > 85;


SELECT s.nombre, s.promedio
FROM (
    SELECT e.id_estudiante, e.nombre, AVG(n.nota) AS promedio
    FROM estudiantes e
    INNER JOIN notas n ON e.id_estudiante = n.estudiante_id
    GROUP BY e.id_estudiante, e.nombre
) AS s
WHERE s.promedio > 85;

+-----------------+----------+
| nombre          | promedio |
+-----------------+----------+
| Ana Torres      |  88.5000 |
| Carla Fern�ndez |  89.5000 |
| Sofia Ram�rez   |  89.0000 |
+-----------------+----------+

```

## Subconsulta con IN o EXISTS

**Muestra los nombres de los estudiantes que han cursado materias de la carrera de Ingeniería.**

```sql
SELECT DISTINCT e.nombre
FROM estudiantes e
JOIN notas n ON e.id_estudiante = n.estudiante_id
WHERE EXISTS (
    SELECT 1
    FROM materias m
    JOIN carreras c ON c.id_carrera = m.carrera_id
    WHERE m.id_materia = n.materia_id
    AND c.nombre_carrera = 'Ingeniería'
);
```

## Ejercicio 7: Subconsulta con ALL o ANY

**Muestra los nombres de los estudiantes cuya nota es mayor que todas las notas obtenidas por los estudiantes de la carrera de Psicología.**

```sql

select distinct es.nombre
from estudiantes es
inner join notas nn on nn.estudiante_id = es.id_estudiante
where nn.nota > all (select n.nota
                    from estudiantes e
                    inner join notas n on e.id_estudiante = n.estudiante_id
                    inner join materias m on m.id_materia = n.materia_id 
                    where m.nombre_materia = "Psicologia social");

+-----------------+
| nombre          |
+-----------------+
| Ana Torres      |
| Carla Fern�ndez |
| Sofia Ram�rez   |
+-----------------+
```


        