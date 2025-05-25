<div style="text-align: justify;" >
## Introducción

### En primer lugar vamos a crear una base de datos llamada **ventas** para trabajar con ella. Los pasos que vamos a realizar es la eliminación si existe y luego crear e insertar datos.

```sql
DROP DATABASE IF EXISTS ventas;
CREATE DATABASE ventas;
USE ventas;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| alumnos            |
| ejemplo            |
| mysql              |
| performance_schema |
| revistas           |
| sys                |
| universidad        |
| ventas             |
+--------------------+

```

## Creación e inserción de datos

En siguiente paso sera la creación e inserción de datos dentro de la esta.

```sql
CREATE TABLE clientes ( ...
mysql> show tables;
+------------------+
| Tables_in_ventas |
+------------------+
| clientes         |
| empleados        |
| ventas           |
+------------------+

```

### Creando índicas

```sql
CREATE INDEX idx_ciudad ON clientes(ciudad);
CREATE INDEX idx_fecha ON ventas(fecha);
```

*obtendremos un resultado similar al siguiente*.

```console
 MySQL ha devuelto un conjunto de valores vacío (es decir: cero columnas). (La consulta tardó 0.0469 segundos.)
 ```
 
 ```sql
 resultado
mysql> create index idx_ciudad on clientes(ciudad);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> create index idx_fecha on  ventas(fecha);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

 ```

### ¿Cuál es su objetivo?

**Optimizar el rendimiento de las consultas que filtran o ordenan por estas columnas**.  
*Los índices permiten a MySQL encontrar los registros más rápidamente, sin escanear toda la tabla*.

### ¿Qué se obtiene?

- Consultas más rápidas al buscar clientes por ciudad o ventas por fecha  
- Mejora significativa en el tiempo de respuesta en bases de datos con gran volumen de datos


---

### 🧠 ¿Por qué cambiar el delimitador?

Cuando se crean **procedimientos almacenados**, **funciones**, **triggers** o **vistas complejas**, se necesita usar `;` dentro del bloque de código.  
Por eso, se cambia temporalmente el delimitador para evitar que MySQL interprete el `;` interno como el final de la instrucción.

---


## ❓ Preguntas teóricas sobre Índices en MySQL en un posible examen (reflexiona)

1. **¿Qué es un índice en MySQL y para qué se utiliza principalmente?**

Un índice es como el índice de un libro. Sirve para buscar datos más rápido sin tener que revisar fila por fila.

En MySQL, un índice acelera las búsquedas (SELECT), y también puede mejorar el rendimiento en filtros (WHERE), uniones (JOIN) y ordenamientos (ORDER BY).

2. **¿Qué diferencia hay entre un índice único (`UNIQUE`) y un índice normal? ¿Qué efecto tiene sobre los datos?**

🔹 Normal: Solo mejora la velocidad de búsqueda.
🔸 UNIQUE:Además de mejorar la búsqueda, no permite valores repetidos en esa columna o combinación de columnas.

3. **¿Qué tipo de columnas son buenas candidatas para tener un índice y por qué?**
Debes crear índices en columnas que:
Se usan mucho en:
cláusulas WHERE
condiciones de JOIN
ORDER BY
GROUP BY

Por ejemplo:
correo, usuario, DNI: porque buscas clientes por esos campos.

id_cliente en una tabla de ventas: porque se usa para unir con la tabla de clientes.

4. **¿Qué ocurre si aplicas una función como `UPPER()` o `YEAR()` sobre una columna indexada en una consulta? ¿Se sigue utilizando el índice?**

```sql
Se pierde el índice en la mayoría de los casos.
SELECT * FROM clientes WHERE UPPER(ciudad) = 'MADRID';
No utiliza el indice por que estas trasformando su valor.
```

5. **¿Cómo puedes verificar si una consulta está usando un índice y cuál está usando específicamente?**
6. 
```sql
EXPLAIN ANALYZE SELECT ...;
EXPLAIN ANALYZE SELECT * FROM clientes WHERE ciudad = 'Madrid';
```

**typo**    Tipo de acceso: ALL, ref, range, etc.
**rows**    Cuántas filas se estimaban leer.
**actual rows**   Cuántas filas se leyeron de verdad.
**filtered**  Porcentaje de filas que pasaron el filtro WHERE.
**cost, latency** Costo y tiempo real de ejecución.
**key**   Qué índice se usó.
**table** Qué tabla se leyó.

### PARA QUE SE CREAN LAS VISTAS

✅ Simplificar consultas complejas: encapsulan JOIN, filtros y cálculos para que no tengas que escribirlos cada vez.
🔒 Restringir acceso a datos sensibles: se pueden mostrar solo algunas columnas a ciertos usuarios.
🔁 Reutilizar lógica de negocio: se centraliza la definición de datos derivados como totales, promedios, relaciones, etc.
📐 Organizar consultas y estructuras: especialmente útil en aplicaciones grandes o con muchos informes.


CREATE VIEW vista_clientes_madrid AS
SELECT nombre, correo
FROM clientes
WHERE ciudad = 'Madrid';

SELECT * FROM vista_clientes_madrid;


## ¿Qué es una vista en MySQL y en qué se diferencia de una tabla?

Una vista es como una consulta guardada con nombre. Se comporta como una tabla, pero no guarda datos, solo muestra los resultados de una consulta cuando la usas.

Tabla	                         Vista
Guarda datos reales	            No guarda datos, solo una consulta
Puedes insertar directo	        A veces no se puede modificar
Tiene estructura propia	        Se basa en otras tablas

## ¿Qué ventajas ofrece el uso de vistas en consultas complejas y en la gestión de permisos de usuarios?

**Ventajas:**
**Simplicidad:** puedes reutilizar una consulta compleja sin escribirla cada vez.

**Seguridad:** puedes permitir que un usuario vea ciertos datos sin darle acceso directo a todas las tablas.

**Organización:** separa la lógica de negocio (consultas) del acceso a datos.

**Mantenimiento:** si cambias la consulta en la vista, no necesitas cambiarla en todos los reportes.



## ¿Qué limitaciones tiene una vista cuando se trata de insertar, actualizar o eliminar datos a través de ella?

```sql
No puedes modificar datos si la vista:
Usa JOIN, GROUP BY, DISTINCT o funciones de agregación (SUM(), COUNT(), etc.).
No incluye todas las columnas necesarias para una inserción o actualización.
Algunas vistas son solo de lectura (solo puedes hacer SELECT).

Las vistas más simples, basadas en una sola tabla y sin transformaciones, sí pueden permitir insertar o actualizar.
```

## Escribe la instrucción SQL para crear una vista que muestre el nombre del cliente y el total gastado, usando las tablas clientes, ventas y productos.

```sql
CREATE VIEW vista_total_gastos AS
SELECT c.nombre, SUM(v.cantidad * p.precio) AS total_gastado
FROM clientes c
JOIN ventas v ON c.id = v.id_cliente_id
JOIN productos p ON v.id_producto = p.id
GROUP BY c.id, c.nombre;

Query OK, 0 rows affected (0.00 sec)

```

## ¿Qué sucede si eliminas una vista que está siendo utilizada por otra vista o procedimiento almacenado? Explica brevemente.

```sql
Si otra vista o procedimiento usa la vista eliminada:
El procedimiento almacenado fallará al ejecutarse.
La otra vista también puede dejar de funcionar o lanzar errores cuando la consultes.
```

## Cómo ver los indices de la tabla

```sql
Usar SHOW INDEX
SHOW INDEX FROM nombre_tabla;
Ejemplo:

SHOW INDEX FROM clientes;
mysql> show index from ventas;
+--------+------------+-----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table  | Non_unique | Key_name  | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+--------+------------+-----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| ventas |          1 | ind_fecha |            1 | fecha       | A         |          11 |     NULL | NULL   | YES  | BTREE      |         |               |
| ventas |          1 | idx_fecha |            1 | fecha       | A         |          11 |     NULL | NULL   | YES  | BTREE      |         |               |
+--------+------------+-----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+


```

## Analizar el rendimiento de un índice

```sql
Usar EXPLAIN
EXPLAIN SELECT * FROM clientes WHERE ciudad = 'Madrid';

mysql> EXPLAIN SELECT * FROM clientes WHERE ciudad = 'Madrid';
+----+-------------+----------+------------+------+---------------+------------+---------+-------+------+----------+-------+
| id | select_type | table    | partitions | type | possible_keys | key        | key_len | ref   | rows | filtered | Extra |
+----+-------------+----------+------------+------+---------------+------------+---------+-------+------+----------+-------+
|  1 | SIMPLE      | clientes | NULL       | ref  | idx_ciudad    | idx_ciudad | 53      | const |    2 |   100.00 | NULL  |
+----+-------------+----------+------------+------+---------------+------------+---------+-------+------+----------+-------+
1 row in set, 1 warning (0.00 sec)


```

## Eliminación de índices

DROP INDEX idx_ciudad ON clientes;
DROP INDEX idx_fecha ON ventas;





</div>
