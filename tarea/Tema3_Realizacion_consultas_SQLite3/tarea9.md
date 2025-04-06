# Code, Learn & Practice (Base de datos - Trabajo con `JOIN` y funciones matemáticas)

## Descripción

En la siguiente tarea se premia el uso de **funciones matemáticas**, así como la **utilización de `JOIN`** en bases de datos.

**Objetivos:**
- Realizar la lectura de la base de datos a través del fichero **base de datos de clientes**.
- Realizar el listado de consultas que se encuentran en el fichero **consultas-bd**.

---

## Requisitos

1. **Uso de funciones matemáticas:**
   - Debes aplicar funciones matemáticas como `AVG()`, `COUNT()`, `SUM()`, `MAX()`, `MIN()`, etc., para realizar cálculos y obtener información relevante de la base de datos.
   
2. **Uso de `JOIN`:**

## base de datos clientes 

```sql
CREATE TABLE IF NOT EXISTS Alumnos (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    edad INTEGER,
    direccion TEXT
);

INSERT INTO Alumnos (nombre, edad, direccion) VALUES
    ('Juan', 20, 'Calle A'),
    ('María', 21, 'Calle B'),
    ('Pedro', 19, 'Calle C'),
    ('Laura', 22, 'Calle D'),
    ('Carlos', 20, 'Calle E'),
    ('Ana', 19, 'Calle F'),
    ('Sofía', 21, 'Calle G'),
    ('Diego', 20, 'Calle H'),
    ('Lucía', 22, 'Calle I'),
    ('Miguel', 19, 'Calle J');

-- Crear tabla para las clases
CREATE TABLE IF NOT EXISTS Clases (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    materia TEXT,
    profesor TEXT
);

INSERT INTO Clases (nombre, materia, profesor) VALUES
    ('Matemáticas 101', 'Matemáticas', 'Profesor X'),
    ('Historia Antigua', 'Historia', 'Profesor Y'),
    ('Literatura Moderna', 'Literatura', 'Profesor Z'),
    ('Biología Avanzada', 'Biología', 'Profesor W'),
    ('Química Orgánica', 'Química', 'Profesor V'),
    ('Física Cuántica', 'Física', 'Profesor U'),
    ('Arte Contemporáneo', 'Arte', 'Profesor T'),
    ('Inglés Avanzado', 'Idiomas', 'Profesor S'),
    ('Economía Internacional', 'Economía', 'Profesor R'),
    ('Derecho Penal', 'Derecho', 'Profesor Q');


CREATE TABLE IF NOT EXISTS Inscripciones (
    id INTEGER PRIMARY KEY,
    id_alumno INTEGER,
    id_clase INTEGER,
    FOREIGN KEY (id_alumno) REFERENCES Alumnos(id),
    FOREIGN KEY (id_clase) REFERENCES Clases(id)
);

INSERT INTO Inscripciones (id_alumno, id_clase) VALUES
    (1, 1), 
    (1, 2), 
    (2, 3), 
    (2, 4), 
    (3, 5), 
    (3, 6), 
    (4, 7), 
    (4, 8), 
    (5, 9), 
    (6, 10);

```
# Consultas SQL para Base de Datos de Alumnos y Clases

## Descripción

En este documento se listan diversas consultas SQL relacionadas con la gestión de alumnos, clases, y profesores. Las consultas están diseñadas para practicar el uso de **`JOIN`** y manipulación de datos a través de SQL.

---

## Consultas

### 1. Obtener el nombre del alumno y el nombre de la clase en la que está inscrito.

```sql
sqlite> SELECT Alumnos.nombre AS alumno, Clases.nombre AS clase
FROM Alumnos
JOIN Inscripciones ON Alumnos.id = Inscripciones.id_alumno
JOIN Clases ON Inscripciones.id_clase = Clases.id;
+--------+------------------------+
| alumno |         clase          |
+--------+------------------------+
| Juan   | Matemáticas 101        |
| Juan   | Historia Antigua       |
| María  | Literatura Moderna     |
| María  | Biología Avanzada      |
| Pedro  | Química Orgánica       |
| Pedro  | Física Cuántica        |
| Laura  | Arte Contemporáneo     |
| Laura  | Inglés Avanzado        |
| Carlos | Economía Internacional |
| Ana    | Derecho Penal          |
+--------+------------------------+

```

### Obtener el nombre del alumno y la materia de las clases en las que está inscrito.

```sql
sqlite> SELECT al.nombre, cl.materia
FROM Alumnos al
INNER JOIN Inscripciones inc ON al.id = inc.id_alumno
INNER JOIN Clases cl ON cl.id = inc.id_clase;
+--------+-------------+
| nombre |   materia   |
+--------+-------------+
| Juan   | Matemáticas |
| Juan   | Historia    |
| María  | Literatura  |
| María  | Biología    |
| Pedro  | Química     |
| Pedro  | Física      |
| Laura  | Arte        |
| Laura  | Idiomas     |
| Carlos | Economía    |
| Ana    | Derecho     |
+--------+-------------+
```
### Obtener el nombre del alumno, la edad y el nombre del profesor de las clases en las que está inscrito.

```sql
sqlite> select al.nombre, al.edad, cl.profesor
from alumnos al
join inscripciones inc on inc.id_alumno = al.id
join clases cl on cl.id = inc.id_clase;
+--------+------+------------+
| nombre | edad |  profesor  |
+--------+------+------------+
| Juan   | 20   | Profesor X |
| Juan   | 20   | Profesor Y |
| María  | 21   | Profesor Z |
| María  | 21   | Profesor W |
| Pedro  | 19   | Profesor V |
| Pedro  | 19   | Profesor U |
| Laura  | 22   | Profesor T |
| Laura  | 22   | Profesor S |
| Carlos | 20   | Profesor R |
| Ana    | 19   | Profesor Q |
+--------+------+------------+



```
### Obtener el nombre del alumno y la dirección de las clases en las que está inscrito.

```sql
sqlite> select al.nombre, al.direccion, cl.nombre as clase_inscriptas
from Alumnos al
join inscripciones inc on al.id = inc.id_alumno
join clases cl on cl.id = inc.id_clase; 
+--------+-----------+------------------------+
| nombre | direccion |    clase_inscriptas    |
+--------+-----------+------------------------+
| Juan   | Calle A   | Matemáticas 101        |
| Juan   | Calle A   | Historia Antigua       |
| María  | Calle B   | Literatura Moderna     |
| María  | Calle B   | Biología Avanzada      |
| Pedro  | Calle C   | Química Orgánica       |
| Pedro  | Calle C   | Física Cuántica        |
| Laura  | Calle D   | Arte Contemporáneo     |
| Laura  | Calle D   | Inglés Avanzado        |
| Carlos | Calle E   | Economía Internacional |
| Ana    | Calle F   | Derecho Penal          |
+--------+-----------+------------------------+

```
### Obtener el nombre del alumno y el nombre de la clase junto con el profesor.

```sql
sqlite> select al.nombre, cl.nombre as nombre_de_clase, cl.profesor as nombre_profesor
from alumnos al
join inscripciones inc on inc.id_alumno = al.id
join clases cl on cl.id = inc.id_clase;
+--------+------------------------+-----------------+
| nombre |    nombre_de_clase     | nombre_profesor |
+--------+------------------------+-----------------+
| Juan   | Matemáticas 101        | Profesor X      |
| Juan   | Historia Antigua       | Profesor Y      |
| María  | Literatura Moderna     | Profesor Z      |
| María  | Biología Avanzada      | Profesor W      |
| Pedro  | Química Orgánica       | Profesor V      |
| Pedro  | Física Cuántica        | Profesor U      |
| Laura  | Arte Contemporáneo     | Profesor T      |
| Laura  | Inglés Avanzado        | Profesor S      |
| Carlos | Economía Internacional | Profesor R      |
| Ana    | Derecho Penal          | Profesor Q      |
+--------+------------------------+-----------------+

```

- Obtener el nombre del alumno, la materia y el nombre del profesor de las clases en las que está inscrito.

```sql
sqlite> select al.nombre, cl.materia, cl.profesor
from alumnos al
join inscripciones inc on inc.id_alumno = al.id
join clases cl on cl.id = inc.id_clase;
+--------+-------------+------------+
| nombre |   materia   |  profesor  |
+--------+-------------+------------+
| Juan   | Matemáticas | Profesor X |
| Juan   | Historia    | Profesor Y |
| María  | Literatura  | Profesor Z |
| María  | Biología    | Profesor W |
| Pedro  | Química     | Profesor V |
| Pedro  | Física      | Profesor U |
| Laura  | Arte        | Profesor T |
| Laura  | Idiomas     | Profesor S |
| Carlos | Economía    | Profesor R |
| Ana    | Derecho     | Profesor Q |
+--------+-------------+------------+

```

- Obtener el nombre del alumno, la edad y la materia de las clases en las que está inscrito.
- Obtener el nombre del alumno, la dirección y el profesor de las clases en las que está inscrito.
- 
## Obtener el nombre del alumno y la materia de las clases en las que está inscrito, ordenado por el nombre del alumno.

```sql
select al.nombre, cl.materia
from alumnos al
join inscripciones inc on inc.id_alumno = al.id
join clases cl on cl.id = inc.id_clase
order by al.nombre ;
+--------+-------------+
| nombre |   materia   |
+--------+-------------+
| Ana    | Derecho     |
| Carlos | Economía    |
| Juan   | Matemáticas |
| Juan   | Historia    |
| Laura  | Arte        |
| Laura  | Idiomas     |
| María  | Literatura  |
| María  | Biología    |
| Pedro  | Química     |
| Pedro  | Física      |
+--------+-------------+

```
- Contar cuántos alumnos están inscritos en cada clase.


## Ejercicios propuestos mios 

## Obtener el nombre del alumno, el nombre de la clase y la materia, pero solo para aquellos alumnos que están inscritos en clases de la materia 'Matemáticas'.
```sql
sqlite> select al.nombre, cl.nombre as nombre_clase, cl.materia
from alumnos al 
join inscripciones inc on inc.id_alumno = al.id
join clases cl on cl.id = inc.id_clase
where cl.materia = "Matemáticas";
+--------+-----------------+-------------+
| nombre |  nombre_clase   |   materia   |
+--------+-----------------+-------------+
| Juan   | Matemáticas 101 | Matemáticas |
+--------+-----------------+-------------+
```

## Obtener el nombre del alumno y el nombre del profesor de las clases en las que están inscritos los alumnos mayores de 18 años.

select al.nombre, cl.nombre as nombre_profesor
from alumnos al
join inscripciones inc on inc.id_alumno = al.id
join clases cl on cl.id = inc.id_clase
where al.edad > 18;
+--------+------------------------+
| nombre |    nombre_profesor     |
+--------+------------------------+
| Juan   | Matemáticas 101        |
| Juan   | Historia Antigua       |
| María  | Literatura Moderna     |
| María  | Biología Avanzada      |
| Pedro  | Química Orgánica       |
| Pedro  | Física Cuántica        |
| Laura  | Arte Contemporáneo     |
| Laura  | Inglés Avanzado        |
| Carlos | Economía Internacional |
| Ana    | Derecho Penal          |
+--------+------------------------+

## Obtener el número total de alumnos inscritos en cada clase. El resultado debe mostrar el nombre de la clase y el número de alumnos.

```sql
sqlite> SELECT cl.nombre AS clase, COUNT(inc.id_alumno) AS numero_de_alumnos
FROM Clases cl
INNER JOIN Inscripciones inc ON cl.id = inc.id_clase
GROUP BY cl.id;
+------------------------+-------------------+
|         clase          | numero_de_alumnos |
+------------------------+-------------------+
| Matemáticas 101        | 1                 |
| Historia Antigua       | 1                 |
| Literatura Moderna     | 1                 |
| Biología Avanzada      | 1                 |
| Química Orgánica       | 1                 |
| Física Cuántica        | 1                 |
| Arte Contemporáneo     | 1                 |
| Inglés Avanzado        | 1                 |
| Economía Internacional | 1                 |
| Derecho Penal          | 1                 |
+------------------------+-------------------+
```

