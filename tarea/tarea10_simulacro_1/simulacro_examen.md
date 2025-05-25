-- ----------------------------------------
-- Consultas sobre una tabla
-- 0,2 puntos la correcta. Total = 1,4 puntos
-- ----------------------------------------

## 1.- Devuelve un listado con todos las compras que se han realizado. Las compras deben estar ordenados

```sql
```

```sql
sqlite> select * from compra;
+----+---------+------------+---------------+------------------+
| id |  total  |   fecha    | id_consumidor | id_suministrador |
+----+---------+------------+---------------+------------------+
| 1  | 150.5   | 2020-10-05 | 5             | 2                |
| 2  | 270.65  | 2019-09-10 | 1             | 5                |
| 3  | 65.26   | 2020-10-05 | 2             | 1                |
| 4  | 110.5   | 2019-08-17 | 8             | 3                |
| 5  | 948.5   | 2020-09-10 | 5             | 2                |
| 6  | 2400.6  | 2019-07-27 | 7             | 1                |
| 7  | 5760.0  | 2018-09-10 | 2             | 1                |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                |
| 9  | 2480.4  | 2019-10-10 | 8             | 3                |
| 10 | 250.45  | 2018-06-27 | 8             | 2                |
| 11 | 75.29   | 2019-08-17 | 3             | 7                |
| 12 | 3045.6  | 2020-04-25 | 2             | 1                |
| 13 | 545.75  | 2022-01-25 | 6             | 1                |
| 14 | 145.82  | 2020-02-02 | 6             | 1                |
| 15 | 370.85  | 2022-03-11 | 1             | 5                |
| 16 | 2389.23 | 2022-03-11 | 1             | 5                |
+----+---------+------------+---------------+------------------+
```

## -- por la fecha de realización, mostrando en primer lugar las compras más recientes.

```sql
sqlite> select * from compra
   ...> order by fecha desc;
+----+---------+------------+---------------+------------------+
| id |  total  |   fecha    | id_consumidor | id_suministrador |
+----+---------+------------+---------------+------------------+
| 15 | 370.85  | 2022-03-11 | 1             | 5                |
| 16 | 2389.23 | 2022-03-11 | 1             | 5                |
| 13 | 545.75  | 2022-01-25 | 6             | 1                |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                |
| 1  | 150.5   | 2020-10-05 | 5             | 2                |
| 3  | 65.26   | 2020-10-05 | 2             | 1                |
| 5  | 948.5   | 2020-09-10 | 5             | 2                |
| 12 | 3045.6  | 2020-04-25 | 2             | 1                |
| 14 | 145.82  | 2020-02-02 | 6             | 1                |
| 9  | 2480.4  | 2019-10-10 | 8             | 3                |
| 2  | 270.65  | 2019-09-10 | 1             | 5                |
| 4  | 110.5   | 2019-08-17 | 8             | 3                |
| 11 | 75.29   | 2019-08-17 | 3             | 7                |
| 6  | 2400.6  | 2019-07-27 | 7             | 1                |
| 7  | 5760.0  | 2018-09-10 | 2             | 1                |
| 10 | 250.45  | 2018-06-27 | 8             | 2                |
+----+---------+------------+---------------+------------------+
```



## -- 2. Devuelve todos los datos de los dos compras de mayor valor.

```sql
 sqlite>  select * from compra
   order by total desc
  limit 2;
+----+--------+------------+---------------+------------------+
| id | total  |   fecha    | id_consumidor | id_suministrador |
+----+--------+------------+---------------+------------------+
| 7  | 5760.0 | 2018-09-10 | 2             | 1                |
| 12 | 3045.6 | 2020-04-25 | 2             | 1                |
+----+--------+------------+---------------+------------------+
```

-- 3. Devuelve un listado con los identificadores de los consumidores que han realizado algún compra.
- Tenga en cuenta que no debe mostrar identificadores que estén repetidos.


```sql
sqlite> select distinct ( id_consumidor) from compra;
+---------------+
| id_consumidor |
+---------------+
| 5             |
| 1             |
| 2             |
| 8             |
| 7             |
| 4             |
| 3             |
| 6             |
+---------------+
```


-- 4. Devuelve un listado de todos las compras que se realizaron durante el año 2020,
-- cuya cantidad total sea superior a 500€.


```sql
sqlite> select * from compra
where fecha between '2020-01-01' and '2020-12-31'
and total > 500;
+----+---------+------------+---------------+------------------+
| id |  total  |   fecha    | id_consumidor | id_suministrador |
+----+---------+------------+---------------+------------------+
| 5  | 948.5   | 2020-09-10 | 5             | 2                |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                |
| 12 | 3045.6  | 2020-04-25 | 2             | 1                |
+----+---------+------------+---------------+------------------+
```

-- 5. Devuelve un listado con el nombre y los apellidos de los suministradores que tienen una comisión entre 0.11 y 0.15.


```sql
sqlite> select nombre, apellido1, apellido2, categoria
from suministrador
where categoria between 0.11 and 0.15;
+---------+-----------+-----------+-----------+
| nombre  | apellido1 | apellido2 | categoria |
+---------+-----------+-----------+-----------+
| Daniel  | Sáez      | Vega      | 0.15      |
| Juan    | Gómez     | López     | 0.13      |
| Diego   | Flores    | Salas     | 0.11      |
| Marta   | Herrera   | Gil       | 0.14      |
| Antonio | Carretero | Ortega    | 0.12      |
| Manuel  | Domínguez | Hernández | 0.13      |
| Antonio | Vega      | Hernández | 0.11      |
+---------+-----------+-----------+-----------+
```



-- 6. Devuelve el valor de la comisión de mayor valor que existe en la tabla suministrador.


```sql
sqlite> select max(categoria) from suministrador; 
+----------------+
| max(categoria) |
+----------------+
| 0.15           |
+----------------+
```

-- 7. Devuelve el identificador, nombre y primer apellido de aquellos consumidores cuyo segundo apellido no es NULL.
-- El listado deberá estar ordenado alfabéticamente por apellidos y nombre.


```sql
sqlite> select id,nombre,apellido1
from consumidor
where apellido2 is null
order by apellido1 and nombre; 
+----+--------+-----------+
| id | nombre | apellido1 |
+----+--------+-----------+
| 4  | Adrián | Suárez    |
| 7  | Pilar  | Ruiz      |
+----+--------+-----------+

```

## -- (Consultas Multitabla Where)
-- -----------------------------------------------
## -- 0,3 puntos la correcta. Total =  2,1 puntos
-- -----------------------------------------------

## -- 1. Devuelve un listado con el identificador, nombre y los apellidos de todos los consumidores que han realizado algún compra.
**-- El listado debe estar ordenado alfabéticamente y se deben eliminar los elementos repetidos.**


```sql
sqlite> select distinct(con.id), con.nombre,con.apellido1,con.apellido2
from consumidor con, compra c
where c.id_consumidor = con.id
order by con.nombre, con.apellido1, con.apellido2;
+----+--------+-----------+-----------+
| id | nombre | apellido1 | apellido2 |
+----+--------+-----------+-----------+
| 1  | Aarón  | Rivero    | Gómez     |
| 2  | Adela  | Salas     | Díaz      |
| 3  | Adolfo | Rubio     | Flores    |
| 4  | Adrián | Suárez    |           |
| 5  | Marcos | Loyola    | Méndez    |
| 6  | María  | Santana   | Moreno    |
| 8  | Pepe   | Ruiz      | Santana   |
| 7  | Pilar  | Ruiz      |           |
+----+--------+-----------+-----------+
```

## -- 2. Devuelve un listado que muestre todos las compras que ha realizado cada consumidor. 
**-- El resultado debe mostrar todos los datos de las compras y del consumidor. El listado debe mostrar los datos de los consumidores ordenados alfabéticamente.**



```sql
select *
from compra c, consumidor con 
where c.id_consumidor = con.id
group by con.id;

+----+---------+------------+---------------+------------------+----+--------+-----------+-----------+---------+-----------+
| id |  total  |   fecha    | id_consumidor | id_suministrador | id | nombre | apellido1 | apellido2 | ciudad  | categoria |
+----+---------+------------+---------------+------------------+----+--------+-----------+-----------+---------+-----------+
| 2  | 270.65  | 2019-09-10 | 1             | 5                | 1  | Aarón  | Rivero    | Gómez     | Almería | 100       |
| 3  | 65.26   | 2020-10-05 | 2             | 1                | 2  | Adela  | Salas     | Díaz      | Granada | 200       |
| 11 | 75.29   | 2019-08-17 | 3             | 7                | 3  | Adolfo | Rubio     | Flores    | Sevilla |           |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                | 4  | Adrián | Suárez    |           | Jaén    | 300       |
| 1  | 150.5   | 2020-10-05 | 5             | 2                | 5  | Marcos | Loyola    | Méndez    | Almería | 200       |
| 13 | 545.75  | 2022-01-25 | 6             | 1                | 6  | María  | Santana   | Moreno    | Cádiz   | 100       |
| 6  | 2400.6  | 2019-07-27 | 7             | 1                | 7  | Pilar  | Ruiz      |           | Sevilla | 300       |
| 4  | 110.5   | 2019-08-17 | 8             | 3                | 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       |
+----+---------+------------+---------------+------------------+----+--------+-----------+-----------+---------+-----------+
```

## -- 3. Devuelve un listado que muestre todos las compras en los que ha participado un suministrador.
**-- El resultado debe mostrar todos los datos de las compras y de los suministradores.**
**-- El listado debe mostrar los datos de los suministradores ordenados alfabéticamente.**


```sql
sqlite> select * 
from compra c, suministrador sum
where sum.id = c.id_suministrador
group by c.id_suministrador
order by sum.nombre;
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
| id |  total  |   fecha    | id_consumidor | id_suministrador | id | nombre  | apellido1 | apellido2 | categoria |
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
| 2  | 270.65  | 2019-09-10 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      |
| 11 | 75.29   | 2019-08-17 | 3             | 7                | 7  | Antonio | Vega      | Hernández | 0.11      |
| 3  | 65.26   | 2020-10-05 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 4  | 110.5   | 2019-08-17 | 8             | 3                | 3  | Diego   | Flores    | Salas     | 0.11      |
| 1  | 150.5   | 2020-10-05 | 5             | 2                | 2  | Juan    | Gómez     | López     | 0.13      |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                | 6  | Manuel  | Domínguez | Hernández | 0.13      |
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
```

## -- 4. Devuelve un listado que muestre todos los consumidores, con todos las compras que han realizado 
**-- y con los datos de los suministradores asociados a cada compra.**


```sql
sqlite> select * 
from compra c, suministrador sum, consumidor con
where sum.id = c.id_suministrador
and c.id_consumidor = con.id
group by con.id
order by sum.nombre;
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+----+--------+-----------+-----------+---------+-----------+
| id |  total  |   fecha    | id_consumidor | id_suministrador | id | nombre  | apellido1 | apellido2 | categoria | id | nombre | apellido1 | apellido2 | ciudad  | categoria |
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+----+--------+-----------+-----------+---------+-----------+
| 2  | 270.65  | 2019-09-10 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      | 1  | Aarón  | Rivero    | Gómez     | Almería | 100       |
| 11 | 75.29   | 2019-08-17 | 3             | 7                | 7  | Antonio | Vega      | Hernández | 0.11      | 3  | Adolfo | Rubio     | Flores    | Sevilla |           |
| 3  | 65.26   | 2020-10-05 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      | 2  | Adela  | Salas     | Díaz      | Granada | 200       |
| 13 | 545.75  | 2022-01-25 | 6             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      | 6  | María  | Santana   | Moreno    | Cádiz   | 100       |
| 6  | 2400.6  | 2019-07-27 | 7             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      | 7  | Pilar  | Ruiz      |           | Sevilla | 300       |
| 4  | 110.5   | 2019-08-17 | 8             | 3                | 3  | Diego   | Flores    | Salas     | 0.11      | 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       |
| 1  | 150.5   | 2020-10-05 | 5             | 2                | 2  | Juan    | Gómez     | López     | 0.13      | 5  | Marcos | Loyola    | Méndez    | Almería | 200       |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                | 6  | Manuel  | Domínguez | Hernández | 0.13      | 4  | Adrián | Suárez    |           | Jaén    | 300       |
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+----+--------+-----------+-----------+---------+-----------+
```

## -- 5. Devuelve un listado de todos los consumidores que realizaron un compra durante el año 2020,
**-- cuya cantidad esté entre 300 € y 1000 €.**


```sql
sqlite> select * 
from consumidor con, compra c
where con.id = c.id_consumidor
and c.fecha regexp '2020-[0-9]{2}-[0-9]{2}'
and c.total between 300 and 1000;
+----+--------+-----------+-----------+---------+-----------+----+-------+------------+---------------+------------------+
| id | nombre | apellido1 | apellido2 | ciudad  | categoria | id | total |   fecha    | id_consumidor | id_suministrador |
+----+--------+-----------+-----------+---------+-----------+----+-------+------------+---------------+------------------+
| 5  | Marcos | Loyola    | Méndez    | Almería | 200       | 5  | 948.5 | 2020-09-10 | 5             | 2                |
+----+--------+-----------+-----------+---------+-----------+----+-------+------------+---------------+------------------+
```



## -- 6. Devuelve el nombre y los apellidos de todos los suministradores que ha participado en algún compra realizado por María Santana Moreno.


```sql
select sum.nombre, sum.apellido1, sum.apellido2 
from suministrador sum, consumidor con, compra c
where sum.id = c.id_suministrador
and con.id = c.id_consumidor
and con.nombre = 'María' and con.apellido1 = 'Santana';

+--------+-----------+-----------+
| nombre | apellido1 | apellido2 |
+--------+-----------+-----------+
| Daniel | Sáez      | Vega      |
| Daniel | Sáez      | Vega      |
+--------+-----------+-----------+
```


## Se empiesa con la tabla que relaciona las dos siguientes en este caso tabla compra. 


```sql
SELECT sum.nombre, sum.apellido1, sum.apellido2
FROM compra c
INNER JOIN consumidor con ON con.id = c.id_consumidor
INNER JOIN suministrador sum ON sum.id = c.id_suministrador
WHERE con.nombre = 'María' 
  AND con.apellido1 = 'Santana' 
  AND con.apellido2 = 'Moreno';

+--------+-----------+-----------+
| nombre | apellido1 | apellido2 |
+--------+-----------+-----------+
| Daniel | Sáez      | Vega      |
| Daniel | Sáez      | Vega      |
+--------+-----------+-----------+
```




## -- 7. Devuelve el nombre de todos los consumidores que han realizado algún compra con el suministrador Daniel Sáez Vega.


```sql
select con.nombre
from compra c, consumidor con, suministrador sum
where con.id = c.id_consumidor
and sum.id = c.id_suministrador
and c.id_consumidor >= 1 
and sum.nombre = 'Daniel' and sum.apellido1 = 'Sáez' and sum.apellido2 = 'Vega';

+--------+
| nombre |
+--------+
| Adela  |
| Pilar  |
| Adela  |
| Adela  |
| María  |
| María  |
+--------+



select con.nombre
from compra c
inner join suministrador sum on sum.id = c.id_suministrador
inner join consumidor con on con.id = c.id_consumidor
and sum.nombre = 'Daniel' and sum.apellido1 = 'Sáez' and sum.apellido2 = 'Vega';

+--------+
| nombre |
+--------+
| Adela  |
| Pilar  |
| Adela  |
| Adela  |
| María  |
| María  |
+--------+
```



## -- (Consultas Multitabla Join)
-- -----------------------------------------------
**-- 0,3 puntos la correcta. Total = 2,1 puntos**
-- -----------------------------------------------

## -- 1. Devuelve un listado con el identificador, nombre y los apellidos de todos los consumidores que han realizado algún compra.
**-- El listado debe estar ordenado alfabéticamente y se deben eliminar los elementos repetidos.**

```sql
select distinct con.id, con.nombre, con.apellido1, con.apellido2
from compra c
inner join consumidor con on con.id = c.id_consumidor
where c.id_consumidor >= 1 
order by con.nombre asc ;

+----+--------+-----------+-----------+
| id | nombre | apellido1 | apellido2 |
+----+--------+-----------+-----------+
| 1  | Aarón  | Rivero    | Gómez     |
| 2  | Adela  | Salas     | Díaz      |
| 3  | Adolfo | Rubio     | Flores    |
| 4  | Adrián | Suárez    |           |
| 5  | Marcos | Loyola    | Méndez    |
| 6  | María  | Santana   | Moreno    |
| 8  | Pepe   | Ruiz      | Santana   |
| 7  | Pilar  | Ruiz      |           |
+----+--------+-----------+-----------+
```





## -- 2. Devuelve un listado que muestre todos las compras que ha realizado cada consumidor. 
**-- El resultado debe mostrar todos los datos de las compras y del consumidor. El listado debe mostrar los datos de los consumidores ordenados alfabéticamente.**


```sql
select *, con.nombre, con.apellido1, con.apellido2 
from compra c
inner join consumidor con on con.id = c.id_consumidor 
order by con.apellido1, con.apellido2, con.nombre;


+----+---------+------------+---------------+------------------+----+--------+-----------+-----------+---------+-----------+--------+-----------+-----------+
| id |  total  |   fecha    | id_consumidor | id_suministrador | id | nombre | apellido1 | apellido2 | ciudad  | categoria | nombre | apellido1 | apellido2 |
+----+---------+------------+---------------+------------------+----+--------+-----------+-----------+---------+-----------+--------+-----------+-----------+
| 1  | 150.5   | 2020-10-05 | 5             | 2                | 5  | Marcos | Loyola    | Méndez    | Almería | 200       | Marcos | Loyola    | Méndez    |
| 5  | 948.5   | 2020-09-10 | 5             | 2                | 5  | Marcos | Loyola    | Méndez    | Almería | 200       | Marcos | Loyola    | Méndez    |
| 2  | 270.65  | 2019-09-10 | 1             | 5                | 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | Aarón  | Rivero    | Gómez     |
| 15 | 370.85  | 2022-03-11 | 1             | 5                | 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | Aarón  | Rivero    | Gómez     |
| 16 | 2389.23 | 2022-03-11 | 1             | 5                | 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | Aarón  | Rivero    | Gómez     |
| 11 | 75.29   | 2019-08-17 | 3             | 7                | 3  | Adolfo | Rubio     | Flores    | Sevilla |           | Adolfo | Rubio     | Flores    |
| 6  | 2400.6  | 2019-07-27 | 7             | 1                | 7  | Pilar  | Ruiz      |           | Sevilla | 300       | Pilar  | Ruiz      |           |
| 4  | 110.5   | 2019-08-17 | 8             | 3                | 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | Pepe   | Ruiz      | Santana   |
| 9  | 2480.4  | 2019-10-10 | 8             | 3                | 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | Pepe   | Ruiz      | Santana   |
| 10 | 250.45  | 2018-06-27 | 8             | 2                | 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | Pepe   | Ruiz      | Santana   |
| 3  | 65.26   | 2020-10-05 | 2             | 1                | 2  | Adela  | Salas     | Díaz      | Granada | 200       | Adela  | Salas     | Díaz      |
| 7  | 5760.0  | 2018-09-10 | 2             | 1                | 2  | Adela  | Salas     | Díaz      | Granada | 200       | Adela  | Salas     | Díaz      |
| 12 | 3045.6  | 2020-04-25 | 2             | 1                | 2  | Adela  | Salas     | Díaz      | Granada | 200       | Adela  | Salas     | Díaz      |
| 13 | 545.75  | 2022-01-25 | 6             | 1                | 6  | María  | Santana   | Moreno    | Cádiz   | 100       | María  | Santana   | Moreno    |
| 14 | 145.82  | 2020-02-02 | 6             | 1                | 6  | María  | Santana   | Moreno    | Cádiz   | 100       | María  | Santana   | Moreno    |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                | 4  | Adrián | Suárez    |           | Jaén    | 300       | Adrián | Suárez    |           |
+----+---------+------------+---------------+------------------+----+--------+-----------+-----------+---------+-----------+--------+-----------+-----------+
sqlite> SELECT c.*, con.nombre, con.apellido1, con.apellido2
FROM compra c
INNER JOIN consumidor con ON con.id = c.id_consumidor
ORDER BY con.nombre, con.apellido1, con.apellido2;
+----+---------+------------+---------------+------------------+--------+-----------+-----------+
| id |  total  |   fecha    | id_consumidor | id_suministrador | nombre | apellido1 | apellido2 |
+----+---------+------------+---------------+------------------+--------+-----------+-----------+
| 2  | 270.65  | 2019-09-10 | 1             | 5                | Aarón  | Rivero    | Gómez     |
| 15 | 370.85  | 2022-03-11 | 1             | 5                | Aarón  | Rivero    | Gómez     |
| 16 | 2389.23 | 2022-03-11 | 1             | 5                | Aarón  | Rivero    | Gómez     |
| 3  | 65.26   | 2020-10-05 | 2             | 1                | Adela  | Salas     | Díaz      |
| 7  | 5760.0  | 2018-09-10 | 2             | 1                | Adela  | Salas     | Díaz      |
| 12 | 3045.6  | 2020-04-25 | 2             | 1                | Adela  | Salas     | Díaz      |
| 11 | 75.29   | 2019-08-17 | 3             | 7                | Adolfo | Rubio     | Flores    |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                | Adrián | Suárez    |           |
| 1  | 150.5   | 2020-10-05 | 5             | 2                | Marcos | Loyola    | Méndez    |
| 5  | 948.5   | 2020-09-10 | 5             | 2                | Marcos | Loyola    | Méndez    |
| 13 | 545.75  | 2022-01-25 | 6             | 1                | María  | Santana   | Moreno    |
| 14 | 145.82  | 2020-02-02 | 6             | 1                | María  | Santana   | Moreno    |
| 4  | 110.5   | 2019-08-17 | 8             | 3                | Pepe   | Ruiz      | Santana   |
| 9  | 2480.4  | 2019-10-10 | 8             | 3                | Pepe   | Ruiz      | Santana   |
| 10 | 250.45  | 2018-06-27 | 8             | 2                | Pepe   | Ruiz      | Santana   |
| 6  | 2400.6  | 2019-07-27 | 7             | 1                | Pilar  | Ruiz      |           |
+----+---------+------------+---------------+------------------+--------+-----------+-----------+
```


sqlite> SELECT c.*, co.* 
FROM consumidor c JOIN compra co ON c.id = co.id_consumidor 
ORDER BY c.apellido1, c.apellido2, c.nombre;

+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+
| id | nombre | apellido1 | apellido2 | ciudad  | categoria | id |  total  |   fecha    | id_consumidor | id_suministrador |
+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+
| 5  | Marcos | Loyola    | Méndez    | Almería | 200       | 1  | 150.5   | 2020-10-05 | 5             | 2                |
| 5  | Marcos | Loyola    | Méndez    | Almería | 200       | 5  | 948.5   | 2020-09-10 | 5             | 2                |
| 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | 2  | 270.65  | 2019-09-10 | 1             | 5                |
| 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | 15 | 370.85  | 2022-03-11 | 1             | 5                |
| 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | 16 | 2389.23 | 2022-03-11 | 1             | 5                |
| 3  | Adolfo | Rubio     | Flores    | Sevilla |           | 11 | 75.29   | 2019-08-17 | 3             | 7                |
| 7  | Pilar  | Ruiz      |           | Sevilla | 300       | 6  | 2400.6  | 2019-07-27 | 7             | 1                |
| 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | 4  | 110.5   | 2019-08-17 | 8             | 3                |
| 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | 9  | 2480.4  | 2019-10-10 | 8             | 3                |
| 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | 10 | 250.45  | 2018-06-27 | 8             | 2                |
| 2  | Adela  | Salas     | Díaz      | Granada | 200       | 3  | 65.26   | 2020-10-05 | 2             | 1                |
| 2  | Adela  | Salas     | Díaz      | Granada | 200       | 7  | 5760.0  | 2018-09-10 | 2             | 1                |
| 2  | Adela  | Salas     | Díaz      | Granada | 200       | 12 | 3045.6  | 2020-04-25 | 2             | 1                |
| 6  | María  | Santana   | Moreno    | Cádiz   | 100       | 13 | 545.75  | 2022-01-25 | 6             | 1                |
| 6  | María  | Santana   | Moreno    | Cádiz   | 100       | 14 | 145.82  | 2020-02-02 | 6             | 1                |
| 4  | Adrián | Suárez    |           | Jaén    | 300       | 8  | 1983.43 | 2020-10-10 | 4             | 6                |
+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+



## -- 3. Devuelve un listado que muestre todos las compras en los que ha participado un suministrador.
**-- El resultado debe mostrar todos los datos de las compras y de los suministradores.
-- El listado debe mostrar los datos de los suministradores ordenados alfabéticamente.**


```sql
SELECT c.*, sum.*
FROM compra c
 inner join suministrador sum on sum.id = c.id_suministrador
ORDER BY sum.apellido1, sum.apellido2, sum.nombre asc;

+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
| id |  total  |   fecha    | id_consumidor | id_suministrador | id | nombre  | apellido1 | apellido2 | categoria |
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
| 2  | 270.65  | 2019-09-10 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      |
| 15 | 370.85  | 2022-03-11 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      |
| 16 | 2389.23 | 2022-03-11 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      |
| 8  | 1983.43 | 2020-10-10 | 4             | 6                | 6  | Manuel  | Domínguez | Hernández | 0.13      |
| 4  | 110.5   | 2019-08-17 | 8             | 3                | 3  | Diego   | Flores    | Salas     | 0.11      |
| 9  | 2480.4  | 2019-10-10 | 8             | 3                | 3  | Diego   | Flores    | Salas     | 0.11      |
| 1  | 150.5   | 2020-10-05 | 5             | 2                | 2  | Juan    | Gómez     | López     | 0.13      |
| 5  | 948.5   | 2020-09-10 | 5             | 2                | 2  | Juan    | Gómez     | López     | 0.13      |
| 10 | 250.45  | 2018-06-27 | 8             | 2                | 2  | Juan    | Gómez     | López     | 0.13      |
| 3  | 65.26   | 2020-10-05 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 6  | 2400.6  | 2019-07-27 | 7             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 7  | 5760.0  | 2018-09-10 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 12 | 3045.6  | 2020-04-25 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 13 | 545.75  | 2022-01-25 | 6             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 14 | 145.82  | 2020-02-02 | 6             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 11 | 75.29   | 2019-08-17 | 3             | 7                | 7  | Antonio | Vega      | Hernández | 0.11      |
+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+


```


## -- 4. Devuelve un listado que muestre todos los consumidores, con todos las compras que han realizado 
**-- y con los datos de los suministradores asociados a cada compra.**


```sql
select cons.*, c.*,su.*
from consumidor cons
inner join compra c on c.id_consumidor = cons.id
inner join suministrador su on su.id = c.id_suministrador;


+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
| id | nombre | apellido1 | apellido2 | ciudad  | categoria | id |  total  |   fecha    | id_consumidor | id_suministrador | id | nombre  | apellido1 | apellido2 | categoria |
+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
| 5  | Marcos | Loyola    | Méndez    | Almería | 200       | 1  | 150.5   | 2020-10-05 | 5             | 2                | 2  | Juan    | Gómez     | López     | 0.13      |
| 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | 2  | 270.65  | 2019-09-10 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      |
| 2  | Adela  | Salas     | Díaz      | Granada | 200       | 3  | 65.26   | 2020-10-05 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | 4  | 110.5   | 2019-08-17 | 8             | 3                | 3  | Diego   | Flores    | Salas     | 0.11      |
| 5  | Marcos | Loyola    | Méndez    | Almería | 200       | 5  | 948.5   | 2020-09-10 | 5             | 2                | 2  | Juan    | Gómez     | López     | 0.13      |
| 7  | Pilar  | Ruiz      |           | Sevilla | 300       | 6  | 2400.6  | 2019-07-27 | 7             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 2  | Adela  | Salas     | Díaz      | Granada | 200       | 7  | 5760.0  | 2018-09-10 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 4  | Adrián | Suárez    |           | Jaén    | 300       | 8  | 1983.43 | 2020-10-10 | 4             | 6                | 6  | Manuel  | Domínguez | Hernández | 0.13      |
| 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | 9  | 2480.4  | 2019-10-10 | 8             | 3                | 3  | Diego   | Flores    | Salas     | 0.11      |
| 8  | Pepe   | Ruiz      | Santana   | Huelva  | 200       | 10 | 250.45  | 2018-06-27 | 8             | 2                | 2  | Juan    | Gómez     | López     | 0.13      |
| 3  | Adolfo | Rubio     | Flores    | Sevilla |           | 11 | 75.29   | 2019-08-17 | 3             | 7                | 7  | Antonio | Vega      | Hernández | 0.11      |
| 2  | Adela  | Salas     | Díaz      | Granada | 200       | 12 | 3045.6  | 2020-04-25 | 2             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 6  | María  | Santana   | Moreno    | Cádiz   | 100       | 13 | 545.75  | 2022-01-25 | 6             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 6  | María  | Santana   | Moreno    | Cádiz   | 100       | 14 | 145.82  | 2020-02-02 | 6             | 1                | 1  | Daniel  | Sáez      | Vega      | 0.15      |
| 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | 15 | 370.85  | 2022-03-11 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      |
| 1  | Aarón  | Rivero    | Gómez     | Almería | 100       | 16 | 2389.23 | 2022-03-11 | 1             | 5                | 5  | Antonio | Carretero | Ortega    | 0.12      |
+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+----+---------+-----------+-----------+-----------+
```






## -- 5. Devuelve un listado de todos los consumidores que realizaron un compra durante el año 2020,
**-- cuya cantidad esté entre 300 € y 1000 €.**


```sql
SELECT DISTINCT con.id, con.nombre, con.apellido1, con.apellido2
FROM compra c
INNER JOIN consumidor con ON con.id = c.id_consumidor
WHERE c.fecha REGEXP '^2020-[0-9]{2}-[0-9]{2}'
  AND c.total BETWEEN 300 AND 1000
ORDER BY con.nombre, con.apellido1, con.apellido2;

+----+--------+-----------+-----------+
| id | nombre | apellido1 | apellido2 |
+----+--------+-----------+-----------+
| 5  | Marcos | Loyola    | Méndez    |
+----+--------+-----------+-----------+
```



## -- 6. Devuelve el nombre y los apellidos de todos los suministradores que ha participado en algún compra realizado por María Santana Moreno.


```sql
select sum.nombre, sum.apellido1, sum.apellido2
from compra c, consumidor con, suministrador sum
where con.id = c.id_consumidor
and sum.id = c.id_suministrador
and c.id_consumidor >= 1 
and con.nombre = 'María' and con.apellido1 = 'Santana' and con.apellido2 = 'Moreno';


select sum.nombre, sum.apellido1, sum.apellido2
from compra c
inner join consumidor con on con.id = c.id_consumidor
inner join suministrador sum on sum.id = c.id_suministrador
where c.id_consumidor >= 1 
and con.nombre = 'María' and con.apellido1 = 'Santana' and con.apellido2 = 'Moreno';

+--------+-----------+-----------+
| nombre | apellido1 | apellido2 |
+--------+-----------+-----------+
| Daniel | Sáez      | Vega      |
| Daniel | Sáez      | Vega      |
+--------+-----------+-----------+
```

## -- 7. Devuelve el nombre de todos los consumidores que han realizado algún compra con el suministrador Daniel Sáez Vega.

```sql
select distinct con.nombre 
from compra c
inner join suministrador sum on sum.id = c.id_suministrador
inner join consumidor con on con.id = c.id_consumidor 
where c.id_consumidor >= 1 
and sum.nombre = 'Daniel' and sum.apellido1 = 'Sáez' and sum.apellido2 = 'Vega';

+--------+
| nombre |
+--------+
| Adela  |
| Pilar  |
| María  |
+--------+

```



-- ---------------------------
## -- Consultas resumen (funciones)
-- -----------------------------------------------
**-- 0,2 puntos la correcta. (1-6) 1,2 puntos
-- 0,25 puntos la correcta. (7-10) 1 punto.
-- Total = 2,2 puntos**
-- -----------------------------------------------

## -- 1. Calcula la cantidad media de todos las compras que aparecen en la tabla compra.


```sql
select avg(total) as media_compra
from compra ;
+--------------+
| media_compra |
+--------------+
| 1312.051875  |
+--------------+
```


## -- 2. Calcula el número total de suministradores distintos que aparecen en la tabla compra.


```sql
select count(distinct id_suministrador)
from compra;

+----------------------------------+
| count(distinct id_suministrador) |
+----------------------------------+
| 6                                |
+----------------------------------+
```


## -- 3. Calcula el número total de consumidores que aparecen en la tabla consumidor.


```sql
select count(id)
from consumidor;
+-----------+
| count(id) |
+-----------+
| 10        |
+-----------+

```


## -- 4. Calcula cuál es la mayor cantidad que aparece en la tabla compra.


```sql
select max(total)
from compra;
+------------+
| max(total) |
+------------+
| 5760.0     |
+------------+
```



## -- 5. Calcula cuál es el valor máximo de categoría para cada una de las ciudades que aparece en la tabla consumidor.


```sql
select ciudad,max(categoria)
from consumidor
group by ciudad;
+---------+----------------+
| ciudad  | max(categoria) |
+---------+----------------+
| Almería | 200            |
| Cádiz   | 100            |
| Granada | 225            |
| Huelva  | 200            |
| Jaén    | 300            |
| Sevilla | 300            |
+---------+----------------+
```

## -- 6. Calcula cuál es el máximo valor de las compras realizadas durante el mismo día para cada uno de los consumidores.

**-- Es decir, el mismo consumidor puede haber realizado varios compras de diferentes cantidades el mismo día.
-- Se pide que se calcule cuál es el compra de máximo valor para cada uno de los días en los que un consumidor ha realizado un compra.
-- Muestra el identificador del consumidor, nombre, apellidos, la fecha y el valor de la cantidad.**


```sql
select con.id, con.nombre, con.apellido1, con.apellido2, c.fecha , max(c.total) as valor_cantidad
from compra c
inner join consumidor con on con.id = c.id_consumidor
group by c.fecha;

+----+--------+-----------+-----------+------------+----------------+
| id | nombre | apellido1 | apellido2 |   fecha    | valor_cantidad |
+----+--------+-----------+-----------+------------+----------------+
| 8  | Pepe   | Ruiz      | Santana   | 2018-06-27 | 250.45         |
| 2  | Adela  | Salas     | Díaz      | 2018-09-10 | 5760.0         |
| 7  | Pilar  | Ruiz      |           | 2019-07-27 | 2400.6         |
| 8  | Pepe   | Ruiz      | Santana   | 2019-08-17 | 110.5          |
| 1  | Aarón  | Rivero    | Gómez     | 2019-09-10 | 270.65         |
| 8  | Pepe   | Ruiz      | Santana   | 2019-10-10 | 2480.4         |
| 6  | María  | Santana   | Moreno    | 2020-02-02 | 145.82         |
| 2  | Adela  | Salas     | Díaz      | 2020-04-25 | 3045.6         |
| 5  | Marcos | Loyola    | Méndez    | 2020-09-10 | 948.5          |
| 5  | Marcos | Loyola    | Méndez    | 2020-10-05 | 150.5          |
| 4  | Adrián | Suárez    |           | 2020-10-10 | 1983.43        |
| 6  | María  | Santana   | Moreno    | 2022-01-25 | 545.75         |
| 1  | Aarón  | Rivero    | Gómez     | 2022-03-11 | 2389.23        |
+----+--------+-----------+-----------+------------+----------------+
```


## -- 7. Calcula cuál es el máximo valor de las compras realizadas durante el mismo día para cada uno de los consumidores,
**-- teniendo en cuenta que sólo queremos mostrar aquellas compras que superen la cantidad de 2000 €.**



```sql
select con.nombre, max(c.total) as compras_realizadas, c.fecha
from compra c
inner join consumidor con on con.id = c.id_consumidor
where c.total > 2000
group by c.fecha, c.id_consumidor;

+--------+--------------------+------------+
| nombre | compras_realizadas |   fecha    |
+--------+--------------------+------------+
| Adela  | 5760.0             | 2018-09-10 |
| Pilar  | 2400.6             | 2019-07-27 |
| Pepe   | 2480.4             | 2019-10-10 |
| Adela  | 3045.6             | 2020-04-25 |
| Aarón  | 2389.23            | 2022-03-11 |
+--------+--------------------+------------+
```




## -- 8. Calcula el máximo valor de las compras realizadas para cada uno de los suministradores durante la fecha 2020-08-17.
**-- Muestra el identificador del suministrador, nombre, apellidos y total.**


```sql
select sum.nombre,sum.apellido1, sum.apellido2, max(distinct c.total) as maximo_valor_compra
from compra c
inner join suministrador sum on sum.id = c.id_suministrador
where c.fecha = '2018-08-17'
order by sum.id;

+--------+-----------+-----------+---------------------+
| nombre | apellido1 | apellido2 | maximo_valor_compra |
+--------+-----------+-----------+---------------------+
|        |           |           |                     |
+--------+-----------+-----------+---------------------+
no sale nada no  hay nadie con la fecha indicada
```





## -- 9. Devuelve un listado con el identificador de consumidor, nombre y apellidos y el número total de compras que ha realizado cada uno de consumidores.

**-- Tenga en cuenta que pueden existir consumidores que no han realizado ninguna compra.
-- Estos consumidores también deben aparecer en el listado indicando que el número de compras realizadas es 0.**


```sql
select con.nombre, con.apellido1, con.apellido2, count(c.id_consumidor) as total_compras
from compra c
right join consumidor con on con.id = c.id_consumidor
group by c.id_consumidor;

+-----------+-----------+-----------+---------------+
|  nombre   | apellido1 | apellido2 | total_compras |
+-----------+-----------+-----------+---------------+
| Guillermo | López     | Gómez     | 0             |
| Aarón     | Rivero    | Gómez     | 3             |
| Adela     | Salas     | Díaz      | 3             |
| Adolfo    | Rubio     | Flores    | 1             |
| Adrián    | Suárez    |           | 1             |
| Marcos    | Loyola    | Méndez    | 2             |
| María     | Santana   | Moreno    | 2             |
| Pilar     | Ruiz      |           | 1             |
| Pepe      | Ruiz      | Santana   | 3             |
+-----------+-----------+-----------+---------------+
```




## -- 10. Devuelve un listado con el identificador de consumidor, nombre y apellidos y el número total de compras que ha realizado cada uno de consumidores durante el año 2020.


```sql
select c.id_consumidor, con.nombre, con.apellido1, con.apellido2, count(c.id_consumidor)
from compra c
inner join consumidor con on con.id = c.id_consumidor
where fecha regexp '^2020-\d{2}-\d{2}$'
group by c.id_consumidor;

+---------------+--------+-----------+-----------+------------------------+
| id_consumidor | nombre | apellido1 | apellido2 | count(c.id_consumidor) |
+---------------+--------+-----------+-----------+------------------------+
| 2             | Adela  | Salas     | Díaz      | 2                      |
| 4             | Adrián | Suárez    |           | 1                      |
| 5             | Marcos | Loyola    | Méndez    | 2                      |
| 6             | María  | Santana   | Moreno    | 1                      |
+---------------+--------+-----------+-----------+------------------------+
```




-- ---------------------
## -- Subconsultas
-- -----------------------------------------------
**-- 0,2 puntos la correcta (1-5).
-- 0,3 puntos la correcta (6-9).
-- Total = 2,2 puntos**
-- -----------------------------------------------

**--- Con operadores básicos de comparación**

## -- 1. Devuelve un listado con todos las compras que ha realizado Adela Salas Díaz. (Sin utilizar INNER JOIN).


```sql
select c.*, con.*
from compra c
inner join consumidor con on con.id = c.id_consumidor
where con.nombre = 'Adela' and  con.apellido1 = 'Salas' and  con.apellido2 = 'Díaz';


select c.*
from compra c
where id_consumidor = (select id from consumidor con
                        where con.nombre = 'Adela' and  con.apellido1 = 'Salas' and  con.apellido2 = 'Díaz');

+----+--------+------------+---------------+------------------+
| id | total  |   fecha    | id_consumidor | id_suministrador |
+----+--------+------------+---------------+------------------+
| 3  | 65.26  | 2020-10-05 | 2             | 1                |
| 7  | 5760.0 | 2018-09-10 | 2             | 1                |
| 12 | 3045.6 | 2020-04-25 | 2             | 1                |
+----+--------+------------+---------------+------------------+
```



## -- 2. Devuelve la fecha y la cantidad del compra de menor valor realizado por el cliente Pepe Ruiz Santana.


```sql
select c.fecha, min(c.total) as minima_compra
from compra c
where id_consumidor = (select id 
                      from consumidor con
                       where con.nombre = 'Pepe' and  con.apellido1 = 'Ruiz' and  con.apellido2 = 'Santana');

+------------+---------------+
|   fecha    | minima_compra |
+------------+---------------+
| 2019-08-17 | 110.5         |
+------------+---------------+
```




## -- 3. Devuelve el número de compras en los que ha participado el suministrador Daniel Sáez Vega. (Sin utilizar INNER JOIN)



```sql
select count(c.id_consumidor)
from compra c
where c.id_suministrador = (select sum.id
                        from suministrador sum
                        where sum.nombre = 'Daniel' and  sum.apellido1 = 'Sáez' and  sum.apellido2 = 'Vega');

+------------------------+
| count(c.id_consumidor) |
+------------------------+
| 6                      |
+------------------------+
```




## -- 4. Devuelve los datos del consumidor que realizó el compra más caro en el año 2021. (Sin utilizar INNER JOIN)



```sql
select * 
from consumidor
where id = 
          (select id_consumidor, max(total)
          from compra
          where fecha regexp '^2021-\d{2}-\d{2}');

##Haciendo esta parte me da que no hay ningauna compra en el 2021 ya no sigo con la subconsulta.
```




## -- 5. Devuelve un listado con los datos de los consumidores y las compras, de todos los consumidores que han realizado un compra durante el año 2020 con un valor mayor o igual al valor medio de las compras realizadas durante ese mismo año.


```sql
select con.*,c.*
from consumidor con
inner join compra c on c.id_consumidor = con.id
where fecha regexp '^2020-\d{2}-\d{2}'
and total >= ( select avg(total)
        from compra c
        where fecha regexp '^2020-\d{2}-\d{2}');

       
+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+
| id | nombre | apellido1 | apellido2 | ciudad  | categoria | id |  total  |   fecha    | id_consumidor | id_suministrador |
+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+
| 4  | Adrián | Suárez    |           | Jaén    | 300       | 8  | 1983.43 | 2020-10-10 | 4             | 6                |
| 2  | Adela  | Salas     | Díaz      | Granada | 200       | 12 | 3045.6  | 2020-04-25 | 2             | 1                |
+----+--------+-----------+-----------+---------+-----------+----+---------+------------+---------------+------------------+
```



## -- 6. Devuelve un listado de los consumidores que no han realizado ningún compra. (Utilizando IN o NOT IN).


```sql
select *
from consumidor
where id not in 
                (select id_consumidor
                from compra );

+----+-----------+-----------+-----------+---------+-----------+
| id |  nombre   | apellido1 | apellido2 | ciudad  | categoria |
+----+-----------+-----------+-----------+---------+-----------+
| 9  | Guillermo | López     | Gómez     | Granada | 225       |
| 10 | Daniel    | Santana   | Loyola    | Sevilla | 125       |
+----+-----------+-----------+-----------+---------+-----------+


```

## -- 7. Devuelve un listado de los suministradores que no han realizado ningún compra. (Utilizando IN o NOT IN).


```sql
select *
from suministrador
where id not in 
              (select id_suministrador
              from compra);

+----+---------+-----------+-----------+-----------+
| id | nombre  | apellido1 | apellido2 | categoria |
+----+---------+-----------+-----------+-----------+
| 4  | Marta   | Herrera   | Gil       | 0.14      |
| 8  | Alfredo | Ruiz      | Flores    | 0.05      |
+----+---------+-----------+-----------+-----------+
```





## -- 8. Devuelve un listado de los consumidores que no han realizado ningún compra. (Utilizando EXISTS o NOT EXISTS).


```sql
SELECT *
FROM consumidor con
WHERE NOT EXISTS (
    SELECT 1
    FROM compra c
    WHERE c.id_consumidor = con.id
);
+----+-----------+-----------+-----------+---------+-----------+
| id |  nombre   | apellido1 | apellido2 | ciudad  | categoria |
+----+-----------+-----------+-----------+---------+-----------+
| 9  | Guillermo | López     | Gómez     | Granada | 225       |
| 10 | Daniel    | Santana   | Loyola    | Sevilla | 125       |
+----+-----------+-----------+-----------+---------+-----------+


```


## -- 9. Devuelve un listado de los suministradores que no han realizado ningún compra. (Utilizando EXISTS o NOT EXISTS).


```sql
select * 
from suministrador sum
where not exists 
              (select 1
              from compra c
              where sum.id = c.id_suministrador);


+----+---------+-----------+-----------+-----------+
| id | nombre  | apellido1 | apellido2 | categoria |
+----+---------+-----------+-----------+-----------+
| 4  | Marta   | Herrera   | Gil       | 0.14      |
| 8  | Alfredo | Ruiz      | Flores    | 0.05      |
+----+---------+-----------+-----------+-----------+
```

