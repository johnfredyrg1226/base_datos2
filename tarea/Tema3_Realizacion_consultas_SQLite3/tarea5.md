
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

```sql
sqlite> select titulo from libro 
   ...> where titulo REGEXP 'and';
   
+----------------------------------+
|              titulo              |
+----------------------------------+
| The Old Man and the Sea          |
| Alice's Adventures in Wonderland |
| War and Peace                    |
| Crime and Punishment             |
+----------------------------------+
```

</details>
-- Libros cuyo título comienza con una vocal.
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select titulo from libro
   ...> where titulo REGEXP '^[AEIOU]';
+----------------------------------+
|              titulo              |
+----------------------------------+
| One Hundred Years of Solitude    |
| Alice's Adventures in Wonderland |
| Anna Karenina                    |
+----------------------------------+

```
</details>
-- Libros cuyo autor tiene al menos una vocal repetida.
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> SELECT nombre 
FROM autor
WHERE nombre REGEXP '(a.*a|e.*e|i.*i|o.*o|u.*u)';
+-----------------+
|     nombre      |
+-----------------+
| Stephen King    |
| George Orwell   |
| Jane Austen     |
| Agatha Christie |
+-----------------+

```

</details>
-- Libros con precios que tienen dos dígitos decimales exactos.
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> SELECT precio 
FROM libro 
WHERE (precio * 100) = CAST(precio * 100 AS INTEGER);
+--------+
| precio |
+--------+
| 20.99  |
| 15.95  |
| 18.75  |
| 22.5   |
| 24.99  |
| 35.5   |
| 28.99  |
| 14.95  |
| 14.95  |
| 16.75  |
| 21.5   |
| 12.99  |
| 18.95  |
| 27.99  |
| 14.5   |
| 13.25  |
| 11.5   |
| 10.99  |
| 26.75  |
| 20.5   |
| 23.99  |
| 29.75  |
| 14.99  |
| 17.5   |
| 33.25  |
+--------+
El CAST() en SQL se usa para convertir un tipo de dato en otro. En nuestro caso, lo usamos para convertir un número decimal (REAL) en un número entero (INTEGER).
```

</details>
-- Libros cuyos títulos tienen al menos tres palabras.
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
WHERE titulo REGEXP '^[^ ]+ [^ ]+ [^ ]+';
+-----------------------------------+
|              titulo               |
+-----------------------------------+
| The Great Gatsby                  |
| To Kill a Mockingbird             |
| The Catcher in the Rye            |
| One Hundred Years of Solitude     |
| Brave New World                   |
| The Lord of the Rings             |
| The Chronicles of Narnia          |
| The Grapes of Wrath               |
| The Old Man and the Sea           |
| The Count of Monte Cristo         |
| The Picture of Dorian Gray        |
| The Adventures of Sherlock Holmes |
| Alice's Adventures in Wonderland  |
| The Divine Comedy                 |
| The Jungle Book                   |
| The Wind in the Willows           |
| War and Peace                     |
| Crime and Punishment              |
+-----------------------------------+
```

</details>
-- Obtener todos los autores cuyo nombre empieza con la letra "A":
<details> 
<summary style="color: red;" > Resultado </summary>

```sql 
sqlite> select nombre from autor
   ...> where nombre REGEXP  '^[A]';
+-----------------+
|     nombre      |
+-----------------+
| Agatha Christie |
+-----------------+
sqlite> 
```

</details>
-- Seleccionar los libros cuyo título contiene la palabra "SQL":
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> SELECT titulo FROM libro 
WHERE titulo REGEXP '\\bSQL\\b';
```

</details>
-- Obtener todos los autores cuyo nombre termina con "ez":
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select titulo from libro 
   ...> where titulo REGEXP 'ez$';
sqlite> SELECT nombre FROM autor
WHERE nombre LIKE '%ez';
```

</details>
-- Obtener todos los autores cuyo nombre tiene al menos 5 caracteres:
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select nombre from autor
   ...> where nombre REGEXP '^.{5,}$';
+-----------------+
|     nombre      |
+-----------------+
| J.K. Rowling    |
| Stephen King    |
| George Orwell   |
| Jane Austen     |
| Agatha Christie |
+-----------------+
```

</details>
-- Seleccionar los libros cuya editorial es diferente de "EditorialX":
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> SELECT * FROM libro
WHERE editorial NOT REGEXP '^EditorialX$';
+--------+-----------------------------------+----------+---------------------------------------------+--------+
| codigo |              titulo               | autor_id |                  editorial                  | precio |
+--------+-----------------------------------+----------+---------------------------------------------+--------+
| 1      | The Great Gatsby                  | 6        | Charles Scribner's Sons                     | 20.99  |
| 2      | To Kill a Mockingbird             | 7        | J.B. Lippincott & Co.                       | 15.95  |
| 3      | The Catcher in the Rye            | 8        | Little, Brown and Company                   | 18.75  |
| 4      | One Hundred Years of Solitude     | 9        | Harper & Row                                | 22.5   |
| 5      | Brave New World                   | 3        | Chatto & Windus                             | 17.99  |
| 6      | The Hobbit                        | 10       | George Allen & Unwin                        | 24.99  |
| 7      | The Lord of the Rings             | 10       | George Allen & Unwin                        | 35.5   |
| 8      | The Chronicles of Narnia          | 11       | Geoffrey Bles                               | 28.99  |
| 9      | The Odyssey                       | 12       | Homer                                       | 14.95  |
| 10     | The Iliad                         | 12       | Homer                                       | 14.95  |
| 11     | Moby-Dick                         | 13       | Harper & Brothers                           | 19.99  |
| 12     | The Road                          | 14       | Alfred A. Knopf                             | 16.75  |
| 13     | The Grapes of Wrath               | 15       | The Viking Press                            | 21.5   |
| 14     | Wuthering Heights                 | 16       | Emily Brontë                                | 12.99  |
| 15     | The Old Man and the Sea           | 17       | Charles Scribner's Sons                     | 18.95  |
| 16     | The Count of Monte Cristo         | 18       | Pétion                                      | 27.99  |
| 17     | The Picture of Dorian Gray        | 19       | Ward, Lock, and Company                     | 14.5   |
| 18     | The Adventures of Sherlock Holmes | 20       | George Newnes                               | 16.99  |
| 19     | Frankenstein                      | 21       | Lackington, Hughes, Harding, Mavor, & Jones | 13.25  |
| 20     | Alice's Adventures in Wonderland  | 22       | Macmillan                                   | 11.5   |
| 21     | The Prince                        | 23       | Niccolò Machiavelli                         | 10.99  |
| 22     | Don Quixote                       | 24       | Francisco de Robles                         | 26.75  |
| 23     | The Divine Comedy                 | 25       | Dante Alighieri                             | 20.5   |
| 24     | Anna Karenina                     | 26       | The Russian Messenger                       | 23.99  |
| 25     | Les Misérables                    | 27       | A. Lacroix, Verboeckhoven & Cie.            | 29.75  |
| 26     | The Jungle Book                   | 28       | Macmillan Publishers                        | 14.99  |
| 27     | The Wind in the Willows           | 29       | Methuen & Co.                               | 17.5   |
| 28     | War and Peace                     | 26       | The Russian Messenger                       | 33.25  |
| 29     | Crime and Punishment              | 30       | The Russian Messenger                       | 19.99  |
+--------+-----------------------------------+----------+---------------------------------------------+--------+
```

</details>
-- Obtener todos los autores cuyo nombre contiene al menos una vocal:
<details> 
<summary style="color: red;" > Resultado </summary>
```sql
sqlite> select nombre from autor 
   ...> where nombre REGEXP '[AEIOUaeiou]';
+-----------------+
|     nombre      |
+-----------------+
| J.K. Rowling    |
| Stephen King    |
| George Orwell   |
| Jane Austen     |
| Agatha Christie |
+-----------------+
```

</details>
-- Seleccionar los libros cuyo título comienza con una letra mayúscula:
<details> 
<summary style="color: red;" > Resultado </summary>
```sql
sqlite> select titulo from libro
   ...> where titulo REGEXP '^[A-Z]';
+-----------------------------------+
|              titulo               |
+-----------------------------------+
| The Great Gatsby                  |
| To Kill a Mockingbird             |
| The Catcher in the Rye            |
| One Hundred Years of Solitude     |
| Brave New World                   |
| The Hobbit                        |
| The Lord of the Rings             |
| The Chronicles of Narnia          |
| The Odyssey                       |
| The Iliad                         |
| Moby-Dick                         |
| The Road                          |
| The Grapes of Wrath               |
| Wuthering Heights                 |
| The Old Man and the Sea           |
| The Count of Monte Cristo         |
| The Picture of Dorian Gray        |
| The Adventures of Sherlock Holmes |
| Frankenstein                      |
| Alice's Adventures in Wonderland  |
| The Prince                        |
| Don Quixote                       |
| The Divine Comedy                 |
| Anna Karenina                     |
| Les Misérables                    |
| The Jungle Book                   |
| The Wind in the Willows           |
| War and Peace                     |
| Crime and Punishment              |
+-----------------------------------+
```

</details>
-- Obtener todos los autores cuyo nombre no contiene la letra "r":
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> SELECT nombre FROM autor
WHERE nombre NOT REGEXP '[rR]';
+--------------+
|    nombre    |
+--------------+
| Stephen King |
| Jane Austen  |
+--------------+
```
</details>
-- Seleccionar los libros cuya editorial empieza con la letra "P":
<details> 
<summary style="color: red;" > Resultado </summary>
```sql
sqlite> select editorial from libro 
   ...> where editorial regexp '^P';
+-----------+
| editorial |
+-----------+
| Pétion    |
+-----------+
```

</details>
-- Obtener todos los autores cuyo nombre tiene exactamente 6 caracteres:
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select nombre from autor
   ...> where nombre regexp '^.{6}&';
```

</details>
-- Seleccionar los libros cuyo título contiene al menos un número:
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> SELECT titulo FROM libro
WHERE titulo REGEXP '\d';
```

</details>
-- Obtener todos los autores cuyo nombre inicia con una vocal:
<details> 
<summary style="color: red;" > Resultado </summary>

```sql 
sqlite> select nombre from autor
   ...> where nombre regexp '^[aeiouAEIOU]';
+-----------------+
|     nombre      |
+-----------------+
| Agatha Christie |
+-----------------+
```

</details>
-- Obtener todos los autores cuyo nombre no contiene espacios en blanco:
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select nombre from autor
   ...> where nombre not regexp ' ';
El patrón ' ' busca un único espacio en blanco, lo que debería funcionar para excluir a los nombres que contengan espacios

SELECT nombre FROM autor
WHERE nombre NOT REGEXP '\\s';
📌 Explicación del patrón \\s:
\\s → Coincide con cualquier carácter de espacio en blanco (esto incluye espacios, tabuladores, saltos de línea, etc.).

NOT REGEXP '\\s' asegura que no haya ningún tipo de espacio en blanco en el nombre.
```

</details>
-- Seleccionar los libros cuyo título termina con una vocal:
<details> 
<summary style="color: red;" > Resultado </summary>

```sql 
sqlite> select titulo from libro
   ...> where titulo regexp '[aeiouAEIOU]$';
+-------------------------------+
|            titulo             |
+-------------------------------+
| The Catcher in the Rye        |
| One Hundred Years of Solitude |
| The Chronicles of Narnia      |
| The Old Man and the Sea       |
| The Count of Monte Cristo     |
| The Prince                    |
| Don Quixote                   |
| Anna Karenina                 |
| War and Peace                 |
+-------------------------------+
```

</details>
-- Obtener todos los autores cuyo nombre contiene la secuencia "er":
<details> 
<summary style="color: red;" > Resultado </summary>

```sql
sqlite> select nombre from autor 
   ...> where nombre regexp 'er';

sqlite> SELECT nombre FROM autor
WHERE LOWER(nombre) REGEXP 'er';

```

</details>
-- Seleccionar los libros cuyo título empieza con la palabra "The":
<details> 
<summary style="color: red;" > Resultado </summary>

```sql 
sqlite> select titulo from libro
   ...> where titulo regexp '^[The]';
+-----------------------------------+
|              titulo               |
+-----------------------------------+
| The Great Gatsby                  |
| To Kill a Mockingbird             |
| The Catcher in the Rye            |
| The Hobbit                        |
| The Lord of the Rings             |
| The Chronicles of Narnia          |
| The Odyssey                       |
| The Iliad                         |
| The Road                          |
| The Grapes of Wrath               |
| The Old Man and the Sea           |
| The Count of Monte Cristo         |
| The Picture of Dorian Gray        |
| The Adventures of Sherlock Holmes |
| The Prince                        |
| The Divine Comedy                 |
| The Jungle Book                   |
| The Wind in the Willows           |
+-----------------------------------+
```

</details>
-- Obtener todos los autores cuyo nombre tiene al menos una letra mayúscula:

```sql
sqlite> select nombre from autor 
   ...> where nombre regexp '[A-Z]'
   ...> ;
+-----------------+
|     nombre      |
+-----------------+
| J.K. Rowling    |
| Stephen King    |
| George Orwell   |
| Jane Austen     |
| Agatha Christie |
+-----------------+

```

-- Seleccionar los libros cuyo precio es un número decimal con exactamente dos decimales:

```sql
sqlite> SELECT titulo, precio FROM libro
WHERE precio REGEXP '^\d+\.\d{2}$';
+-----------------------------------+--------+
|              titulo               | precio |
+-----------------------------------+--------+
| The Great Gatsby                  | 20.99  |
| To Kill a Mockingbird             | 15.95  |
| The Catcher in the Rye            | 18.75  |
| Brave New World                   | 17.99  |
| The Hobbit                        | 24.99  |
| The Chronicles of Narnia          | 28.99  |
| The Odyssey                       | 14.95  |
| The Iliad                         | 14.95  |
| Moby-Dick                         | 19.99  |
| The Road                          | 16.75  |
| Wuthering Heights                 | 12.99  |
| The Old Man and the Sea           | 18.95  |
| The Count of Monte Cristo         | 27.99  |
| The Adventures of Sherlock Holmes | 16.99  |
| Frankenstein                      | 13.25  |
| The Prince                        | 10.99  |
| Don Quixote                       | 26.75  |
| Anna Karenina                     | 23.99  |
| Les Misérables                    | 29.75  |
| The Jungle Book                   | 14.99  |
| War and Peace                     | 33.25  |
| Crime and Punishment              | 19.99  |
+-----------------------------------+--------+

```
## Obtener todos los autores cuyo nombre no contiene números:

```sql
sqlite> select nombre from autor 
   ...> where nombre not regexp '[0-9]';
+-----------------+
|     nombre      |
+-----------------+
| J.K. Rowling    |
| Stephen King    |
| George Orwell   |
| Jane Austen     |
| Agatha Christie |
+-----------------+
```
## Seleccionar los libros cuyo título contiene al menos tres vocales:

```sql
sqlite> SELECT titulo FROM libro
WHERE titulo REGEXP '[aeiouAEIOU].*[aeiouAEIOU].*[aeiouAEIOU]';
+-----------------------------------+
|              titulo               |
+-----------------------------------+
| The Great Gatsby                  |
| To Kill a Mockingbird             |
| The Catcher in the Rye            |
| One Hundred Years of Solitude     |
| Brave New World                   |
| The Hobbit                        |
| The Lord of the Rings             |
| The Chronicles of Narnia          |
| The Odyssey                       |
| The Iliad                         |
| The Road                          |
| The Grapes of Wrath               |
| Wuthering Heights                 |
| The Old Man and the Sea           |
| The Count of Monte Cristo         |
| The Picture of Dorian Gray        |
| The Adventures of Sherlock Holmes |
| Frankenstein                      |
| Alice's Adventures in Wonderland  |
| The Prince                        |
| Don Quixote                       |
| The Divine Comedy                 |
| Anna Karenina                     |
| Les Misérables                    |
| The Jungle Book                   |
| The Wind in the Willows           |
| War and Peace                     |
| Crime and Punishment              |
+-----------------------------------+

```
## Obtener todos los autores cuyo nombre inicia con una consonante:

```sql
SELECT nombre FROM autor
WHERE nombre REGEXP '^[^aeiouAEIOU]';


```
## Seleccionar los libros cuyo título no contiene la palabra "Science":

```sql
sqlite> SELECT nombre FROM autor
WHERE nombre REGEXP '^[^aeiouAEIOU]';
+---------------+
|    nombre     |
+---------------+
| J.K. Rowling  |
| Stephen King  |
| George Orwell |
| Jane Austen   |
+---------------+

```
## Obtener todos los autores cuyo nombre tiene al menos una letra repetida consecutivamente:

```sql
SELECT nombre FROM autor
WHERE nombre REGEXP '(.)\1';

Explicación del patrón (.)\1:
(.) → Captura cualquier carácter (letra, número o símbolo).

\1 → Hace referencia al mismo carácter capturado antes, es decir, busca una repetición consecutiva de cualquier carácter.
```
## Obtener todos los autores cuyo nombre empieza con "M" o termina con "n":

```sql
SELECT nombre FROM autor
WHERE nombre REGEXP '^M|n$';

Explicación del patrón '^M|n$':
^M → Coincide con nombres que comienzan con "M" (^ indica el inicio).

n$ → Coincide con nombres que terminan con "n" ($ indica el final).

| → Es el operador "o" en expresiones regulares, por lo que se cumple cualquiera de las dos condiciones.
```
## Obtener todos los autores cuyo nombre no contiene caracteres especiales:

```sql
sqlite> SELECT nombre FROM autor
WHERE nombre NOT REGEXP '[^a-zA-Z ]';
+-----------------+
|     nombre      |
+-----------------+
| Stephen King    |
| George Orwell   |
| Jane Austen     |
| Agatha Christie |
+-----------------+

 Explicación del patrón [^a-zA-Z ]:
[^...] → La negación dentro de corchetes significa "buscar cualquier carácter que no esté en esta lista".

a-zA-Z → Permite solo letras mayúsculas y minúsculas.

' ' (espacio) → Permite espacios en los nombres compuestos.

NOT REGEXP → Filtra los nombres que no contienen caracteres especiales.
```


</div>

