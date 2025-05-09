## -- Consultas sobre una tabla Francisco José Rodríguez Afonso

### -- 1.Listar todas las ventas ordenadas por fecha (más recientes primero):

```sql
 select * from venta order by fecha desc;

+----+---------+------------+------------+-------------+
| id |  total  |   fecha    | id_cliente | id_empleado |
+----+---------+------------+------------+-------------+
| 1  | 899.99  | 2023-05-15 | 5          | 2           |
| 3  | 450.75  | 2023-05-15 | 2          | 1           |
| 5  | 1799.0  | 2023-04-22 | 5          | 2           |
| 8  | 1299.95 | 2023-03-18 | 4          | 6           |
| 15 | 899.0   | 2023-03-10 | 1          | 5           |
| 16 | 2799.99 | 2023-03-10 | 1          | 5           |
| 12 | 4199.0  | 2023-02-14 | 2          | 1           |
| 14 | 249.9   | 2023-02-02 | 6          | 1           |
| 13 | 799.5   | 2023-01-25 | 6          | 1           |
| 9  | 2499.5  | 2022-10-15 | 8          | 3           |
| 2  | 1499.5  | 2022-09-20 | 1          | 5           |
| 4  | 299.9   | 2022-08-10 | 8          | 3           |
| 11 | 199.99  | 2022-08-10 | 3          | 7           |
| 6  | 3299.99 | 2022-07-05 | 7          | 1           |
| 7  | 5999.0  | 2021-09-12 | 2          | 1           |
| 10 | 350.25  | 2021-06-30 | 8          | 2           |
+----+---------+------------+------------+-------------+
```


### -- 2. Top 3 ventas de mayor valor:

```sql
select * from venta order by fecha desc;

+----+---------+------------+------------+-------------+
| id |  total  |   fecha    | id_cliente | id_empleado |
+----+---------+------------+------------+-------------+
| 7  | 5999.0  | 2021-09-12 | 2          | 1           |
| 12 | 4199.0  | 2023-02-14 | 2          | 1           |
| 6  | 3299.99 | 2022-07-05 | 7          | 1           |
+----+---------+------------+------------+-------------+
```



### -- 3.Clientes con puntos de fidelidad no nulos:

```sql
sqlite> select * from cliente where puntos_fidelidad not null;
+----+----------+-----------+-----------+-----------+------------------+
| id |  nombre  | apellido1 | apellido2 |  ciudad   | puntos_fidelidad |
+----+----------+-----------+-----------+-----------+------------------+
| 1  | Carlos   | Martínez  | García    | Madrid    | 1500             |
| 2  | Ana      | López     | Fernández | Barcelona | 800              |
| 4  | Elena    | Gómez     |           | Sevilla   | 1200             |
| 5  | David    | Pérez     | Ruiz      | Madrid    | 750              |
| 6  | Laura    | Jiménez   | Moreno    | Bilbao    | 950              |
| 7  | Sofía    | Hernández |           | Zaragoza  | 1800             |
| 8  | Javier   | Domingo   | Santos    | Málaga    | 600              |
| 9  | Patricia | Romero    | González  | Barcelona | 1100             |
| 10 | Antonio  | Navarro   | Torres    | Valencia  | 400              |
+----+----------+-----------+-----------+-----------+------------------+
```
### -- 4. Ventas del año 2023 con total superior a 1000€:

```sql
sqlite> select * from venta where fecha regexp "^2023-\d{2}-\d{2}" and total >1000;
+----+---------+------------+------------+-------------+
| id |  total  |   fecha    | id_cliente | id_empleado |
+----+---------+------------+------------+-------------+
| 5  | 1799.0  | 2023-04-22 | 5          | 2           |
| 8  | 1299.95 | 2023-03-18 | 4          | 6           |
| 12 | 4199.0  | 2023-02-14 | 2          | 1           |
| 16 | 2799.99 | 2023-03-10 | 1          | 5           |
+----+---------+------------+------------+-------------+
```
### -- 5. Empleados con comisión mayor a 0.10:

```sql
sqlite> select * from empleado where comision >0.10;
+----+--------+-----------+-----------+----------+
| id | nombre | apellido1 | apellido2 | comision |
+----+--------+-----------+-----------+----------+
| 1  | Daniel | Vázquez   | Gil       | 0.12     |
| 4  | Lucía  | Reyes     | Martín    | 0.11     |
+----+--------+-----------+-----------+----------+
```
### -- 6. Clientes de Madrid o Barcelona:

```sql
sqlite> select * from cliente where ciudad='Madrid' or ciudad='Barcelona';
+----+----------+-----------+-----------+-----------+------------------+
| id |  nombre  | apellido1 | apellido2 |  ciudad   | puntos_fidelidad |
+----+----------+-----------+-----------+-----------+------------------+
| 1  | Carlos   | Martínez  | García    | Madrid    | 1500             |
| 2  | Ana      | López     | Fernández | Barcelona | 800              |
| 5  | David    | Pérez     | Ruiz      | Madrid    | 750              |
| 9  | Patricia | Romero    | González  | Barcelona | 1100             |
+----+----------+-----------+-----------+-----------+------------------+
```

## -- 2. Consultas multitabla (WHERE) (6 consultas - 1.8 puntos / 0.3 cada una)

### -- 7. Ventas con nombres de clientes, empleados y total de ventas (sin JOIN):

```sql
select c.nombre,e.nombre,v.total
from venta v, empleado e, cliente c
where v.id_cliente = c.id
and v.id_empleado = e.id;
+--------+-----------------+---------+
| nombre | nombre_empleado |  total  |
+--------+-----------------+---------+
| David  | María           | 899.99  |
| Carlos | Alejandro       | 1499.5  |
| Ana    | Daniel          | 450.75  |
| Javier | Pablo           | 299.9   |
| David  | María           | 1799.0  |
| Sofía  | Daniel          | 3299.99 |
| Ana    | Daniel          | 5999.0  |
| Elena  | Isabel          | 1299.95 |
| Javier | Pablo           | 2499.5  |
| Javier | María           | 350.25  |
| Miguel | Francisco       | 199.99  |
| Ana    | Daniel          | 4199.0  |
| Laura  | Daniel          | 799.5   |
| Laura  | Daniel          | 249.9   |
| Carlos | Alejandro       | 899.0   |
| Carlos | Alejandro       | 2799.99 |
+--------+-----------------+---------+
```

-- 8.  Clientes que compraron en 2023 (sin JOIN):

```sql
select c.nombre, c.apellido1, v.fecha
from venta v, cliente c
where v.id_cliente = c.id 
and v.fecha regexp '^2023-\d{2}-\d{2}'
group by c.nombre;
+--------+-----------+------------+
| nombre | apellido1 |   fecha    |
+--------+-----------+------------+
| Ana    | López     | 2023-05-15 |
| Carlos | Martínez  | 2023-03-10 |
| David  | Pérez     | 2023-05-15 |
| Elena  | Gómez     | 2023-03-18 |
| Laura  | Jiménez   | 2023-01-25 |
+--------+-----------+------------+
```

### -- 9.  Empleados que atendieron a clientes de Madrid:

```sql
select e.nombre as nombre_empleado, 
        e.apellido1 as apellido_empleado, 
        c.nombre as nombre_cliente, 
        c.ciudad as ciudad_cliente
from venta v, cliente c, empleado e
where v.id_cliente = c.id
and v.id_empleado = e.id
and c.ciudad='Madrid'
group by e.nombre;

+-----------------+-------------------+----------------+----------------+
| nombre_empleado | apellido_empleado | nombre_cliente | ciudad_cliente |
+-----------------+-------------------+----------------+----------------+
| Alejandro       | Suárez            | Carlos         | Madrid         |
| María           | Castro            | David          | Madrid         |
+-----------------+-------------------+----------------+----------------+
```
### -- 10. Ventas superiores a 2000€ con datos de clientes:

```sql
select c.nombre,c.apellido1,c.apellido2,v.total as total_venta
from cliente c, venta v
where v.id_cliente = c.id
and v.total > 2000
group by v.total;
+--------+-----------+-----------+-------------+
| nombre | apellido1 | apellido2 | total_venta |
+--------+-----------+-----------+-------------+
| Javier | Domingo   | Santos    | 2499.5      |
| Carlos | Martínez  | García    | 2799.99     |
| Sofía  | Hernández |           | 3299.99     |
| Ana    | López     | Fernández | 4199.0      |
| Ana    | López     | Fernández | 5999.0      |
+--------+-----------+-----------+-------------+
```


### -- 11. Promedio de ventas por empleado (sin JOIN):

```sql
select avg(v.total) as promedio_ventas,e.nombre as nombre_empleado
from venta v,empleado e
where v.id_empleado = e.id
group by e.nombre;
+------------------+-----------------+
| promedio_ventas  | nombre_empleado |
+------------------+-----------------+
| 1732.83          | Alejandro       |
| 2499.69          | Daniel          |
| 199.99           | Francisco       |
| 1299.95          | Isabel          |
| 1016.41333333333 | María           |
| 1399.7           | Pablo           |
+------------------+-----------------+
```

### -- 12. Clientes que no han comprado (sin JOIN):

```sql
select *
from cliente c
where c.id not in(
        select v.id_cliente
        from venta v
        group by v.id_cliente);
+----+----------+-----------+-----------+-----------+------------------+
| id |  nombre  | apellido1 | apellido2 |  ciudad   | puntos_fidelidad |
+----+----------+-----------+-----------+-----------+------------------+
| 9  | Patricia | Romero    | González  | Barcelona | 1100             |
| 10 | Antonio  | Navarro   | Torres    | Valencia  | 400              |
+----+----------+-----------+-----------+-----------+------------------+
```


## -- 3. Consultas multitabla (JOIN) (6 consultas - 1.8 puntos / 0.3 cada una)

### -- 13. Ventas con nombres de clientes ,empleados y total de ventas (CON UN TIPO DE JOIN):

```sql
select c.nombre as nombre_cliente,
        e.nombre as nombre_empleado,
        v.total as total_ventas
from venta v
inner join empleado e on e.id = v.id_empleado
inner join cliente c on c.id = v.id_cliente
order by c.nombre;
+----------------+-----------------+--------------+
| nombre_cliente | nombre_empleado | total_ventas |
+----------------+-----------------+--------------+
| Ana            | Daniel          | 450.75       |
| Ana            | Daniel          | 5999.0       |
| Ana            | Daniel          | 4199.0       |
| Carlos         | Alejandro       | 1499.5       |
| Carlos         | Alejandro       | 899.0        |
| Carlos         | Alejandro       | 2799.99      |
| David          | María           | 899.99       |
| David          | María           | 1799.0       |
| Elena          | Isabel          | 1299.95      |
| Javier         | Pablo           | 299.9        |
| Javier         | Pablo           | 2499.5       |
| Javier         | María           | 350.25       |
| Laura          | Daniel          | 799.5        |
| Laura          | Daniel          | 249.9        |
| Miguel         | Francisco       | 199.99       |
| Sofía          | Daniel          | 3299.99      |
+----------------+-----------------+--------------+
```


### -- 14.  Clientes que compraron en 2023 (CON UN TIPO DE JOIN):

```sql
select c.id,c.nombre,c.apellido1
from cliente c
inner join venta v on c.id = v.id_cliente
where v.fecha regexp '^2023-\d{2}-\d{2}'
group by c.nombre;
+----+--------+-----------+
| id | nombre | apellido1 |
+----+--------+-----------+
| 2  | Ana    | López     |
| 1  | Carlos | Martínez  |
| 5  | David  | Pérez     |
| 4  | Elena  | Gómez     |
| 6  | Laura  | Jiménez   |
+----+--------+-----------+
```

## -- 15.  Empleados que atendieron a clientes de Madrid:

```sql
select e.nombre as nombre_empleado,
        c.nombre as nombre_cliente,
        c.ciudad as _ciudad_del_cliente
from venta v
inner join cliente c on c.id = v.id_cliente
inner join empleado e on e.id = v.id_empleado
where c.ciudad = 'Madrid'
group by c.nombre;
+-----------------+----------------+---------------------+
| nombre_empleado | nombre_cliente | _ciudad_del_cliente |
+-----------------+----------------+---------------------+
| Alejandro       | Carlos         | Madrid              |
| María           | David          | Madrid              |
+-----------------+----------------+---------------------+
```

### -- 16. Ventas superiores a 2000€ con datos de clientes:

```sql
select * 
from venta v
inner join cliente c on c.id = v.id_cliente
where v.total > 2000;
+----+---------+------------+------------+-------------+----+--------+-----------+-----------+-----------+------------------+
| id |  total  |   fecha    | id_cliente | id_empleado | id | nombre | apellido1 | apellido2 |  ciudad   | puntos_fidelidad |
+----+---------+------------+------------+-------------+----+--------+-----------+-----------+-----------+------------------+
| 6  | 3299.99 | 2022-07-05 | 7          | 1           | 7  | Sofía  | Hernández |           | Zaragoza  | 1800             |
| 7  | 5999.0  | 2021-09-12 | 2          | 1           | 2  | Ana    | López     | Fernández | Barcelona | 800              |
| 9  | 2499.5  | 2022-10-15 | 8          | 3           | 8  | Javier | Domingo   | Santos    | Málaga    | 600              |
| 12 | 4199.0  | 2023-02-14 | 2          | 1           | 2  | Ana    | López     | Fernández | Barcelona | 800              |
| 16 | 2799.99 | 2023-03-10 | 1          | 5           | 1  | Carlos | Martínez  | García    | Madrid    | 1500             |
+----+---------+------------+------------+-------------+----+--------+-----------+-----------+-----------+------------------+

```

### -- 17. Promedio de ventas por empleado (COUN TIPO DE JOIN):

```sql
select e.nombre, avg(v.total)as premodio_ventas
from empleado e
inner join venta v on v.id_empleado = e.id
group by e.nombre;
+-----------+------------------+
|  nombre   | promedio_ventas  |
+-----------+------------------+
| Alejandro | 1732.83          |
| Daniel    | 2499.69          |
| Francisco | 199.99           |
| Isabel    | 1299.95          |
| María     | 1016.41333333333 |
| Pablo     | 1399.7           |
+-----------+------------------+
```

### -- 18. Clientes que no han comprado (CON UN TIPO DE JOIN):

```sql

select c.*
from cliente c 
left join venta v on c.id = v.id_cliente
where v.id_cliente is null;


+----+----------+-----------+-----------+-----------+------------------+
| id |  nombre  | apellido1 | apellido2 |  ciudad   | puntos_fidelidad |
+----+----------+-----------+-----------+-----------+------------------+
| 9  | Patricia | Romero    | González  | Barcelona | 1100             |
| 10 | Antonio  | Navarro   | Torres    | Valencia  | 400              |
+----+----------+-----------+-----------+-----------+------------------+
```

```sql
SELECT c.*
FROM cliente c
WHERE c.id NOT IN (
    SELECT v.id_cliente
    FROM venta v
);
```

#### -- 4. Consultas resumen (6 consultas - 2.4 puntos / 0.4 cada una)

#### -- 19. Total de ventas por ciudad de cliente:

```sql
select sum(v.total)as total_ventas, c.ciudad 
from venta v
inner join cliente c on c.id = v.id_cliente
group by c.ciudad;

+--------------+-----------+
| total_ventas |  ciudad   |
+--------------+-----------+
| 10648.75     | Barcelona |
| 1049.4       | Bilbao    |
| 7897.48      | Madrid    |
| 3149.65      | Málaga    |
| 1299.95      | Sevilla   |
| 199.99       | Valencia  |
| 3299.99      | Zaragoza  |
+--------------+-----------+
```

#### -- 20. Número de ventas por empleado en 2023:

```sql
select count(v.id)as total_ventas, e.nombre
from venta v
inner join empleado e on e.id = v.id_empleado
where fecha regexp '^2023'
group by id_empleado;

+--------------+-----------+
| total_ventas |  nombre   |
+--------------+-----------+
| 4            | Daniel    |
| 2            | María     |
| 2            | Alejandro |
| 1            | Isabel    |
+--------------+-----------+

```

### -- 21. Promedio de puntos de fidelidad por ciudad:

```sql
select c.ciudad, avg(c.puntos_fidelidad)
from cliente c
group by ciudad;
+-----------+-------------------------+
|  ciudad   | avg(c.puntos_fidelidad) |
+-----------+-------------------------+
| Barcelona | 950.0                   |
| Bilbao    | 950.0                   |
| Madrid    | 1125.0                  |
| Málaga    | 600.0                   |
| Sevilla   | 1200.0                  |
| Valencia  | 400.0                   |
| Zaragoza  | 1800.0                  |
+-----------+-------------------------+
```

### -- 22. Máxima venta por año:

```sql
select strftime('%Y', fecha)as anio, max(total)as maxima_venta
from venta
group by anio;

STRFTIME('%Y', FECHA) EXTRAE EL AÑO DE LA FECHA 2023-10-10
+------+--------------+
| anio | maxima_venta |
+------+--------------+
| 2021 | 5999.0       |
| 2022 | 3299.99      |
| 2023 | 4199.0       |
+------+--------------+
```
### -- 23. Clientes con más de 1 compra:

```sql
select count(*)as compras_total, c.nombre
from venta v
inner join cliente c on c.id = v.id_cliente
group by v.id_cliente
having compras_total >1;
+---------------+--------+
| compras_total | nombre |
+---------------+--------+
| 3             | Carlos |
| 3             | Ana    |
| 2             | David  |
| 2             | Laura  |
| 3             | Javier |
+---------------+--------+

```

### -- 24. Empleados con ventas promedio superiores a 1000€:

```sql
select e.nombre, avg(v.total)as venta_promedio
from venta v
inner join empleado e on v.id_empleado = e.id
group by e.nombre
having venta_promedio > 1000;

+-----------+------------------+
|  nombre   |  venta_promedio  |
+-----------+------------------+
| Alejandro | 1732.83          |
| Daniel    | 2499.69          |
| Isabel    | 1299.95          |
| María     | 1016.41333333333 |
| Pablo     | 1399.7           |
+-----------+------------------+
```

### -- 5. Subconsultas (6 consultas - 3.0 puntos / 0.5 cada una)

#### -- 25. Clientes con ventas superiores al promedio:

```sql
select c.nombre, avg(v.total)as promedio_ventas
from cliente c
inner join venta v on v.id_cliente = c.id
group by  c.nombre
having promedio_ventas > (select avg(ve.total)
                            from venta ve);

+--------+------------------+
| nombre | promedio_ventas  |
+--------+------------------+
| Ana    | 3549.58333333333 |
| Carlos | 1732.83          |
| Sofía  | 3299.99          |
+--------+------------------+

```

### -- 26. Empleados que no han realizado ventas:

```sql
select *
from empleado
where id not in (
    select distinct id_empleado
    from venta
    where id_empleado is not null
);
+----+----------+-----------+-----------+----------+
| id |  nombre  | apellido1 | apellido2 | comision |
+----+----------+-----------+-----------+----------+
| 4  | Lucía    | Reyes     | Martín    | 0.11     |
| 8  | Cristina | Cabrera   | Flores    | 0.04     |
+----+----------+-----------+-----------+----------+
```

#### -- 27. Ventas de clientes con puntos de fidelidad > 1000:

```sql
select v.*
from venta v
where id_cliente in(
    slect id
    from cliente
    where puntos_fidelidad >1000
);

+----+---------+------------+------------+-------------+
| id |  total  |   fecha    | id_cliente | id_empleado |
+----+---------+------------+------------+-------------+
| 2  | 1499.5  | 2022-09-20 | 1          | 5           |
| 6  | 3299.99 | 2022-07-05 | 7          | 1           |
| 8  | 1299.95 | 2023-03-18 | 4          | 6           |
| 15 | 899.0   | 2023-03-10 | 1          | 5           |
| 16 | 2799.99 | 2023-03-10 | 1          | 5           |
+----+---------+------------+------------+-------------+
```


#### -- 28. Clientes con al menos una venta > 2000€:

```sql
SELECT c.*
FROM cliente c
JOIN venta v ON c.id = v.id_cliente
WHERE v.total > 2000
GROUP BY c.nombre
ORDER BY c.id;
+----+--------+-----------+-----------+-----------+------------------+
| id | nombre | apellido1 | apellido2 |  ciudad   | puntos_fidelidad |
+----+--------+-----------+-----------+-----------+------------------+
| 1  | Carlos | Martínez  | García    | Madrid    | 1500             |
| 2  | Ana    | López     | Fernández | Barcelona | 800              |
| 7  | Sofía  | Hernández |           | Zaragoza  | 1800             |
| 8  | Javier | Domingo   | Santos    | Málaga    | 600              |
+----+--------+-----------+-----------+-----------+------------------+
```

-- 29. Empleados con ventas en todas las ciudades:

```sql

```

#### -- 30. Ventas del cliente con más puntos de fidelidad:

```sql
SELECT v.*
FROM venta v
JOIN cliente c ON v.id_cliente = c.id
WHERE c.puntos_fidelidad = (
    SELECT c.puntos_fidelidad
    FROM cliente c
    ORDER BY c.puntos_fidelidad DESC LIMIT 1
);
+----+---------+------------+------------+-------------+
| id |  total  |   fecha    | id_cliente | id_empleado |
+----+---------+------------+------------+-------------+
| 6  | 3299.99 | 2022-07-05 | 7          | 1           |
+----+---------+------------+------------+-------------+
```
