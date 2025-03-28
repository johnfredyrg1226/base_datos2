
<div align="justify">

## consultas REGEXP

## Objetivo

_Practicar la creación y manipulación de una base de datos SQLite3 desde la línea de comandos_.

## Descripción

## Pasos:

### Paso 1: Creación de la BBDD

## Crea con el siguente contenido el fichero biblioteca_db.sql.

<details> 
<summary style="color: red;" > Resultado </summary>

![Imagen de terminal creacion DDBB](https://raw.githubusercontent.com/johnfredyrg1226/base_datos2/main/tarea/Tema3_Realizacion_consultas_SQLite3/imagenes/tarea5_imagen_creacion_ddbb.png)

</details>


```SQL
-- Elimino la tabla autor si exite
DROP TABLE if EXISTS autor;
CREATE TABLE IF NOT EXISTS autor (
    id INTEGER PRIMARY KEY,
    nombre TEXT
);
-- Elimino la tabla libro si existe
DROP table if EXISTS libro;
CREATE TABLE IF NOT EXISTS libro (
    codigo INTEGER PRIMARY KEY,
    titulo TEXT,
    autor_id INTEGER,
    editorial TEXT,
    precio REAL,
    FOREIGN KEY (autor_id) REFERENCES autor(id)
);

INSERT INTO autor (nombre) VALUES
    ('J.K. Rowling'),
    ('Stephen King'),
    ('George Orwell'),
    ('Jane Austen'),
    ('Agatha Christie');

INSERT INTO libro (titulo, autor_id, editorial, precio) VALUES
    ('The Great Gatsby', 6, 'Charles Scribner''s Sons', 20.99),
    ('To Kill a Mockingbird', 7, 'J.B. Lippincott & Co.', 15.95),
    ('The Catcher in the Rye', 8, 'Little, Brown and Company', 18.75),
    ('One Hundred Years of Solitude', 9, 'Harper & Row', 22.50),
    ('Brave New World', 3, 'Chatto & Windus', 17.99),
    ('The Hobbit', 10, 'George Allen & Unwin', 24.99),
    ('The Lord of the Rings', 10, 'George Allen & Unwin', 35.50),
    ('The Chronicles of Narnia', 11, 'Geoffrey Bles', 28.99),
    ('The Odyssey', 12, 'Homer', 14.95),
    ('The Iliad', 12, 'Homer', 14.95),
    ('Moby-Dick', 13, 'Harper & Brothers', 19.99),
    ('The Road', 14, 'Alfred A. Knopf', 16.75),
    ('The Grapes of Wrath', 15, 'The Viking Press', 21.50),
    ('Wuthering Heights', 16, 'Emily Brontë', 12.99),
    ('The Old Man and the Sea', 17, 'Charles Scribner''s Sons', 18.95),
    ('The Count of Monte Cristo', 18, 'Pétion', 27.99),
    ('The Picture of Dorian Gray', 19, 'Ward, Lock, and Company', 14.50),
    ('The Adventures of Sherlock Holmes', 20, 'George Newnes', 16.99),
    ('Frankenstein', 21, 'Lackington, Hughes, Harding, Mavor, & Jones', 13.25),
    ('Alice''s Adventures in Wonderland', 22, 'Macmillan', 11.50),
    ('The Prince', 23, 'Niccolò Machiavelli', 10.99),
    ('Don Quixote', 24, 'Francisco de Robles', 26.75),
    ('The Divine Comedy', 25, 'Dante Alighieri', 20.50),
    ('Anna Karenina', 26, 'The Russian Messenger', 23.99),
    ('Les Misérables', 27, 'A. Lacroix, Verboeckhoven & Cie.', 29.75),
    ('The Jungle Book', 28, 'Macmillan Publishers', 14.99),
    ('The Wind in the Willows', 29, 'Methuen & Co.', 17.50),
    ('War and Peace', 26, 'The Russian Messenger', 33.25),
    ('Crime and Punishment', 30, 'The Russian Messenger', 19.99);
```
## PASO DOS PRACTICAR CON LAS CONSULTAS.



-- Selección de libros cuyo título comienza con "H".
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select titulo from libro
   ...> where titulo REGEXP '^[hH]';

sqlite> SELECT titulo FROM libro
WHERE titulo LIKE 'H%' OR titulo LIKE 'h%';

** no hay ningun titulo comience con H.
```
</details>

-- Libros escritos por autores cuyos nombres terminan con "ing".
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select nombre from autor
   ...> where nombre REGEXP 'ing$';
+--------------+
|    nombre    |
+--------------+
| J.K. Rowling |
| Stephen King |
+--------------+
```

</details>

-- Libros con títulos que contienen la palabra "and" en cualquier posición.
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Libros cuyo título comienza con una vocal.
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Libros cuyo autor tiene al menos una vocal repetida.
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Libros con precios que tienen dos dígitos decimales exactos.
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Libros cuyos títulos tienen al menos tres palabras.
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre empieza con la letra "A":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo título contiene la palabra "SQL":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre termina con "ez":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre tiene al menos 5 caracteres:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuya editorial es diferente de "EditorialX":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre contiene al menos una vocal:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo título comienza con una letra mayúscula:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre no contiene la letra "r":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuya editorial empieza con la letra "P":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre tiene exactamente 6 caracteres:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo título contiene al menos un número:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre inicia con una vocal:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre no contiene espacios en blanco:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo título termina con una vocal:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre contiene la secuencia "er":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo título empieza con la palabra "The":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre tiene al menos una letra mayúscula:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo precio es un número decimal con exactamente dos decimales:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre no contiene números:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo título contiene al menos tres vocales:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre inicia con una consonante:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Seleccionar los libros cuyo título no contiene la palabra "Science":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre tiene al menos una letra repetida consecutivamente:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre empieza con "M" o termina con "n":
<details> 
<summary style="color: red;" > Resultado </summary>

</details>
-- Obtener todos los autores cuyo nombre no contiene caracteres especiales:
<details> 
<summary style="color: red;" > Resultado </summary>

</details>



</div>

