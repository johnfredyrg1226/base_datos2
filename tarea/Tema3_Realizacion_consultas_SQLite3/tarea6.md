## Code, Learn & Practice ( Base de datos (Trabajo con expresiones regulares y funciones matemáticas")

**Descripción**

**En la siguiente tarea se premia el uso de expresiones regulares en BBDD.**

## Realiza la lectura de la base de datos a través del fichero base datos de clientes.

```sql
-- Crear la tabla de Clientes
CREATE TABLE IF NOT EXISTS Clientes (
    id INTEGER PRIMARY KEY,
    nombre TEXT NOT NULL,
    email TEXT UNIQUE
);

-- Crear la tabla de Productos
CREATE TABLE IF NOT EXISTS Productos (
    id INTEGER PRIMARY KEY,
    nombre TEXT NOT NULL,
    precio REAL
);

-- Crear la tabla de Pedidos
CREATE TABLE IF NOT EXISTS Pedidos (
    id_pedido INTEGER PRIMARY KEY,
    id_cliente INTEGER,
    id_producto INTEGER,
    cantidad INTEGER,
    fecha_pedido DATE,
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id),
    FOREIGN KEY (id_producto) REFERENCES Productos(id)
);

INSERT INTO Clientes (nombre, email) VALUES
    ('Juan Pérez', 'juan@example.com'),
    ('María Gómez', 'maria@example.com'),
    ('Carlos López', 'carlos@example.com'),
    ('Ana Rodríguez', 'ana@example.com'),
    ('Luisa Martínez', 'luisa@example.com'),
    ('Pedro Sánchez', 'pedro@example.com'),
    ('Laura García', 'laura@example.com'),
    ('Miguel Martín', 'miguel@example.com'),
    ('Elena González', 'elena@example.com'),
    ('David Torres', 'david@example.com'),
    ('Sofía Ruiz', 'sofia@example.com'),
    ('Javier López', 'javier@example.com'),
    ('Carmen Vargas', 'carmen@example.com'),
    ('Daniel Muñoz', 'daniel@example.com'),
    ('Isabel Serrano', 'isabel@example.com'),
    ('Alejandro Muñoz', 'alejandro@example.com'),
    ('Raquel Herrera', 'raquel@example.com'),
    ('Francisco Mora', 'francisco@example.com'),
    ('Marina Díaz', 'marina@example.com'),
    ('Antonio Jiménez', 'antonio@example.com'),
    ('Beatriz Romero', 'beatriz@example.com'),
    ('Carlos Gómez', 'carlos.gomez@example.com'),
    ('Clara Sánchez', 'clara.sanchez@example.com'),
    ('Andrés Martínez', 'andres@example.com'),
    ('Lucía Díaz', 'lucia@example.com'),
    ('Mario Serrano', 'mario@example.com'),
    ('Eva Torres', 'eva.torres@example.com'),
    ('Roberto Ruiz', 'roberto@example.com'),
    ('Celia García', 'celia@example.com');

INSERT INTO productos (nombre, precio) VALUES
    ('Laptop', 1200.00),
    ('Smartphone', 699.99),
    ('TV LED', 799.50),
    ('Tablet', 299.99),
    ('Auriculares Bluetooth', 79.99),
    ('Impresora', 199.99),
    ('Cámara Digital', 499.99),
    ('Reproductor de Audio', 149.99),
    ('Altavoces Inalámbricos', 129.99),
    ('Reloj Inteligente', 249.99),
    ('Teclado Inalámbrico', 59.99),
    ('Ratón Óptico', 29.99),
    ('Monitor LED', 349.99),
    ('Mochila para Portátil', 49.99),
    ('Disco Duro Externo', 89.99),
    ('Router Wi-Fi', 69.99),
    ('Lámpara LED', 39.99),
    ('Batería Externa', 19.99),
    ('Estuche para Auriculares', 14.99),
    ('Tarjeta de Memoria', 24.99),
    ('Cargador Inalámbrico', 34.99),
    ('Kit de Limpieza para Computadoras', 9.99),
    ('Funda para Tablet', 19.99),
    ('Soporte para Teléfono', 14.99),
    ('Hub USB', 29.99),
    ('Webcam HD', 59.99),
    ('Funda para Laptop', 29.99),
    ('Adaptador HDMI', 12.99);
INSERT INTO Pedidos (id_cliente, id_producto, cantidad, fecha_pedido) VALUES
    (1, 1, 2, '2024-02-01'),
    (2, 2, 1, '2024-02-02'),
    (3, 3, 3, '2024-02-03'),
    (4, 4, 1, '2024-02-04'),
    (5, 5, 2, '2024-02-05'),
    (6, 6, 1, '2024-02-06'),
    (7, 7, 3, '2024-02-07'),
    (8, 8, 2, '2024-02-08'),
    (9, 9, 1, '2024-02-09'),
    (10, 10, 2, '2024-02-10'),
    (11, 11, 1, '2024-02-11'),
    (12, 12, 3, '2024-02-12'),
    (13, 13, 1, '2024-02-13'),
    (14, 14, 2, '2024-02-14'),
    (15, 15, 1, '2024-02-15'),
    (16, 16, 3, '2024-02-16'),
    (17, 17, 2, '2024-02-17'),
    (18, 18, 1, '2024-02-18'),
    (19, 19, 2, '2024-02-19'),
    (20, 20, 1, '2024-02-20'),
    (21, 21, 3, '2024-02-21'),
    (22, 22, 1, '2024-02-22'),
    (23, 23, 2, '2024-02-23'),
    (24, 24, 1, '2024-02-24'),
    (25, 25, 3, '2024-02-25'),
    (26, 26, 2, '2024-02-26'),
    (27, 27, 1, '2024-02-27'),
    (28, 28, 2, '2024-02-28'),
    (29, 29, 1, '2024-02-29'),
    (30, 30, 3, '2024-03-01');
```

## Realiza el listado de consultas que se encuentran en el fichero consultas-bd.

**Obtener todos los clientes.**  

```sql
sqlite> select * from clientes;
+----+-----------------+---------------------------+
| id |     nombre      |           email           |
+----+-----------------+---------------------------+
| 1  | Juan Pérez      | juan@example.com          |
| 2  | María Gómez     | maria@example.com         |
| 3  | Carlos López    | carlos@example.com        |
| 4  | Ana Rodríguez   | ana@example.com           |
| 5  | Luisa Martínez  | luisa@example.com         |
| 6  | Pedro Sánchez   | pedro@example.com         |
| 7  | Laura García    | laura@example.com         |
| 8  | Miguel Martín   | miguel@example.com        |
| 9  | Elena González  | elena@example.com         |
| 10 | David Torres    | david@example.com         |
| 11 | Sofía Ruiz      | sofia@example.com         |
| 12 | Javier López    | javier@example.com        |
| 13 | Carmen Vargas   | carmen@example.com        |
| 14 | Daniel Muñoz    | daniel@example.com        |
| 15 | Isabel Serrano  | isabel@example.com        |
| 16 | Alejandro Muñoz | alejandro@example.com     |
| 17 | Raquel Herrera  | raquel@example.com        |
| 18 | Francisco Mora  | francisco@example.com     |
| 19 | Marina Díaz     | marina@example.com        |
| 20 | Antonio Jiménez | antonio@example.com       |
| 21 | Beatriz Romero  | beatriz@example.com       |
| 22 | Carlos Gómez    | carlos.gomez@example.com  |
| 23 | Clara Sánchez   | clara.sanchez@example.com |
| 24 | Andrés Martínez | andres@example.com        |
| 25 | Lucía Díaz      | lucia@example.com         |
| 26 | Mario Serrano   | mario@example.com         |
| 27 | Eva Torres      | eva.torres@example.com    |
| 28 | Roberto Ruiz    | roberto@example.com       |
| 29 | Celia García    | celia@example.com         |

```

**Obtener la cantidad total de productos en todos los pedidos.**  

```sql
sqlite> select sum(cantidad) as Suma_total_productos from pedidos;
+----------------------+
| Suma_total_productos |
+----------------------+
| 54                   |
+----------------------+

```

**Obtener el precio promedio de los productos.**  
```sql
sqlite> select avg(precio)as precio_promedio_productos from productos;
+---------------------------+
| precio_promedio_productos |
+---------------------------+
| 188.294285714286          |
+---------------------------+
```

**Obtener los clientes que tienen un email válido (contiene '@').** 
 
```sql
SELECT * FROM Clientes WHERE email REGEXP '@';
```

**Obtener el producto más caro.**  
```sql```

**Obtener los pedidos realizados en febrero de 2024.**  
```sql```

**Obtener la cantidad total de productos en todos los pedidos por producto.**  
```sql```

**Obtener los clientes que han realizado más de un pedido.**  
```sql```

**Obtener los productos que tienen un precio registrado.**  
```sql```

**Obtener la fecha del primer pedido realizado.**  
```sql```

**Obtener los productos cuyos nombres comienzan con 'A' o 'B'.**  
```sql```

**Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cliente.**  
```sql```

**Obtener los clientes que han realizado más de un pedido en febrero de 2024.**  
```sql```

**Obtener los productos con precio entre 100 y 500.**  
```sql```

**Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cantidad descendente.**  
```sql```

**Obtener los clientes que tienen una 'a' en cualquier posición de su nombre.**  
```sql```

**Obtener el precio máximo de los productos.**  
```sql```

**Obtener los pedidos realizados por el cliente con ID 1 en febrero de 2024.**  
```sql```

**Obtener la cantidad total de productos en todos los pedidos por producto ordenado por total de productos descendente.**  
```sql```

**Obtener los productos que no tienen un precio registrado.**  
```sql```

**Obtener la fecha del último pedido realizado.**  
```sql```

**Obtener los clientes cuyo nombre tiene al menos 5 caracteres.**  
```sql```

**Obtener los productos que tienen la letra 'o' en cualquier posición del nombre.**  
```sql```

**Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cliente.**  
```sql```

**Obtener los clientes cuyos nombres no contienen la letra 'i'.**  
```sql```

**Obtener**

