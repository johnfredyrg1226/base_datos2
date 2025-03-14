# Comandos y Consultas Básicas en SQLite3

## 1. Iniciar SQLite en la terminal

sh
sqlite3 nombre_base_de_datos.db


Si el archivo no existe, SQLite lo crea automáticamente.

---

## 2. Comandos básicos dentro de SQLite

| Comando                | Descripción                                     |
| ---------------------- | ----------------------------------------------- |
| .help                | Muestra todos los comandos disponibles.         |
| .databases           | Lista las bases de datos abiertas.              |
| .tables              | Muestra las tablas en la base de datos actual.  |
| .schema nombre_tabla | Muestra la estructura de una tabla.             |
| .mode column         | Muestra los resultados en formato de columna.   |
| .headers on          | Activa los encabezados de columna en la salida. |
| .exit o .quit      | Sale de SQLite.                                 |
| .modo table           | El resultado te sale como ujna tabla          |

---

## 3. Crear una tabla

sql
CREATE TABLE usuarios (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT NOT NULL,
    edad INTEGER
);


---

## 4. Insertar datos

sql
INSERT INTO usuarios (nombre, edad) VALUES ('Juan', 25);


---

## 5. Consultar datos

sql
SELECT * FROM usuarios;


---

## 6. Actualizar datos

sql
UPDATE usuarios SET edad = 26 WHERE nombre = 'Juan';


---

## 7. Eliminar datos

sql
DELETE FROM usuarios WHERE nombre = 'Juan';


---

## 8. Usar SQLite en Python

python
import sqlite3
import pandas as pd

conn = sqlite3.connect("nombre_base_de_datos.db")



---

## 9. Mejorar la visualización en la terminal

sh
.mode column
.headers on


Si tienes SQLite 3.33.0 o superior, puedes usar:

sh
.mode box
SELECT * FROM usuarios;


---

## 10. Herramientas para visualización

- [**DB Browser for SQLite**](https://sqlitebrowser.org/): Interfaz gráfica para explorar bases de datos.
- [**SQLite Viewer**](https://inloop.github.io/sqlite-viewer/): Herramienta online para ver bases de datos SQLite.

---