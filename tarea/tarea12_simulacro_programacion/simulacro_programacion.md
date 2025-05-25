<div align="justify">

# <img src=../../../../../images/computer.png width="40"> Code, Learn & Practice("Simulacro de bbdd 🧪:  Índices, Vistas, Funciones y Procedimientos")

<div align="center">
<img src="https://www.seguridadkimika.eus/wp-content/uploads/2017/10/sirenas-seguridad-kimika-simulacro.jpg" width="200px"/>
</div>

## 🎯 Objetivo

Consolidar el uso de los principales componentes de MySQL:

- Índices
- Vistas
- Funciones
- Procedimientos

---

## 🧱 Enunciado del ejercicio

La empresa "TecnoMarket" quiere analizar las ventas realizadas por sus clientes. Para ello, necesita organizar la información en su base de datos y optimizar el rendimiento de las consultas.

### Tu tarea consiste en

1. Crear las tablas necesarias.
2. Insertar índices que mejoren las búsquedas más frecuentes.
3. Crear una vista que resuma las ventas.
4. Definir una función para calcular totales.
5. Crear un procedimiento que devuelva el resumen de ventas de un cliente específico.
6. Ejecutar el procedimiento para validar el resultado.

---

## 📘 Parte 1: Creación de tablas

```sql
DROP DATABASE IF EXISTS ventas;
CREATE DATABASE ventas;
USE ventas;

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

DROP TABLE IF EXISTS clientes;
CREATE TABLE clientes (
  id int NOT NULL,
  nombre varchar(100) DEFAULT NULL,
  correo varchar(100) DEFAULT NULL,
  ciudad varchar(50) DEFAULT NULL
);

INSERT INTO clientes (id, nombre, correo, ciudad) VALUES
(1, 'Ana Pérez', 'ana@example.com', 'Madrid'),
(2, 'Luis Gómez', 'luis@example.com', 'Barcelona'),
(3, 'Carla Ruiz', 'carla@example.com', 'Valencia'),
(4, 'Pedro Sánchez', 'pedro@example.com', 'Sevilla'),
(5, 'Lucía Martínez', 'lucia@example.com', 'Bilbao'),
(6, 'Jorge Torres', 'jorge@example.com', 'Madrid');

DROP TABLE IF EXISTS productos;
CREATE TABLE productos (
  id int NOT NULL,
  nombre varchar(100) DEFAULT NULL,
  precio decimal(10,2) DEFAULT NULL,
  categoria varchar(50) DEFAULT NULL
);

INSERT INTO productos (id, nombre, precio, categoria) VALUES
(1, 'Laptop', 1200.00, 'Electrónica'),
(2, 'Teléfono', 800.00, 'Electrónica'),
(3, 'Tablet', 500.00, 'Electrónica'),
(4, 'Auriculares', 150.00, 'Accesorios'),
(5, 'Monitor', 300.00, 'Periféricos'),
(6, 'Teclado', 50.00, 'Periféricos');

DROP TABLE IF EXISTS ventas;
CREATE TABLE ventas (
  id int NOT NULL,
  cliente_id int DEFAULT NULL,
  producto_id int DEFAULT NULL,
  fecha date DEFAULT NULL,
  cantidad int DEFAULT NULL
);

INSERT INTO ventas (id, cliente_id, producto_id, fecha, cantidad) VALUES
(1, 1, 1, '2024-05-01', 1),
(2, 2, 2, '2024-05-03', 2),
(3, 3, 3, '2024-05-05', 1),
(4, 4, 4, '2024-05-07', 3),
(5, 5, 5, '2024-05-10', 1),
(6, 6, 1, '2024-05-11', 1),
(7, 1, 6, '2024-05-12', 2),
(8, 2, 3, '2024-05-13', 1),
(9, 3, 2, '2024-05-14', 1),
(10, 4, 5, '2024-05-15', 2),
(11, 1, 2, '2024-05-16', 1);

COMMIT;

---

## 🔍 Parte 2: Creación de índices

Crea los siguientes clientes:

- **idx_ciudad** sobre la tabla clientes y el campo ciudad.
- **idx_fecha** sobre la tabla ventas, y el campo fecha.

use ventas;
create index idx_ciudad on clientes(ciudad);
create index idx_fecha on ventas(fecha);

RENDIMIENTO 



### ¿Preguntas?

- Crea los indices, muestra su rendimiento, y explica si son óptimos y por qué?.

| id | select\_type | table    | partitions | type | possible\_keys | key         | key\_len | ref   | rows | filtered | Extra |
| -- | ------------ | -------- | ---------- | ---- | -------------- | ----------- | -------- | ----- | ---- | -------- | ----- |
| 1  | SIMPLE       | clientes | NULL       | ref  | idx\_ciudad    | idx\_ciudad | 103      | const | 2    | 100.00   | NULL  |



| id | select\_type | table  | partitions | type | possible\_keys | key        | key\_len | ref   | rows | filtered | Extra |
| -- | ------------ | ------ | ---------- | ---- | -------------- | ---------- | -------- | ----- | ---- | -------- | ----- |
| 1  | SIMPLE       | ventas | NULL       | ref  | idx\_fecha     | idx\_fecha | 4        | const | 1    | 100.00   | NULL  |


---

## 👁️ Parte 3: Crear una vista

- **Obtén, a través de una vista**, la siguiente información detallada de cada venta:

- ID de la venta
- Nombre del cliente
- Producto vendido
- Fecha de la venta
- Cantidad comprada
- Total gastado (precio × cantidad)

La vista **vista** que consolida los datos de las tablas `ventas`, `clientes` y `productos`, permitiendo consultar fácilmente el historial de ventas detallado.

> **RECUERDA**: Una vista es una **consulta sql** encapsulada en una tabla ficticia.

use ventas;
create view detalle_venta AS
select v.id,c.nombre,p.id,v.fecha,v.cantidad, p.precio * v.cantidad as total
from ventas v
join clientes c on v.cliente_id = c.id
join productos p on v.producto_id = p.id

### 📊 Resultado esperado

| venta_id | cliente     | producto | fecha       | cantidad | total   |
|----------|-------------|----------|-------------|----------|---------|
| 1        | Ana Pérez   | Laptop   | 2024-05-01  | 1        | 1200.00 |
| 2        | Ana Pérez   | Teclado  | 2024-05-12  | 2        | 100.00  |
| 3        | Luis Gómez  | Monitor  | 2024-05-13  | 1        | 300.00  |
| 4        | Carla Ruiz  | Teclado  | 2024-05-14  | 1        | 50.00   |

---

## 🧮 Parte 4: Crear una función

Crea una **función almacenada** en MySQL llamada `calcular_total` que reciba los siguientes parámetros:

- `precio`: un valor decimal con dos decimales (precio del producto)
- `cantidad`: un número entero que representa las unidades compradas

La función debe devolver el resultado de multiplicar ambos valores, es decir, el **total a pagar** por esa línea de venta.
use ventas;
drop function if exists calcular_total;

delimiter $$
create FUNCTION calcular_total(p_precio decimal(10,2),p_cantidad int)
RETURNS decimal(10,2)
DETERMINISTIC
BEGIN  
    declare total decimal(10,2);
    set total = p_precio * p_cantidad;
    RETURN total;
end $$
delimiter ;

example: SELECT 
    precio_unitario,
    cantidad,
    calcular_total(precio_unitario, cantidad) AS total
FROM ventas;


```sql
SELECT calcular_total(1200.00, 2);
```

| calcular_total(1200.00, 2) |
|----------------------------|
| 2400.00                    |


---

## ⚙️ Parte 5: Crear un procedimiento

Crea un procedimiento llamado `resumen_cliente` que reciba como parámetro el **ID de un cliente** (`cliente_id`), y que devuelva el **historial de ventas** de dicho cliente.  
El procedimiento debe mostrar los siguientes datos por cada venta realizada por ese cliente:

- El **nombre del cliente**
- La **fecha de la venta**
- El **nombre del producto**
- La **cantidad comprada**
- El **total de la línea de venta**, calculado como `precio * cantidad`

💡 **Sugerencia:** Puedes reutilizar una función existente (como `calcular_total`) o calcular el total directamente en la consulta.

```sql
use ventas;
delimiter $$
create procedure resumen_cliente(in p_cliente_id int)
begin 
    select c.nombre as nombre_cliente,
    v.fecha,p.nombre as nombre_producto,
    v.cantidad as cantidad_comprada,
    p.precio * v.cantidad as historial_total_ventas
    from ventas v 
    join clientes c on c.id = v.cliente_id
    join productos p on p.id = v.producto_id
    where v.cliente_id = p_cliente_id;
    
end $$
delimiter ;
```

```sql
CALL resumen_cliente(1);
```

Con el siguiente resultado: 

| nombre     | fecha       | producto   | cantidad | total   |
|------------|-------------|------------|----------|---------|
| Ana Pérez | 2024-05-01  | Laptop     | 1        | 1200.00 |
| Ana Pérez | 2024-05-12  | Teclado    | 2        | 100.00  |

> *Este resultado depende de los datos que se hayan insertado en la base de datos.*

---

## ❓ Preguntas teóricas

1. ¿Qué ventajas ofrece el uso de una vista en lugar de una consulta con múltiples `JOIN`?
**Pues, usar una vista tiene sus ventajas. Por un lado, te ahorra tener que escribir y repetir consultas complejas cada vez que las necesitas, porque la vista ya guarda toda esa lógica. Si algún día quieres cambiar algo, solo tienes que modificar la vista, y no todas las consultas que la usan. Además, es más seguro dar acceso solo a la vista en vez de a las tablas originales, así proteges mejor los datos. Y lo que más me gusta es que simplifica todo para quien la usa, porque no tiene que saber ni cómo funcionan los JOIN ni cómo está armada la base de datos.**
2. ¿Por qué es importante declarar una función como `DETERMINISTIC`?
**Decir que una función es DETERMINISTIC es como decirle a la base de datos: “Oye, si le das estos mismos datos, siempre vas a devolver el mismo resultado”. Eso ayuda al motor a optimizar, porque puede guardar en memoria esos resultados y no tener que calcularlos otra vez cada vez que alguien llame la función. También es clave para poder usar la función en cosas como índices o vistas materializadas. Y además, evita que la función dé resultados locos si depende de algo externo que cambia.**
3. ¿Cuál es la diferencia entre una función y un procedimiento?
**Aunque parezcan parecidos, tienen diferencias importantes. La función siempre te devuelve un resultado y la puedes usar dentro de una consulta, como en un SELECT. En cambio, un procedimiento puede o no devolver algo, y no se usa dentro de las consultas; se ejecuta por separado. También las funciones solo reciben datos para entrar, pero los procedimientos pueden recibir y devolver datos con distintos tipos de parámetros. En resumen, la función sirve para hacer un cálculo y devolverlo, y el procedimiento para hacer tareas más complejas, como varios pasos o manejar transacciones.**
4. ¿Qué impacto tienen los índices sobre el rendimiento de una base de datos?
**Los índices son como los índices de un libro: te ayudan a encontrar la información mucho más rápido. Cuando haces búsquedas o filtras datos, son súper útiles. Pero ojo, que no todo es perfecto: cuando agregas, cambias o borras datos, el índice también tiene que actualizarse, y eso puede hacer que esas operaciones tarden un poco más. Además, ocupan espacio en la base de datos. Aun así, en general, hacen que las consultas sean más rápidas y eficientes.**
5. ¿Cuándo se recomienda usar un trigger en lugar de un procedimiento?
6. **Los triggers son ideales cuando quieres que algo suceda automáticamente justo después de un cambio en la base de datos, como insertar, actualizar o borrar algo. Por ejemplo, para validar datos o actualizar otras tablas sin que alguien tenga que acordarse de ejecutar un procedimiento manualmente. Los triggers funcionan solos, reaccionan a esos eventos. En cambio, los procedimientos siempre tienes que llamarlos explícitamente. Por eso, para acciones automáticas relacionadas con cambios en los datos, el trigger es lo mejor.**

---

## 📝 Preguntas prácticas

1. Modifica el procedimiento para filtrar también por un rango de fechas.

```sql
drop procedure if exists resumen_cliente;
delimiter $$
create procedure resumen_cliente(in p_cliente_id int,in p_fecha_inicio date, in p_fecha_fin date)
begin 
	select
    	c.nombre AS nombre_cliente,
        v.fecha,
        p.nombre AS nombre_producto,
        v.cantidad AS cantidad_comprada,
        p.precio * v.cantidad AS historial_total_ventas
     from ventas v
     join clientes c ON c.id = v.cliente_id
     join productos p ON p.id = v.producto_id
     where v.cliente_id = p_cliente_id
      AND v.fecha between  p_fecha_inicio and p_fecha_fin;

end;
delimiter;
```

2. Crea un índice sobre la columna `producto_id` en la tabla `ventas`.

```sql
use ventas;
create index idx_producto_id on ventas(producto_id);
```
3. ¿Qué ocurre si insertas una venta con un `cliente_id` inexistente?
**que devuelve un conjunto de valores vacio**
4. Modifica la vista para incluir también el nombre de la ciudad del cliente.

```sql
use ventas;
drop view if exists detalle_venta;

create view detalle_venta AS
select v.id,c.nombre,c.ciudad,p.id as producto,v.fecha,v.cantidad, p.precio * v.cantidad as total
from ventas v
join clientes c on v.cliente_id = c.id
join productos p on v.producto_id = p.id
```

5. Agrega una validación en el procedimiento para evitar resultados si el cliente no existe.

```sql
USE ventas;
DROP PROCEDURE IF EXISTS validacion_cliente;

DELIMITER $$

CREATE PROCEDURE validacion_cliente(IN p_clientes_id INT)
BEGIN
    -- Validar si el cliente existe
    IF EXISTS (SELECT * FROM clientes WHERE id = p_clientes_id) THEN
        SELECT 
            v.id,
            c.nombre,
            c.ciudad,
            p.id AS producto,
            v.fecha,
            v.cantidad,
            p.precio * v.cantidad AS total
        FROM ventas v
        JOIN clientes c ON v.cliente_id = c.id
        JOIN productos p ON v.producto_id = p.id
        WHERE c.id = p_clientes_id;  -- ← ¡Este punto y coma es crucial!
    ELSE
        SELECT 'Cliente no encontrado' AS mensaje;
    END IF;
END $$

DELIMITER ;

```
**llamar el procedimiento.**

```sql
CALL validacion_cliente(100);
```

---



</div>