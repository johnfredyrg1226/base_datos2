
# Code, Learn & Practice("Simulacro de bbdd 🧪: Consultas, Índices, Vistas, Funciones y Procedimientos")

🧾 Contexto
Como analista de datos en una universidad, se te ha encargado la explotación de una base de datos que permita gestionar estudiantes, profesores, cursos y matrículas. Además, deberás demostrar habilidades en consultas SQL, índices, vistas, procedimientos y funciones. Si la base de datos no estuvira creada, a continuación tienes el init.sql.

Base de datos en docker
Crea una carpeta y añade el fichero docker-compose.yml y el directorio docker-init.

Ejecuta a continuación el siguiente comando:

docker compose up -d
Obtendrar una salida similar a la siguiente:

 docker compose up -d
[+] Running 2/2
 ✔ Container adminer_container  Started                                                                                                             0.9s
 ✔ Container mysql_container    Started
A continuación ejecuta el siguiente comando:

docker exec -it mysql_container mysql -u root -p
Indica el password que es bae.

A continuación debes de estar dentro de la consola:

....
....
....
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
IMPORTANTE: Para salir de la consola se debe de ejecutar exit.

Verifica las bases de datos que tienes cargadas: (SHOW DATABASES;)

SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| bae                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| universidad        |
+--------------------+
6 rows in set (0.00 sec)
Usa la base de datos universidad: (use universidad;)

use universidad;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
También podemos acceder a través del navegador. Para ello utilizaremos Adminer porque simula la línea de comandos, y nos ayuda a aprender. Una vez que accedas a <http://localhost:8099>, Adminer te pedirá los siguientes datos:

Puedes consultar la documentación aquí.

Sistema: MySQL
Servidor: db
Es el nombre del servicio del contenedor MySQL dentro del mismo docker-compose (Adminer y MySQL están en la misma red db-network).
Usuario: bae
Contraseña: bae
Lee atentamente cada una de los puntos y cuestiones y realiza.

## Parte 1: Consultas SQL

## A. Consultas Simples

**Mostrar todos los cursos disponibles.**

```sql
mysql> select * from cursos;
+----+----------------------+-------------+----------+
| id | nombre               | profesor_id | creditos |
+----+----------------------+-------------+----------+
|  1 | �lgebra Lineal       |           1 |        6 |
|  2 | Programaci�n I       |           2 |        5 |
|  3 | Mec�nica Cl�sica     |           3 |        6 |
|  4 | Estructuras de Datos |           2 |        5 |
|  5 | C�lculo I            |           1 |        6 |
+----+----------------------+-------------+----------+
```

## Mostrar el nombre de todos los profesores.

```sql
mysql> select nombre from profesores;
+-----------------+
| nombre          |
+-----------------+
| Dra. Ana Torres |
| Dr. Luis G�mez  |
| Dra. Marta D�az |
+-----------------+
```

## Listar todas las matrículas.

```sql
mysql> select * from matriculas;
+----+---------------+----------+------------+
| id | estudiante_id | curso_id | fecha      |
+----+---------------+----------+------------+
|  1 |             1 |        1 | 2021-09-01 |
|  2 |             2 |        2 | 2022-09-01 |
|  3 |             3 |        3 | 2023-09-02 |
|  4 |             4 |        4 | 2024-09-03 |
|  5 |             1 |        5 | 2020-09-04 |
|  6 |             2 |        4 | 2022-09-05 |
|  7 |             3 |        1 | 2023-09-06 |
|  8 |             4 |        2 | 2024-09-06 |
+----+---------------+----------+------------+

```

## Ver los nombres y correos de los estudiantes.

```sql

mysql> select nombre, email from estudiantes;
+-----------------+----------------+
| nombre          | email          |
+-----------------+----------------+
| Mar�a L�pez     | maria@uni.edu  |
| Juan P�rez      | juan@uni.edu   |
| Luc�a Fern�ndez | lucia@uni.edu  |
| Carlos Ruiz     | carlos@uni.edu |
+-----------------+----------------+
```

## Ver los cursos y su número de créditos.

```sql
mysql> select nombre, creditos from cursos;
+----------------------+----------+
| nombre               | creditos |
+----------------------+----------+
| �lgebra Lineal       |        6 |
| Programaci�n I       |        5 |
| Mec�nica Cl�sica     |        6 |
| Estructuras de Datos |        5 |
| C�lculo I            |        6 |
+----------------------+----------+

```

## B. Consultas con WHERE. Obligatorio utilizar WHERE donde se combine dos o más tablas

## Obtener los cursos impartidos por profesores del departamento de Informática.

```sql
mysql> select c.nombre from cursos c, profesores p where p.departamento = 'Informatica';
+----------------------+
| nombre               |
+----------------------+
| �lgebra Lineal       |
| Programaci�n I       |
| Mec�nica Cl�sica     |
| Estructuras de Datos |
| C�lculo I            |
+----------------------+
```

## Obtener los estudiantes que viven en Madrid.

```sql
select e.nombre from estudiantes e where e.ciudad = 'Madrid';sql
+-------------+
| nombre      |
+-------------+
| Mar�a L�pez |
+-------------+

```

## Mostrar los cursos con más de 5 créditos.

```sql
mysql> select * from cursos c where c.creditos >= 0;
+----+----------------------+-------------+----------+
| id | nombre               | profesor_id | creditos |
+----+----------------------+-------------+----------+
|  1 | �lgebra Lineal       |           1 |        6 |
|  2 | Programaci�n I       |           2 |        5 |
|  3 | Mec�nica Cl�sica     |           3 |        6 |
|  4 | Estructuras de Datos |           2 |        5 |
|  5 | C�lculo I            |           1 |        6 |
+----+----------------------+-------------+----------+
```

## Ver las matrículas realizadas después del año 2022.

```sql
select * from matriculas where fecha > '2022-12-31';
+----+---------------+----------+------------+
| id | estudiante_id | curso_id | fecha      |
+----+---------------+----------+------------+
|  3 |             3 |        3 | 2023-09-02 |
|  4 |             4 |        4 | 2024-09-03 |
|  7 |             3 |        1 | 2023-09-06 |
|  8 |             4 |        2 | 2024-09-06 |
+----+---------------+----------+------------+

```

## Ver los cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
+----+----------------+-------------+----------+----+-----------------+--------------+
| id | nombre         | profesor_id | creditos | id | nombre          | departamento |
+----+----------------+-------------+----------+----+-----------------+--------------+
|  1 | �lgebra Lineal |           1 |        6 |  1 | Dra. Ana Torres | Matem�ticas  |
|  5 | C�lculo I      |           1 |        6 |  1 | Dra. Ana Torres | Matem�ticas  |
+----+----------------+-------------+----------+----+-----------------+--------------+

```

## C. Consultas con JOIN. Obligatorio utilizar JOIN donde se combine dos o más tablas

## (Devuelven el mismo resultado que las anteriores, pero usando combinaciones de tablas)

## Mostrar cursos impartidos por profesores del departamento de Informática.

```sql
mysql> select c.nombre from cursos c join profesores p on p.id = c.profesor_id and p.departamento = 'Informatica';

+----------------------+
| nombre               |
+----------------------+
| Programaci�n I       |
| Estructuras de Datos |
+----------------------+
```

## Obtener estudiantes que viven en Madrid.ss

no se puede porque no conecta dostablas

## Mostrar cursos con más de 5 créditos.

no se puede conectar dos tablas.

## Listar matrículas realizadas después del año 2022.

```sql
select * 
from matriculas where fecha > '2022-12-31';
```

## Mostrar los cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
+----------------+
| nombre         |
+----------------+
| �lgebra Lineal |
| C�lculo I      |
+----------------+
```

## D. Consultas con Subconsultas

## (Devuelven el mismo resultado que las anteriores, pero usando subconsultas)

## Cursos impartidos por profesores del departamento de Informática.

```sql
select c.nombre
from cursos c, profesores pro 
where pro.nombre = (select p.nombre
					from profesores p
					where p.departamento REGEXP 'Informática');
+----------------------+
| nombre               |
+----------------------+
| �lgebra Lineal       |
| Programaci�n I       |
| Mec�nica Cl�sica     |
| Estructuras de Datos |
| C�lculo I            |
+----------------------+

```

## Estudiantes que viven en Madrid.

```sql
select es.nombre
from estudiantes es
where es.ciudad = (select e.ciudad
					from estudiantes e 
					where e.ciudad REGEXP '^M');

+-------------+
| nombre      |
+-------------+
| Mar�a L�pez |
+-------------+

```

## Cursos con más de 5 créditos.

```sql
SELECT * FROM cursos WHERE id IN ( SELECT id FROM cursos WHERE creditos > 5 );
+----+------------------+-------------+----------+
| id | nombre           | profesor_id | creditos |
+----+------------------+-------------+----------+
|  1 | �lgebra Lineal   |           1 |        6 |
|  3 | Mec�nica Cl�sica |           3 |        6 |
|  5 | C�lculo I        |           1 |        6 |
+----+------------------+-------------+----------+


```
## Matrículas realizadas después del año 2022.

## Cursos impartidos por la profesora “Dra. Ana Torres”.

## Parte 2: Índices

## Crear un índice en la columna ciudad de la tabla estudiantes. 

**Crear un índice en la columna departamento de la tabla profesores.
Consultar los índices creados.
Eliminar ambos índices.**

```sql
create index idx_ciudad on estudiantes(ciudad);
create index idx_departamento on profesores(departamento);

mysql> show INDEX from estudiantes;
+-------------+------------+------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table       | Non_unique | Key_name   | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+-------------+------------+------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| estudiantes |          0 | PRIMARY    |            1 | id          | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
| estudiantes |          1 | idx_ciudad |            1 | ciudad      | A         |           4 |     NULL | NULL   | YES  | BTREE      |         |               |
+-------------+------------+------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+


+------------+------------+------------------+--------------+--------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table      | Non_unique | Key_name         | Seq_in_index | Column_name  | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+------------+------------+------------------+--------------+--------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| profesores |          0 | PRIMARY          |            1 | id           | A         |           3 |     NULL | NULL   |      | BTREE      |         |               |
| profesores |          1 | idx_departamento |            1 | departamento | A         |           3 |     NULL | NULL   | YES  | BTREE      |         |               |
+------------+------------+------------------+--------------+--------------+-----------+-------------+----------+--------+------+------------+---------+---------------+

```

## 🪞 Parte 3: Vistas

Crear una vista llamada vista_matriculas_completas que muestre:
nombre del estudiante,
nombre del curso,
fecha de la matrícula.
Consultar datos desde la vista, mostrando el nombre del estudiante y la fecha de matrícula.
Eliminar la vista.

```sql
drop view if exists vista_matriculas;
create view vista_matriculas as select e.nombre as nombre_estudiante , c.nombre as nombre_curso , m.fecha as fecha_matricula from estudiantes e inner join matriculas m on e.id = m.estudiante_id inner join cursos c on c.id = m.curso_id;

select nombre_estudiante, fecha_matricula from vista_matriculas;

+-------------------+-----------------+
| nombre_estudiante | fecha_matricula |
+-------------------+-----------------+
| Mar�a L�pez       | 2021-09-01      |
| Juan P�rez        | 2022-09-01      |
| Luc�a Fern�ndez   | 2023-09-02      |
| Carlos Ruiz       | 2024-09-03      |
| Mar�a L�pez       | 2020-09-04      |
| Juan P�rez        | 2022-09-05      |
| Luc�a Fern�ndez   | 2023-09-06      |
| Carlos Ruiz       | 2024-09-06      |
+-------------------+-----------------+

drop VIEW vista_matriculas;
```

## ⚙ Parte 4: Procedimiento Almacenado

Crear un procedimiento llamado cursos_por_profesor que reciba el nombre del profesor como parámetro y devuelva los cursos que imparte y su número de créditos.
Ejecutar el procedimiento con el nombre “Dr. Luis Gómez”.
Eliminar el procedimiento.

```sql
drop PROCEDURE if EXISTS curso_por_profesor;

DELIMITER $$s
CREATE PROCEDURE curso_por_profesor(in nombre_pro varchar(50))
BEGIN
   		select c.nombre as nombre _del_curso, c.creditos
        from cursos c 
        inner join profesores p on p.id = c.profesor_id
        where p.nombre = nombre_pro ;
END $$
DELIMITER ; 

call curso_por_profesor('Dr. Luis Gómez');

```

## 🔢 Parte 5: Función Definida por el Usuario

Crear una función llamada total_creditos_estudiante que reciba el ID de un estudiante y devuelva el total de créditos que ha matriculado.
Ejecutar la función para un estudiante específico.
Eliminar la función.

```sql

drop FUNCTION if exists total_creditos_estudiante;

DELIMITER $$
create FUNCTION total_creditos_estudiante(id_estudiante int)
 RETURNS int 
 BEGIN
        DECLARE total int;
        
        select sum(c.creditos) into total
            from matriculas m  
            inner join cursos c ON m.curso_id = c.id
            where m.estudiante_id = id_estudiante;
 
 		RETURN IFNULL(total, 0);
 END $$
 DELIMITER ;


 SELECT total_creditos_estudiante(3);

 drop FUNCTION if exists total_creditos_estudiante;
```