## BASE DE DATOS



##### Mostrar las bases de datos disponibles:
SHOW DATABASES;

##### Seleccionar una base de datos:
USE <nombre_de_base_de_datos>;

##### Mostrar las tablas en una base de datos:
SHOW TABLES;

##### Mostrar la estructura de una tabla:
DESCRIBE <nombre_de_tabla>;

##### Ver los registros de una tabla:
SELECT * FROM <nombre_de_tabla>;

##### Crear una nueva base de datos:
CREATE DATABASE <nombre_de_base_de_datos>;

##### modificar tabla y colocar primari key(despues de crear tabla)
ALTER TABLE cliente
ADD PRIMARY KEY (documento);



Crear una nueva tabla:
##### CREATE TABLE <nombre_de_tabla> (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(255),
    edad INT
);

##### Insertar datos en una tabla:
INSERT INTO <nombre_de_tabla> (nombre, edad)
VALUES ('Juan', 30);

##### Actualizar datos en una tabla:
UPDATE <nombre_de_tabla>
SET nombre = 'Carlos', edad = 35
WHERE id = 1;

#####  Eliminar datos de una tabla:
DELETE FROM <nombre_de_tabla>
WHERE id = 1;

##### Eliminar una tabla:
 DROP TABLE <nombre_de_tabla>;

 ##### Eliminar una base de datos:
 DROP DATABASE <nombre_de_base_de_datos>;

 ## Ver los índices de una tabla:
```sql
SHOW INDEXES FROM <nombre_de_tabla>;
show index from alumno;
```

##### Crear un índice en una columna:
```sql
CREATE INDEX <nombre_del_indice> ON <nombre_de_tabla> (<columna>);
```
##### Crear un índice único (asegura que los valores en la columna sean únicos):
```sql
CREATE UNIQUE INDEX <nombre_del_indice> ON <nombre_de_tabla> (<columna>);
```
##### Crear un índice compuesto (índice en varias columnas):
```sql
CREATE INDEX <nombre_del_indice> ON <nombre_de_tabla> (<columna1>, <columna2>);
```
##### Eliminar un índice de una tabla:
DROP INDEX <nombre_del_indice> ON <nombre_de_tabla>;


##### Crear un índice en una columna con FULLTEXT (para búsqueda de texto completo):
CREATE FULLTEXT INDEX <nombre_del_indice> ON <nombre_de_tabla> (<columna>);

##### Índice de Clave Foránea (FOREIGN KEY INDEX)
```sql
CREATE TABLE pedidos (
    id INT PRIMARY KEY,
    cliente_id INT,
    FOREIGN KEY(cliente_id) REFERENCES clientes(id)
);

```

