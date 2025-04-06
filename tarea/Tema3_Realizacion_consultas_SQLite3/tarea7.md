## tarea 7_ ejercicios de practica

-- Listar los coches vendidos con sus modelos y precios, junto con los nombres de los clientes que los compraron.
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. ¿Qué es lo que no me han pedido?

```sql
sqlite> .mode table 
sqlite> SELECT 
    clientes.nombre AS nombre_cliente,
    coches.modelo AS modelo_coche,
    coches.precio AS precio_coche
FROM 
    ventas
JOIN 
    clientes ON ventas.id_cliente = clientes.id_cliente
JOIN 
    coches ON ventas.id_coche = coches.id_coche;
+-----------------+----------------+--------------+
| nombre_cliente  |  modelo_coche  | precio_coche |
+-----------------+----------------+--------------+
| Juan Pérez      | Sedán 2022     | 25000.0      |
| María Gómez     | Hatchback 2021 | 22000.0      |
| Carlos López    | SUV 2023       | 30000.0      |
| Ana Martínez    | Coupé 2022     | 28000.0      |
| Pedro Rodríguez | Camioneta 2023 | 32000.0      |
| Laura Sánchez   | Compacto 2021  | 20000.0      |
| Miguel González | Híbrido 2022   | 27000.0      |
| Isabel Díaz     | Deportivo 2023 | 35000.0      |
| Elena Torres    | Eléctrico 2021 | 40000.0      |
+-----------------+----------------+--------------+


```


-- Encontrar los clientes que han comprado coches con precios superiores al promedio de todos los coches vendidos.
  -- Cosas que debo de tener en cuenta:
    -- Precios superiores.
    -- Obtener la media. AVG(precio)

```sql
sqlite> SELECT DISTINCT
    clientes.nombre AS nombre_cliente
FROM 
    ventas
JOIN 
    coches ON ventas.id_coche = coches.id_coche
JOIN 
    clientes ON ventas.id_cliente = clientes.id_cliente
WHERE 
    coches.precio > (SELECT AVG(precio) FROM coches);
+-----------------+
| nombre_cliente  |
+-----------------+
| Carlos López    |
| Pedro Rodríguez |
| Isabel Díaz     |
| Elena Torres    |
+-----------------+


```

-- Mostrar los modelos de coches y sus precios que no han sido vendidos aún:

  -- Cosas que debo de tener en cuenta:
    -- Coches que han sido vendidos.
    -- Quiero los coches que no han sido vendidos. NOT id_coche IN ventas

```sql
sqlite> SELECT 
    coches.modelo, 
    coches.precio
FROM 
    coches
WHERE 
    coches.id_coche NOT IN (SELECT id_coche FROM ventas);
+-------------+---------+
|   modelo    | precio  |
+-------------+---------+
| Pickup 2022 | 31000.0 |
+-------------+---------+


```

-- Calcular el total gastado por todos los clientes en coches:
  -- Cosas que debo de tener en cuenta:
    -- Me estan pidiendo la suma total de todos los coches vendidos, NO de aquellos que aún no se han vendido.


```sql
sqlite> SELECT 
    SUM(coches.precio) AS total_gastado
FROM 
    coches
JOIN 
    ventas ON coches.id_coche = ventas.id_coche;
+---------------+
| total_gastado |
+---------------+
| 259000.0      |
+---------------+
sqlite> 

```

-- Listar los coches vendidos junto con la fecha de venta y el nombre del cliente, ordenados por fecha de venta de forma descendente:
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. ¿Por qué campo tengo que ordenadar. Es uno o más campos?

```sql
sqlite> SELECT 
    coches.modelo AS modelo_coche,
    coches.precio AS precio_coche,
    ventas.fecha_venta,
    clientes.nombre AS nombre_cliente
FROM 
    ventas
JOIN 
    coches ON ventas.id_coche = coches.id_coche
JOIN 
    clientes ON ventas.id_cliente = clientes.id_cliente
ORDER BY 
    ventas.fecha_venta DESC;
+----------------+--------------+-------------+-----------------+
|  modelo_coche  | precio_coche | fecha_venta | nombre_cliente  |
+----------------+--------------+-------------+-----------------+
| Eléctrico 2021 | 40000.0      | 2023-10-05  | Elena Torres    |
| Deportivo 2023 | 35000.0      | 2023-08-25  | Isabel Díaz     |
| Híbrido 2022   | 27000.0      | 2023-07-20  | Miguel González |
| Compacto 2021  | 20000.0      | 2023-06-15  | Laura Sánchez   |
| Camioneta 2023 | 32000.0      | 2023-05-05  | Pedro Rodríguez |
| Coupé 2022     | 28000.0      | 2023-04-10  | Ana Martínez    |
| SUV 2023       | 30000.0      | 2023-03-25  | Carlos López    |
| Hatchback 2021 | 22000.0      | 2023-02-20  | María Gómez     |
| Sedán 2022     | 25000.0      | 2023-01-15  | Juan Pérez      |
+----------------+--------------+-------------+-----------------+
sqlite> 

```

-- Encontrar el modelo de coche más caro.
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. MAX

```sql
sqlite> SELECT 
    modelo, 
    precio
FROM 
    coches
WHERE 
    precio = (SELECT MAX(precio) FROM coches);
+----------------+---------+
|     modelo     | precio  |
+----------------+---------+
| Eléctrico 2021 | 40000.0 |
+----------------+---------+


```

-- Mostrar los clientes que han comprado al menos un coche (un coche o más) y la cantidad de coches comprados.
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. COUNT

```sql
sqlite> SELECT 
    clientes.nombre AS nombre_cliente,
    COUNT(ventas.id_coche) AS cantidad_coches_comprados
FROM 
    ventas
JOIN 
    clientes ON ventas.id_cliente = clientes.id_cliente
GROUP BY 
    clientes.id_cliente
HAVING 
    COUNT(ventas.id_coche) > 0;
+-----------------+---------------------------+
| nombre_cliente  | cantidad_coches_comprados |
+-----------------+---------------------------+
| Juan Pérez      | 1                         |
| María Gómez     | 1                         |
| Carlos López    | 1                         |
| Ana Martínez    | 1                         |
| Pedro Rodríguez | 1                         |
| Laura Sánchez   | 1                         |
| Miguel González | 1                         |
| Isabel Díaz     | 1                         |
| Elena Torres    | 1                         |
+-----------------+---------------------------+



```
-- Encontrar los clientes que han comprado coches de la marca 'Toyota':
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. Like | regexp | =. Tabla normalizada ?.

```sql
sqlite> SELECT 
    clientes.nombre AS nombre_cliente
FROM 
    ventas
JOIN 
    coches ON ventas.id_coche = coches.id_coche
JOIN 
    clientes ON ventas.id_cliente = clientes.id_cliente
WHERE 
    coches.marca = 'Toyota';
+----------------+
| nombre_cliente |
+----------------+
| Juan Pérez     |
+----------------+
sqlite> 

```
-- Calcular el promedio de edad de los clientes que han comprado coches de más de 25,000.
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. 

```sql
sqlite> SELECT 
    AVG(clientes.edad) AS promedio_edad
FROM 
    clientes
JOIN 
    ventas ON clientes.id_cliente = ventas.id_cliente
JOIN 
    coches ON ventas.id_coche = coches.id_coche
WHERE 
    coches.precio > 25000;
+------------------+
|  promedio_edad   |
+------------------+
| 32.8333333333333 |
+------------------+


```
-- Mostrar los modelos de coches y sus precios que fueron comprados por clientes mayores de 30 años.
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?.

```sql
sqlite> SELECT 
    coches.modelo AS modelo_coche,
    coches.precio AS precio_coche
FROM 
    ventas
JOIN 
    coches ON ventas.id_coche = coches.id_coche
JOIN 
    clientes ON ventas.id_cliente = clientes.id_cliente
WHERE 
    clientes.edad > 30;
+----------------+--------------+
|  modelo_coche  | precio_coche |
+----------------+--------------+
| SUV 2023       | 30000.0      |
| Camioneta 2023 | 32000.0      |
| Compacto 2021  | 20000.0      |
| Deportivo 2023 | 35000.0      |
+----------------+--------------+

```
-- Encontrar los coches vendidos en el año 2022 junto con la cantidad total de ventas en ese año.
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?.

```sql

SELECT 
    coches.modelo AS modelo_coche,
    COUNT(ventas.id_coche) AS cantidad_ventas
FROM 
    ventas
JOIN 
    coches ON ventas.id_coche = coches.id_coche
WHERE 
    ventas.fecha_venta REGEXP '^2022'
GROUP BY 
    coches.id_coche;
 nohay coches vendidso ese año.

```
-- Listar los coches cuyos precios son mayores que el precio promedio de coches vendidos a clientes menores de 30 años.
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. AVG

```sql

sqlite> SELECT 
    coches.modelo AS modelo_coche,
    coches.precio AS precio_coche
FROM 
    coches
WHERE 
    coches.precio > (
        SELECT 
            AVG(coches.precio)
        FROM 
            ventas
        JOIN 
            coches ON ventas.id_coche = coches.id_coche
        JOIN 
            clientes ON ventas.id_cliente = clientes.id_cliente
        WHERE 
            clientes.edad < 30
    );
+----------------+--------------+
|  modelo_coche  | precio_coche |
+----------------+--------------+
| SUV 2023       | 30000.0      |
| Camioneta 2023 | 32000.0      |
| Deportivo 2023 | 35000.0      |
| Pickup 2022    | 31000.0      |
| Eléctrico 2021 | 40000.0      |
+----------------+--------------+


```
-- Calcular el total de ventas por marca de coche, ordenado de forma descendente por el total de ventas:
  -- Cosas que debo de tener en cuenta:
    -- ¿Qué me están pidiendo?. COUNT| DESC|ASC precio

```sql
sqlite> SELECT 
    coches.marca AS marca_coche,
    COUNT(ventas.id_coche) AS total_ventas
FROM 
    ventas
JOIN 
    coches ON ventas.id_coche = coches.id_coche
GROUP BY 
    coches.marca
ORDER BY 
    total_ventas DESC;
+-------------+--------------+
| marca_coche | total_ventas |
+-------------+--------------+
| Volkswagen  | 1            |
| Toyota      | 1            |
| Tesla       | 1            |
| Nissan      | 1            |
| Mazda       | 1            |
| Hyundai     | 1            |
| Honda       | 1            |
| Ford        | 1            |
| Chevrolet   | 1            |
+-------------+--------------+

```