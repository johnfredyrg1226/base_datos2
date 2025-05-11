## Tarea 1 de trabajo con índices

**Un instituto de enseñanza guarda los siguientes datos de sus alumnos:**

**número de inscripción, comienza desde 1 cada año,
año de inscripción,
nombre del alumno,
documento del alumno,
domicilio,
ciudad,
provincia,
clave primaria: número de inscripto y año de inscripción.
Se pide:**



#### 1.Elimine la tabla "alumno" si existe.
**Nota:Muestra el comando y la salida.**

```sql

mysql> drop table if exists alumno;

```

#### 2.Cree la tabla definiendo una clave primaria compuesta (año de inscripción y número de inscripción).
**Nota:Muestra el comando y la salida.**

```sql
mysql> 
drop table if exists alumno;

create table alumno(
    ->     numero_inscripcion int not null,
    ->     anio_inscripcion int not null,
    ->     nombre_alumno varchar(100) not null,
    ->     documento varchar(20) not null,
    ->     domicilio varchar(255) not null,
    ->     ciudad varchar(100) not null,
    ->     provincia varchar(100) not null,
    ->     primary key (numero_inscripcion, anio_inscripcion)
    ->     );
Query OK, 0 rows affected (0.01 sec)

mysql> 

```

##### Define los siguientes indices:
**Un índice único por el campo "documento" y un índice común por ciudad y provincia.
Nota:Muestra el comando y la salida. Justifica el tipo de indice en un comentario.**

```sql
mysql>  create unique index idx_documento on alumno (documento);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0


** El tipo de indice es unique ya que no deja que se dupliquen numeros en la columna y son unicos


mysql> create index idx_ciudad_provincia on alumno (ciudad, provincia);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0


** El tipo de indice seria compuesto o multicolumna asi se filtran los datos utilizando 
varias columnas, se suelen utilizar con el where. ejemplo:select * from alumno where ciudad = 'valor1' and provincia = 'valor2';

```

#### Vea los índices de la tabla.
**Nota:Muestra el comando y la salida "show index".**

```sql
mysql> show index from alumno;
+--------+------------+----------------------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table  | Non_unique | Key_name             | Seq_in_index | Column_name        | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+--------+------------+----------------------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| alumno |          0 | PRIMARY              |            1 | numero_inscripcion | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          0 | PRIMARY              |            2 | anio_inscripcion   | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          0 | idx_documento        |            1 | documento          | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          1 | idx_ciudad_provincia |            1 | ciudad             | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          1 | idx_ciudad_provincia |            2 | provincia          | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
+--------+------------+----------------------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+


```

#### Intente ingresar un alumno con clave primaria repetida.
**Nota:Muestra el comando y la salida.**

```sql
Para hacer este apartada dobo de insertar un alumno.

mysql> insert into alumno(
    ->     numero_inscripcion,
    ->     anio_inscripcion,
    ->     nombre_alumno,
    ->     documento,
    ->     domicilio,
    ->     ciudad,
    ->     provincia
    -> ) values(
    ->     1,2025,'john','12345678X','calle el mar 11','madrid','madrid'
    -> );
Query OK, 1 row affected (0.01 sec)

se hace un select...

mysql> select * from alumno;
+--------------------+------------------+---------------+-----------+-----------------+--------+-----------+
| numero_inscripcion | anio_inscripcion | nombre_alumno | documento | domicilio       | ciudad | provincia |
+--------------------+------------------+---------------+-----------+-----------------+--------+-----------+
|                  1 |             2025 | john          | 12345678X | calle el mar 11 | madrid | madrid    |
+--------------------+------------------+---------------+-----------+-----------------+--------+-----------+

ahora se inserta otro alumno conla clave primaria igual.

mysql> insert into alumno(
    ->     numero_inscripcion,
    ->     anio_inscripcion,
    ->     nombre_alumno,
    ->     documento,
    ->     domicilio,
    ->     ciudad,
    ->     provincia
    -> ) values(
    ->     1,2025,'David','87654321X','calle madrid 11','madrid','madrid'
    -> );
ERROR 1062 (23000): Duplicate entry '1-2025' for key 'PRIMARY'

```


#### Intente ingresar un alumno con documento repetido.
**Nota:Muestra el comando y la salida.***

```SQL
mysql> insert into alumno(
    ->     numero_inscripcion,
    ->     anio_inscripcion,
    ->     nombre_alumno,
    ->     documento,
    ->     domicilio,
    ->     ciudad,
    ->     provincia
    -> ) values(
    ->     2,2025,'David','12345678X','calle madrid 11','madrid','madrid'
    -> );
ERROR 1062 (23000): Duplicate entry '12345678X' for key 'idx_documento'



```

### Ingrese varios alumnos de la misma ciudad y provincia.
**Nota:Muestra el comando y la salida.**

```sql
mysql> insert into alumno(
    ->     numero_inscripcion,
    ->     anio_inscripcion,
    ->     nombre_alumno,
    ->     documento,
    ->     domicilio,
    ->     ciudad,
    ->     provincia
    -> ) values
    ->     (6,2025,'Fran','12345678T','calle mendez 3','madrid','madrid'),
    ->     (7,2020,'Esa','12365487H','calle junior 1','madrid','madrid'),
    ->     (8,2020,'Audry','87652314D','calle candelaria','madrid','madrid');
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0

no sale nada ya que es correcta.
mysql> select * from alumno;
+--------------------+------------------+---------------+-----------+------------------+--------+-----------+
| numero_inscripcion | anio_inscripcion | nombre_alumno | documento | domicilio        | ciudad | provincia |
+--------------------+------------------+---------------+-----------+------------------+--------+-----------+
|                  1 |             2025 | john          | 12345678X | calle el mar 11  | madrid | madrid    |
|                  6 |             2025 | Fran          | 12345678T | calle mendez 3   | madrid | madrid    |
|                  7 |             2020 | Esa           | 12365487H | calle junior 1   | madrid | madrid    |
|                  8 |             2020 | Audry         | 87652314D | calle candelaria | madrid | madrid    |
+--------------------+------------------+---------------+-----------+------------------+--------+-----------+

```

Elimina los indices creados, y muestra que ya no se encuentran.
Nota:Muestra el comando y la salida.

```sql
Muestro los indices. 
mysql> show index from alumno;
+--------+------------+----------------------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table  | Non_unique | Key_name             | Seq_in_index | Column_name        | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+--------+------------+----------------------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| alumno |          0 | PRIMARY              |            1 | numero_inscripcion | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          0 | PRIMARY              |            2 | anio_inscripcion   | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          0 | idx_documento        |            1 | documento          | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          1 | idx_ciudad_provincia |            1 | ciudad             | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          1 | idx_ciudad_provincia |            2 | provincia          | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
+--------+------------+----------------------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+

Los índices ayudan en consultas con WHERE, JOIN, ORDER BY y GROUP BY.

EXPLAIN QUERY PLAN -- como saber si esta usuando el indice -- 
SELECT * FROM cliente WHERE documento = '12345678A';


y los elimino 

mysql> drop index idx_documento on alumno;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> drop index idx_ciudad_provincia on alumno;
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0


mysql> show index from alumno;
+--------+------------+----------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table  | Non_unique | Key_name | Seq_in_index | Column_name        | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+--------+------------+----------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| alumno |          0 | PRIMARY  |            1 | numero_inscripcion | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
| alumno |          0 | PRIMARY  |            2 | anio_inscripcion   | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
+--------+------------+----------+--------------+--------------------+-----------+-------------+----------+--------+------+------------+---------+---------------+



```