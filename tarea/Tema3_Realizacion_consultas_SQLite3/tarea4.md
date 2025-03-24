<div align="justify">

## Code, Learn & Practice(Base de datos (Trabajo con funciones en BBDD")

<div align="center">
<img src="https://i0.wp.com/hunna.org/wp-content/uploads/2014/06/huellas.jpg?resize=324%2C215" width="500px"/>
</div>

## Objetivo

_Practicar la creación y manipulación de una base de datos SQLite3 desde la línea de comandos_.

## Descripción

## Pasos:

### Paso 1: Creación de la BBDD

Crea con el siguente contenido el fichero __supermercado-dump.sql__.

<details>
<summary style= "color: red"> Resultado </summary>

```sql
s
```
</details>


```sql
CREATE TABLE productos (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    categoria TEXT,
    precio REAL
);

CREATE TABLE ventas (
    id INTEGER PRIMARY KEY,
    id_producto INTEGER,
    cantidad INTEGER,
    fecha DATE,
    FOREIGN KEY (id_producto) REFERENCES productos(id)
);

INSERT INTO productos (id, nombre, categoria, precio) VALUES 
    (1, 'Arroz', 'Alimentos', 2.5),
    (2, 'Leche', 'Lácteos', 1.8),
    (3, 'Pan', 'Panadería', 1.2),
    (4, 'Manzanas', 'Frutas', 3.0),
    (5, 'Pollo', 'Carnes', 5.5),
    (6, 'Huevos', 'Lácteos', 1.0),
    (7, 'Yogurt', 'Lácteos', 2.0),
    (8, 'Tomates', 'Verduras', 2.2),
    (9, 'Queso', 'Lácteos', 4.0),
    (10, 'Cereal', 'Desayuno', 3.5),
    (11, 'Papel Higiénico', 'Hogar', 1.5),
    (12, 'Cepillo de Dientes', 'Higiene', 2.0),
    (13, 'Detergente', 'Limpieza', 2.8),
    (14, 'Galletas', 'Snacks', 1.7),
    (15, 'Aceite de Oliva', 'Cocina', 4.5),
    (16, 'Café', 'Bebidas', 5.0),
    (17, 'Sopa enlatada', 'Conservas', 2.3),
    (18, 'Jabón de Baño', 'Higiene', 1.2),
    (19, 'Botellas de Agua', 'Bebidas', 1.0),
    (20, 'Cerveza', 'Bebidas', 3.8);

INSERT INTO ventas (id_producto, cantidad, fecha) VALUES 
    (1, 5, '2024-01-17'),
    (2, 3, '2024-01-17'),
    (4, 2, '2024-01-17'),
    (5, 1, '2024-01-17'),
    (6, 10, '2024-01-18'),
    (8, 4, '2024-01-18'),
    (10, 2, '2024-01-18'),
    (14, 7, '2024-01-19'),
    (16, 3, '2024-01-19'),
    (18, 6, '2024-01-20');
```
  
### Paso 2 Lectura del fichero sql.

Entra en sqlite a través del siguiente comando:

```sql
sqlite3 tarea4.db 
```

Haciendo un __.read__ del fichero __sql__, de nombre __supermercado-db.sql__, realiza la creación e inserción de información de la __BBDD__.

<details>
<summary style= "color: red"> Resultado </summary>

```sql
![lectura de BBDD](https://raw.githubusercontent.com/johnfredyrg1226/base_datos2/main/tarea/Tema3_Realizacion_consultas_SQLite3/imagenes/read.png)



```
</details>

### Paso 3: Responde a las siguientes cuestiones

- Realiza el diagrama __ER__ de la __BBDD__ supermercado.

<details>
<summary style= "color: red"> Resultado </summary>

## Diagrama Entidad-Relación

![Diagrama ER](https://github.com/johnfredyrg1226/base_datos2/raw/main/tarea/Tema3_Realizacion_consultas_SQLite3/tarea4_ER_.drawio.png)

</details>

- Realiza el diagrama __MR__ de la __BBDD__ supermercado.

<details>
<summary style= "color: red"> Resultado </summary>

## DIAGRAMA MODELO RELACIONAL
![Diagrama ER](https://github.com/johnfredyrg1226/base_datos2/raw/main/tarea/Tema3_Realizacion_consultas_SQLite3/tarea4_MR_.drawio.png)

</details>


- Indica si la BBDD esta __normalizada__ hasta la 3ª forma normal, justificando la respuesta.

<details>
<summary style= "color: red"> Resultado </summary>

```sql
# Conclusión general:

La base de datos está normalizada hasta la 3ª forma normal (3FN). Las tablas `productos` y `ventas` cumplen con los requisitos de 1FN, 2FN y 3FN:
- No hay valores repetidos ni listas en las columnas (1FN).
- Todas las columnas no clave dependen completamente de la clave primaria (2FN).
- No existen dependencias transitivas entre columnas no clave (3FN).


```
</details>

### Paso 4: Responde a las siguientes cuestiones

Realiza las siguientes consultas, y muestra el resultado obtenido:

- Mostrar todos los productos de la categoría "Bebidas".
<details>
<summary style= "color: red"> Resultado </summary>

**LOWER(nombre) convierte el nombre a minúsculas.**

**UPPER(nombre) convierte el nombre a mayúsculas.**

```sql
sqlite> select * from productos 
   ...> where categoria = "bebidas";
sqlite> select * from productos 
   ...> where categoria = "Bebidas";
+----+------------------+-----------+--------+
| id |      nombre      | categoria | precio |
+----+------------------+-----------+--------+
| 16 | Café             | Bebidas   | 5.0    |
| 19 | Botellas de Agua | Bebidas   | 1.0    |
| 20 | Cerveza          | Bebidas   | 3.8    |
+----+------------------+-----------+--------+
sqlite> select * from productos 
   ...> where  Lower(categoria) = "bebidas";
+----+------------------+-----------+--------+
| id |      nombre      | categoria | precio |
+----+------------------+-----------+--------+
| 16 | Café             | Bebidas   | 5.0    |
| 19 | Botellas de Agua | Bebidas   | 1.0    |
| 20 | Cerveza          | Bebidas   | 3.8    |
+----+------------------+-----------+--------+
sqlite> 
```
</details>

- Listar los productos ordenados por precio de forma descendente.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select * from productos
   ...> ORDER BY precio desc;
+----+--------------------+-----------+--------+
| id |       nombre       | categoria | precio |
+----+--------------------+-----------+--------+
| 5  | Pollo              | Carnes    | 5.5    |
| 16 | Café               | Bebidas   | 5.0    |
| 15 | Aceite de Oliva    | Cocina    | 4.5    |
| 9  | Queso              | Lácteos   | 4.0    |
| 20 | Cerveza            | Bebidas   | 3.8    |
| 10 | Cereal             | Desayuno  | 3.5    |
| 4  | Manzanas           | Frutas    | 3.0    |
| 13 | Detergente         | Limpieza  | 2.8    |
| 1  | Arroz              | Alimentos | 2.5    |
| 17 | Sopa enlatada      | Conservas | 2.3    |
| 8  | Tomates            | Verduras  | 2.2    |
| 7  | Yogurt             | Lácteos   | 2.0    |
| 12 | Cepillo de Dientes | Higiene   | 2.0    |
| 2  | Leche              | Lácteos   | 1.8    |
| 14 | Galletas           | Snacks    | 1.7    |
| 11 | Papel Higiénico    | Hogar     | 1.5    |
| 3  | Pan                | Panadería | 1.2    |
| 18 | Jabón de Baño      | Higiene   | 1.2    |
| 6  | Huevos             | Lácteos   | 1.0    |
| 19 | Botellas de Agua   | Bebidas   | 1.0    |
+----+--------------------+-----------+--------+

```
</details>
- Calcular el precio total de todos los productos en la tabla "productos".
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select SUM(precio) as precio_total from productos;
+--------------+
| precio_total |
+--------------+
| 52.5         |
+--------------+
```
</details>
- Encontrar los productos con un nombre que contenga la letra 'a'.

<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre from productos
   ...> where nombre REGEXP '[aA]';
+------------------+
|      nombre      |
+------------------+
| Arroz            |
| Pan              |
| Manzanas         |
| Tomates          |
| Cereal           |
| Papel Higiénico  |
| Galletas         |
| Aceite de Oliva  |
| Café             |
| Sopa enlatada    |
| Jabón de Baño    |
| Botellas de Agua |
| Cerveza          |
+------------------+

```
</details>
- Obtener la cantidad total de productos vendidos en todas las fechas.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select sum(cantidad) as cantidad_total from ventas; 
+----------------+
| cantidad_total |
+----------------+
| 43             |
+----------------+

```
</details>
- Encontrar el producto más caro en cada categoría.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
WHERE precio = (
    SELECT MAX(precio)
    FROM productos p2
    WHERE p2.categoria = p1.categoria
);
+--------------------+-----------+--------+
|       nombre       | categoria | precio |
+--------------------+-----------+--------+
| Arroz              | Alimentos | 2.5    |
| Pan                | Panadería | 1.2    |
| Manzanas           | Frutas    | 3.0    |
| Pollo              | Carnes    | 5.5    |
| Tomates            | Verduras  | 2.2    |
| Queso              | Lácteos   | 4.0    |
| Cereal             | Desayuno  | 3.5    |
| Papel Higiénico    | Hogar     | 1.5    |
| Cepillo de Dientes | Higiene   | 2.0    |
| Detergente         | Limpieza  | 2.8    |
| Galletas           | Snacks    | 1.7    |
| Aceite de Oliva    | Cocina    | 4.5    |
| Café               | Bebidas   | 5.0    |
| Sopa enlatada      | Conservas | 2.3    |
+--------------------+-----------+--------+
sqlite> SELECT p1.nombre, p1.categoria, p1.precio
FROM productos p1
INNER JOIN (
    SELECT categoria, MAX(precio) AS precio_maximo
    FROM productos
    GROUP BY categoria
) p2 ON p1.categoria = p2.categoria AND p1.precio = p2.precio_maximo;
+--------------------+-----------+--------+
|       nombre       | categoria | precio |
+--------------------+-----------+--------+
| Arroz              | Alimentos | 2.5    |
| Pan                | Panadería | 1.2    |
| Manzanas           | Frutas    | 3.0    |
| Pollo              | Carnes    | 5.5    |
| Tomates            | Verduras  | 2.2    |
| Queso              | Lácteos   | 4.0    |
| Cereal             | Desayuno  | 3.5    |
| Papel Higiénico    | Hogar     | 1.5    |
| Cepillo de Dientes | Higiene   | 2.0    |
| Detergente         | Limpieza  | 2.8    |
| Galletas           | Snacks    | 1.7    |
| Aceite de Oliva    | Cocina    | 4.5    |
| Café               | Bebidas   | 5.0    |
| Sopa enlatada      | Conservas | 2.3    |
+--------------------+-----------+--------+
sqlite> 


```
</details>
- Listar los productos que no han sido vendidos.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT p1.nombre, p1.categoria, p1.precio
FROM productos p1
LEFT JOIN ventas v ON p1.id = v.id_producto
WHERE v.id_producto IS NULL;
+--------------------+-----------+--------+
|       nombre       | categoria | precio |
+--------------------+-----------+--------+
| Pan                | Panadería | 1.2    |
| Yogurt             | Lácteos   | 2.0    |
| Queso              | Lácteos   | 4.0    |
| Papel Higiénico    | Hogar     | 1.5    |
| Cepillo de Dientes | Higiene   | 2.0    |
| Detergente         | Limpieza  | 2.8    |
| Aceite de Oliva    | Cocina    | 4.5    |
| Sopa enlatada      | Conservas | 2.3    |
| Botellas de Agua   | Bebidas   | 1.0    |
| Cerveza            | Bebidas   | 3.8    |
+--------------------+-----------+--------+


```
</details>
- Calcular el precio promedio de los productos en la categoría "Snacks".
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select avg(precio) as precio_promedio from productos p1
   ...> where p1.categoria = "Snacks";
+-----------------+
| precio_promedio |
+-----------------+
| 1.7             |
+-----------------+
sqlite> 

```
</details>
- Encontrar los productos que han sido vendidos más de 5 veces.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT p.nombre, v.cantidad
FROM productos p
INNER JOIN ventas v ON p.id = v.id_producto
WHERE v.cantidad > 5;
+---------------+----------+
|    nombre     | cantidad |
+---------------+----------+
| Huevos        | 10       |
| Galletas      | 7        |
| Jabón de Baño | 6        |
+---------------+----------+

```
</details>
- Mostrar la fecha y la cantidad de ventas para cada producto.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select v.cantidad, v.fecha, p.nombre from ventas v
   ...> inner join productos p on p.id = v.id_producto;
+----------+------------+---------------+
| cantidad |   fecha    |    nombre     |
+----------+------------+---------------+
| 5        | 2024-01-17 | Arroz         |
| 3        | 2024-01-17 | Leche         |
| 2        | 2024-01-17 | Manzanas      |
| 1        | 2024-01-17 | Pollo         |
| 10       | 2024-01-18 | Huevos        |
| 4        | 2024-01-18 | Tomates       |
| 2        | 2024-01-18 | Cereal        |
| 7        | 2024-01-19 | Galletas      |
| 3        | 2024-01-19 | Café          |
| 6        | 2024-01-20 | Jabón de Baño |
+----------+------------+---------------+

```
</details>
- Encontrar los productos que tienen un precio menor o igual a 2.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select p.nombre, p.precio from productos p
   ...> where precio <= 2;
+--------------------+--------+
|       nombre       | precio |
+--------------------+--------+
| Leche              | 1.8    |
| Pan                | 1.2    |
| Huevos             | 1.0    |
| Yogurt             | 2.0    |
| Papel Higiénico    | 1.5    |
| Cepillo de Dientes | 2.0    |
| Galletas           | 1.7    |
| Jabón de Baño      | 1.2    |
| Botellas de Agua   | 1.0    |
+--------------------+--------+

```
</details>
- Calcular la cantidad total de ventas para cada fecha.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select v.fecha, SUM(v.cantidad) AS cantidad_total
   ...> from ventas v
   ...> group by v.fecha
   ...> order by v.fecha;
+------------+----------------+
|   fecha    | cantidad_total |
+------------+----------------+
| 2024-01-17 | 11             |
| 2024-01-18 | 16             |
| 2024-01-19 | 10             |
| 2024-01-20 | 6              |
+------------+----------------+

```
</details>
- Listar los productos cuyo nombre comienza con la letra 'P'.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre from productos
   ...> where nombre REGEXP '^[pP]';
+-----------------+
|     nombre      |
+-----------------+
| Pan             |
| Pollo           |
| Papel Higiénico |
+-----------------+

```
</details>
- Obtener el producto más vendido en términos de cantidad.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT p.nombre, v_ma.max_cantidad
FROM productos p
INNER JOIN (
    SELECT id_producto, MAX(cantidad) AS max_cantidad
    FROM ventas
    GROUP BY id_producto
) v_ma ON v_ma.id_producto = p.id 
ORDER BY v_ma.max_cantidad ASC;
+---------------+--------------+
|    nombre     | max_cantidad |
+---------------+--------------+
| Pollo         | 1            |
| Manzanas      | 2            |
| Cereal        | 2            |
| Leche         | 3            |
| Café          | 3            |
| Tomates       | 4            |
| Arroz         | 5            |
| Jabón de Baño | 6            |
| Galletas      | 7            |
| Huevos        | 10           |
+---------------+--------------+
sqlite> 
```
</details>
- Mostrar los productos que fueron vendidos en la fecha '__2024-01-18__'.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT p.nombre, v.id_producto
FROM productos p
INNER JOIN (
    SELECT id_producto
    FROM ventas
    WHERE fecha = '2024-01-18'
) v ON p.id = v.id_producto;
+---------+-------------+
| nombre  | id_producto |
+---------+-------------+
| Huevos  | 6           |
| Tomates | 8           |
| Cereal  | 10          |
+---------+-------------+
```
</details>
- Calcular el total de ventas para cada producto.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT p.nombre, v2.total_vendido
FROM productos p
INNER JOIN (
    SELECT id_producto, SUM(cantidad) AS total_vendido
    FROM ventas
    GROUP BY id_producto
) v2 ON v2.id_producto = p.id;
+---------------+---------------+
|    nombre     | total_vendido |
+---------------+---------------+
| Arroz         | 5             |
| Leche         | 3             |
| Manzanas      | 2             |
| Pollo         | 1             |
| Huevos        | 10            |
| Tomates       | 4             |
| Cereal        | 2             |
| Galletas      | 7             |
| Café          | 3             |
| Jabón de Baño | 6             |
+---------------+---------------+

```
</details>
- Encontrar los productos con un precio entre 3 y 4.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre, precio from productos
   ...> where precio >= 3 and precio <= 4;
+----------+--------+
|  nombre  | precio |
+----------+--------+
| Manzanas | 3.0    |
| Queso    | 4.0    |
| Cereal   | 3.5    |
| Cerveza  | 3.8    |
+----------+--------+

SELECT nombre, precio 
FROM productos
WHERE precio BETWEEN 3 AND 4;

sqlite> 
```
</details>
- Listar los productos y sus categorías ordenados alfabéticamente por categoría.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre, categoria from productos p
   ...> order by categoria asc;
+--------------------+-----------+
|       nombre       | categoria |
+--------------------+-----------+
| Arroz              | Alimentos |
| Café               | Bebidas   |
| Botellas de Agua   | Bebidas   |
| Cerveza            | Bebidas   |
| Pollo              | Carnes    |
| Aceite de Oliva    | Cocina    |
| Sopa enlatada      | Conservas |
| Cereal             | Desayuno  |
| Manzanas           | Frutas    |
| Cepillo de Dientes | Higiene   |
| Jabón de Baño      | Higiene   |
| Papel Higiénico    | Hogar     |
| Detergente         | Limpieza  |
| Leche              | Lácteos   |
| Huevos             | Lácteos   |
| Yogurt             | Lácteos   |
| Queso              | Lácteos   |
| Pan                | Panadería |
| Galletas           | Snacks    |
| Tomates            | Verduras  |
+--------------------+-----------+

```
</details>
- Calcular el precio total de los productos vendidos en la fecha '2024-01-19'.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT SUM(p.precio * v.cantidad) AS total_ventas
FROM ventas v
INNER JOIN productos p ON v.id_producto = p.id
WHERE v.fecha = '2024-01-19';
+--------------+
| total_ventas |
+--------------+
| 26.9         |
+--------------+

```
</details>
- Mostrar los productos que no pertenecen a la categoría "__Higiene__".
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre, categoria from productos
   ...> where categoria REGEXP '[^Higiene]';
+------------------+-----------+
|      nombre      | categoria |
+------------------+-----------+
| Arroz            | Alimentos |
| Leche            | Lácteos   |
| Pan              | Panadería |
| Manzanas         | Frutas    |
| Pollo            | Carnes    |
| Huevos           | Lácteos   |
| Yogurt           | Lácteos   |
| Tomates          | Verduras  |
| Queso            | Lácteos   |
| Cereal           | Desayuno  |
| Papel Higiénico  | Hogar     |
| Detergente       | Limpieza  |
| Galletas         | Snacks    |
| Aceite de Oliva  | Cocina    |
| Café             | Bebidas   |
| Sopa enlatada    | Conservas |
| Botellas de Agua | Bebidas   |
| Cerveza          | Bebidas   |
+------------------+-----------+

```
</details>
- Encontrar la cantidad total de productos en cada categoría.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select p.categoria, SUM(v.cantidad) as total_vendido
   ...> from ventas v
   ...> inner join productos p on p.id=v.id_producto
   ...> group by p.categoria;
+-----------+---------------+
| categoria | total_vendido |
+-----------+---------------+
| Alimentos | 5             |
| Bebidas   | 3             |
| Carnes    | 1             |
| Desayuno  | 2             |
| Frutas    | 2             |
| Higiene   | 6             |
| Lácteos   | 13            |
| Snacks    | 7             |
| Verduras  | 4             |
+-----------+---------------+

```
</details>
- Listar los productos que tienen un precio igual a la media de precios.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
esta es la media 
sqlite> SELECT AVG(precio) AS precio_promedio
FROM productos;
+-----------------+
| precio_promedio |
+-----------------+
| 2.625           |
+-----------------+

pero no hay productos con ese valor sqlite> SELECT nombre, precio
FROM productos
WHERE precio = (SELECT AVG(precio) FROM productos);


```
</details>
- Calcular el precio total de los productos vendidos en cada fecha.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select p.categoria, SUM(v.cantidad * p.precio) as precio_total
   ...> from ventas v
   ...> inner join productos p on p.id=v.id_producto
   ...> group by v.fecha 
   ...> order by v.fecha;
+-----------+--------------+
| categoria | precio_total |
+-----------+--------------+
| Alimentos | 29.4         |
| Lácteos   | 25.8         |
| Snacks    | 26.9         |
| Higiene   | 7.2          |
+-----------+--------------+

```
</details>
- Mostrar los productos con un nombre que termina con la letra 'o'.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre from productos p
   ...> where nombre REGEXP '[Oo]$';
+-----------------+
|     nombre      |
+-----------------+
| Pollo           |
| Queso           |
| Papel Higiénico |
| Jabón de Baño   |
+-----------------+

```
</details>
- Encontrar los productos que han sido vendidos en más de una fecha.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT p.id, p.nombre
FROM productos p
INNER JOIN (
    SELECT id_producto
    FROM ventas
    GROUP BY id_producto
    HAVING COUNT(DISTINCT fecha) > 1
) v ON p.id = v.id_producto;


## no se encuentra nada...
```
</details>
- Listar los productos cuya categoría comienza con la letra 'L'.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT nombre, categoria FROM productos
WHERE categoria REGEXP '^[Ll]';
+------------+-----------+
|   nombre   | categoria |
+------------+-----------+
| Leche      | Lácteos   |
| Huevos     | Lácteos   |
| Yogurt     | Lácteos   |
| Queso      | Lácteos   |
| Detergente | Limpieza  |
+------------+-----------+
sqlite> 


```
</details>
- Calcular el total de ventas para cada producto en la fecha '2024-01-17'.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select fecha,SUM(cantidad)as ventas_totales from ventas
   ...> where fecha = '2024-01-17';
+------------+----------------+
|   fecha    | ventas_totales |
+------------+----------------+
| 2024-01-17 | 11             |
+------------+----------------+

```
</details>
- Mostrar los productos cuyo nombre tiene al menos 5 caracteres.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> SELECT nombre 
FROM productos
WHERE nombre REGEXP '^.{5,}$';
+--------------------+
|       nombre       |
+--------------------+
| Arroz              |
| Leche              |
| Manzanas           |
| Pollo              |
| Huevos             |
| Yogurt             |
| Tomates            |
| Queso              |
| Cereal             |
| Papel Higiénico    |
| Cepillo de Dientes |
| Detergente         |
| Galletas           |
| Aceite de Oliva    |
| Sopa enlatada      |
| Jabón de Baño      |
| Botellas de Agua   |
| Cerveza            |
+--------------------+

```
</details>
- Encontrar los productos que tienen un precio superior al precio máximo en la tabla "__productos__".
<details>
<summary style= "color: red"> Resultado </summary>

```sql

```
</details>

### Generación Informe

Genera un informe con cada una de las consultas y los resuldos obtenidos tras su ejecución. El informe se debe de realizar en __markdown, y enviar el enlace__.

</div>
