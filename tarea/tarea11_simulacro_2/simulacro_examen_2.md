<div align="justify">

# Code, Learn & Practice("Simulacro consultas bbdd 2")



## Objetivo

### Consultas Básicas (8 consultas - 1.6 puntos)

1. Listar todos los libros disponibles.
   > **Pista**: Select *

```sql

 select *
from libro;

+----+-----------------------------------+------------------------+-----------------+-----------------+------------+
| id |              titulo               |         autor          |     genero      | año_publicacion | disponible |
+----+-----------------------------------+------------------------+-----------------+-----------------+------------+
| 1  | El Quijote                        | Miguel de Cervantes    | Clásico         | 1605            | 1          |
| 2  | Cien años de soledad              | Gabriel García Márquez | Realismo mágico | 1967            | 0          |
| 3  | 1984                              | George Orwell          | Ciencia ficción | 1949            | 1          |
| 4  | Orgullo y prejuicio               | Jane Austen            | Romance         | 1813            | 0          |
| 5  | La sombra del viento              | Carlos Ruiz Zafón      | Misterio        | 2001            | 1          |
| 6  | Rayuela                           | Julio Cortázar         | Experimental    | 1963            | 0          |
| 7  | Ficciones                         | Jorge Luis Borges      | Cuentos         | 1944            | 1          |
| 8  | Los pilares de la Tierra          | Ken Follett            | Histórica       | 1989            | 0          |
| 9  | El amor en los tiempos del cólera | Gabriel García Márquez | Romance         | 1985            | 1          |
| 10 | La casa de los espíritus          | Isabel Allende         | Realismo mágico | 1982            | 0          |
+----+-----------------------------------+------------------------+-----------------+-----------------+------------+
```

 
2. Mostrar socios de Madrid ordenados por apellido.
   > **Pista**: order. 

```sql
   select s.*
   from socio s
   where s.ciudad = 'Madrid'
   order by s.apellido1;

   +----+--------+-----------+-----------+--------+------------+-----------+
| id | nombre | apellido1 | apellido2 | ciudad | fecha_alta | categoria |
+----+--------+-----------+-----------+--------+------------+-----------+
| 1  | Laura  | García    | Martínez  | Madrid | 2020-03-15 | A         |
| 5  | Elena  | Martín    | Díaz      | Madrid | 2023-02-18 | B         |
+----+--------+-----------+-----------+--------+------------+-----------+
```  
3. Libros publicados después de 1950
      > **Pista**: where

```sql

select l.* 
from libro l
where l.año_publicacion > 1950;

+----+-----------------------------------+------------------------+-----------------+-----------------+------------+
| id |              titulo               |         autor          |     genero      | año_publicacion | disponible |
+----+-----------------------------------+------------------------+-----------------+-----------------+------------+
| 2  | Cien años de soledad              | Gabriel García Márquez | Realismo mágico | 1967            | 0          |
| 5  | La sombra del viento              | Carlos Ruiz Zafón      | Misterio        | 2001            | 1          |
| 6  | Rayuela                           | Julio Cortázar         | Experimental    | 1963            | 0          |
| 8  | Los pilares de la Tierra          | Ken Follett            | Histórica       | 1989            | 0          |
| 9  | El amor en los tiempos del cólera | Gabriel García Márquez | Romance         | 1985            | 1          |
| 10 | La casa de los espíritus          | Isabel Allende         | Realismo mágico | 1982            | 0          |
+----+-----------------------------------+------------------------+-----------------+-----------------+------------+

```
4. Bibliotecarios con más de 3 años de antigüedad
      > **Pista**: saber la fecha actual

```sql
select *
from bibliotecario
where antiguedad > 3;

+----+-----------+-----------+-----------+------------+
| id |  nombre   | apellido1 | apellido2 | antiguedad |
+----+-----------+-----------+-----------+------------+
| 1  | Daniel    | Vázquez   | Gil       | 5          |
| 4  | Lucía     | Reyes     | Martín    | 7          |
| 6  | Isabel    | Morales   | Iglesias  | 4          |
| 7  | Francisco | Santana   | Méndez    | 6          |
+----+-----------+-----------+-----------+------------+

```
5. Préstamos realizados en 2023
      > **Pista**: where like|Expresion regular

```sql
select p.fecha_prestamo, l.titulo
from prestamo p
inner join libro l on l.id = p.id_libro
where fecha_devolucion regexp '^2023-\d{2}-\d{2}';
--------------------------------------------------------

select p.fecha_prestamo, l.titulo
from prestamo p, libro l
where l.id = p.id_libro
and fecha_devolucion regexp '^2023-\d{2}-\d{2}';

+----------------+--------------------------+
| fecha_prestamo |          titulo          |
+----------------+--------------------------+
| 2023-01-10     | Cien años de soledad     |
| 2023-02-15     | Orgullo y prejuicio      |
| 2023-04-05     | Los pilares de la Tierra |
| 2023-01-22     | Cien años de soledad     |
| 2023-02-18     | Orgullo y prejuicio      |
| 2023-04-10     | Los pilares de la Tierra |
| 2023-01-05     | El Quijote               |
| 2023-02-10     | 1984                     |
| 2023-04-20     | Ficciones                |
+----------------+--------------------------+

```

6. Socios sin segundo apellido.
      > **Pista**: Apellido2 = NULL

```sql
select *
from socio
where apellido2 is null;

+----+----------+-----------+-----------+-----------+------------+-----------+
| id |  nombre  | apellido1 | apellido2 |  ciudad   | fecha_alta | categoria |
+----+----------+-----------+-----------+-----------+------------+-----------+
| 3  | Ana      | Sánchez   |           | Valencia  | 2022-01-10 | C         |
| 9  | Patricia | Romero    |           | Barcelona | 2023-01-15 | A         |
+----+----------+-----------+-----------+-----------+------------+-----------+

```
7. Libros del género "Realismo mágico"
      > **Pista**: Where

```sql
select *
from libro
where genero = 'Realismo mágico';

+----+--------------------------+------------------------+-----------------+-----------------+------------+
| id |          titulo          |         autor          |     genero      | año_publicacion | disponible |
+----+--------------------------+------------------------+-----------------+-----------------+------------+
| 2  | Cien años de soledad     | Gabriel García Márquez | Realismo mágico | 1967            | 0          |
| 10 | La casa de los espíritus | Isabel Allende         | Realismo mágico | 1982            | 0          |
+----+--------------------------+------------------------+-----------------+-----------------+------------+

```
8. Préstamos no devueltos. 
   > **Pista**: fecha_devolucion = NULL

```sql
select pre.*, l.titulo
from prestamo pre
inner join libro l on l.id = pre.id_libro
where pre.fecha_devolucion is null; 

+----+----------------+------------------+----------+----------+-----------------------------------+
| id | fecha_prestamo | fecha_devolucion | id_socio | id_libro |              titulo               |
+----+----------------+------------------+----------+----------+-----------------------------------+
| 3  | 2023-03-20     |                  | 5        | 6        | Rayuela                           |
| 5  | 2023-05-12     |                  | 4        | 10       | La casa de los espíritus          |
| 8  | 2023-03-25     |                  | 8        | 6        | Rayuela                           |
| 10 | 2023-05-15     |                  | 10       | 10       | La casa de los espíritus          |
| 13 | 2023-03-15     |                  | 3        | 5        | La sombra del viento              |
| 15 | 2023-05-25     |                  | 5        | 9        | El amor en los tiempos del cólera |
+----+----------------+------------------+----------+----------+-----------------------------------+

```
### Consultas Multitabla (WHERE) (8 consultas - 2.4 puntos)

1. Préstamos con nombres de socio y libro (sin JOIN)
      > **Pista**: where id claves tablas.

```sql
select s.nombre, l.titulo
from prestamo pre, libro l, socio s
where pre.id_libro = l.id
and s.id = pre.id_socio
and pre.fecha_devolucion is null;

+---------+-----------------------------------+
| nombre  |              titulo               |
+---------+-----------------------------------+
| Elena   | Rayuela                           |
| David   | La casa de los espíritus          |
| Miguel  | Rayuela                           |
| Antonio | La casa de los espíritus          |
| Ana     | La sombra del viento              |
| Elena   | El amor en los tiempos del cólera |
+---------+-----------------------------------+

```
2. Libros prestados a socios de Barcelona (sin JOIN)
      > **Pista**: where id claves tablas.

```sql 
select s.nombre
from prestamo pre, socio s
where s.id = pre.id_socio
and s.ciudad = 'Barcelona';
+----------+
|  nombre  |
+----------+
| Carlos   |
| Patricia |
| Carlos   |
+----------+

select s.nombre, s.ciudad
from prestamo pre, socio s
where s.id = pre.id_socio
and s.ciudad = 'Barcelona';
+----------+-----------+
|  nombre  |  ciudad   |
+----------+-----------+
| Carlos   | Barcelona |
| Patricia | Barcelona |
| Carlos   | Barcelona |
+----------+-----------+

```
3. Socios que han tomado prestado "Cien años de soledad" (sin JOIN)
      > **Pista**: where id claves tablas and edad

```sql
select s.nombre
from prestamo pre, socio s, libro l
where pre.id_socio = s.id
and pre.id_libro = l.id
and titulo = 'Cien años de soledad';

+--------+
| nombre |
+--------+
| Laura  |
| Javier |
+--------+

select s.nombre
from prestamo pre,socio s, libro l
where pre.id_socio = s.id
and pre.id_libro = l.id
and l.id = (select l.id
            from libro l
            where l.titulo = 'Cien años de soledad');

+--------+
| nombre |
+--------+
| Laura  |
| Javier |
+--------+

```
4. Bibliotecarios que han gestionado préstamos (sin JOIN)
      > **Pista**: where id claves tablas.

```sql



```
5. Préstamos con retraso.
      > **Pista**: where id claves tablas && fecha_devolucion > fecha_prestamo + 14 días.

```sql
select titulo
from libro l, prestamo p
where l.id = p.id_libro 
and id_libro in ( SELECT 
                        id_libro
                        FROM prestamo
                        WHERE JULIANDAY(fecha_devolucion) - JULIANDAY(fecha_prestamo) > 14);

```
6. Socios que nunca han tomado prestado un libro (sin LEFT JOIN)
      > **Pista**: where id claves tablas.

```sql

select s.id, s.nombre
from socio s, prestamo p, libro l
where s.id = p.id_socio 
and l.id = p.id_libro
and p.id_libro is null;



select id_socio
from prestamo 
where id_socio is null;

```

7. Libros más prestados (sin JOIN)
      > **Pista**: where id claves tablas and top

```sql
select 
```
8. Autores cuyos libros han sido prestados (sin JOIN)
      > **Pista**: where id claves tablas.

```sql

```

### Consultas Multitabla (JOIN) (8 consultas - 2.4 puntos)

1. Préstamos con nombres de socio y libro.
   > **Pista**: JOIN.
2. Libros prestados a socios de Barcelona.
   > **Pista**: JOIN.
3. Socios que han tomado prestado "Cien años de soledad".
   > **Pista**: JOIN.
4. Bibliotecarios que han gestionado préstamos.
   > **Pista**: JOIN.
5. Préstamos con datos completos (socio, libro, bibliotecario)
6. Socios con sus préstamos activos.
   > **Pista**: JOIN.
7. Libros nunca prestados.
   > **Pista**: LEFT|RIGHT JOIN en función del orden de las tablas.
8. Autores con número de libros prestados.
   > **Pista**: JOIN + GROUP BY.

## Consultas Resumen (8 consultas - 2.4 puntos)

1. Número de socios por ciudad.
2. Promedio de antigüedad de bibliotecarios.
3. Cantidad de préstamos por mes en 2023.
4. Libros más populares (por veces prestados).
5. Socios más activos (por préstamos realizados).
6. Porcentaje de libros disponibles.
7. Días promedio de préstamo.
8. Número de préstamos por categoría de socio.

### Subconsultas (8 consultas - 1.2 puntos)

1. Socios que han prestado libros de Gabriel García Márquez.
  > **Pista**: WHERE + IN|EXIST.
1. Libros con préstamos superiores al promedio.
     > **Pista**: WHERE + > + AVG .
2. Socios con todos los préstamos devueltos a tiempo.
     > **Pista**: WHERE + IN|EXIST.
3. Bibliotecarios que no han gestionado préstamos.
     > **Pista**: WHERE + IN|EXIST O NOT IN|EXIST.
4. Socios que han prestado más libros que el promedio.
      > **Pista**: WHERE + > + AVG .
5. Libros disponibles que nunca han sido prestados.
   > **Pista**: WHERE + NOT IN|EXIST.
6. Socios con préstamos en todas las categorías de libros.
   > **Pista**: WHERE + IN|EXIST.
7. Bibliotecarios que han gestionado préstamos de todos los socios de Madrid.
   > **Pista**: WHERE + IN|EXIST.
</div>