<div align="justify">

## Code, Learn & Practice Base de datos  Creación de la Base de Datos

<div align="center">
<img src="https://i0.wp.com/hunna.org/wp-content/uploads/2014/06/huellas.jpg?resize=324%2C215" width="500px"/>
</div>

## Objetivo

_Practicar la creación y manipulación de una base de datos SQLite3 desde la línea de comandos_.

## Descripción

## Pasos

### Paso 1: Crear una tabla con un campo de cada tipo

1. Utilizando la terminal o línea de comandos, abre SQLite3 y crea una base de datos llamada `tarea2.db`.
   <details>
   <summary style=" color: red;"> RESULTADO </summary>

   **jramg23@jramg23-GL62-7QF:~$ sqlite3 tarea2.db
SQLite version 3.45.1 2024-01-30 16:01:20
Enter ".help" for usage hints.
sqlite>** 
   </details>

2. Dentro de SQLite3, crea las siguientes tablas

- __Propietarios__: Almacena información de los propietarios.
  - __id__ INTEGER ENTERO clave primaria y AUTOINCREMENT.
  - __nombre__ TEXT no nulo.
  - __apellido__ TEXT no nulo.
  - __dni__ TEXT Valor único. 
  - __Vehiculos__: Almacena información sobre los propietarios de los vehículos.
  - __id__ INTEGER ENTERO clave primaria y AUTOINCREMENT.
  - __marca__ TEXT no nulo.
  - __modelo__ TEXT no nulo.
  - __anio__ INTEGER no nulo.
  - __id_propietario__ INTEGER, FK propietarios(id_propietario). 

>__Nota__: Un propietario puede tener varios vehículos, pero un vehículo pertenece a un único propietario.
<details>
<summary style="color: red;"> RESULTADO </summary>

**sqlite> create table Propietarios(id integer primary key autoincrement,
(x1...> nombre text not null,
(x1...> apellido text not null,
(x1...> dni text unique);
sqlite> .tables
Propietarios
sqlite>**


**CREATE TABLE Vehiculos (
    id_vehiculo INTEGER PRIMARY KEY AUTOINCREMENT,
    marca TEXT NOT NULL,
    modelo TEXT NOT NULL,
    anio INTEGER NOT NULL,
    id_propietario INTEGER,  
    FOREIGN KEY (id_propietario) REFERENCES Propietarios(id)
);**


</details>

Asegúrate de cerrar SQLite3 al finalizar.

>__Nota__: Ayudate de los [apuntes](https://github.com/jpexposito/code-learn/blob/main/primero/bae/unidad-5/sqlite/01_crear_borrar_tabla.md).

### Paso 2: Insertar 20 entradas

Dado el siguiente conjunto de información:

| id_propietario | nombre      | apellido    | dni       | marca      | modelo     | ano  |
|----------------|-------------|-------------|-----------|------------|------------|------|
| 1              | Juan        | Perez       | 12345678A | Ford       | Fiesta     | 2019 |
| 2              | Maria       | Lopez       | 87654321B | Toyota     | Corolla    | 2018 |
| 3              | Carlos      | Ruiz        | 11111111C | Nissan     | Sentra     | 2020 |
| 4              | Laura       | Gomez       | 22222222D | Chevrolet  | Spark      | 2017 |
| 5              | Pedro       | Martinez    | 33333333E | Honda      | Civic      | 2016 |
| 6              | Ana         | Fernandez   | 44444444F | Ford       | Mustang    | 2021 |
| 7              | Diego       | Sanchez     | 55555555G | Toyota     | RAV4       | 2019 |
| 8              | Sofia       | Torres      | 66666666H | Volkswagen | Golf       | 2020 |
| 9              | Javier      | Leon        | 77777777I | Honda      | CR-V       | 2018 |
| 10             | Lucia       | Castillo    | 88888888J | Nissan     | Altima     | 2017 |
| 11             | Luis        | Gonzalez    | 99999999K | Chevrolet  | Malibu     | 2019 |
| 12             | Marta       | Diaz        | 10101010L | Toyota     | Camry      | 2020 |
| 13             | Victor      | Vargas      | 11111112M | Honda      | Accord     | 2018 |
| 14             | Elena       | Castro      | 12121212N | Ford       | Explorer   | 2021 |
| 15             | Roberto     | Blanco      | 13131313O | Nissan     | Rogue      | 2017 |
| 16             | Natalia     | Paredes     | 14141414P | Volkswagen | Jetta      | 2019 |
| 17             | Fernando    | Herrera     | 15151515Q | Chevrolet  | Equinox    | 2018 |
| 18             | Clara       | Soto        | 16161616R | Toyota     | Highlander | 2020 |
| 19             | Sergio      | Mendoza     | 17171717S | Honda      | Odyssey    | 2016 |
| 20             | Patricia    | Navarro     | 18181818T | Nissan     | Murano     | 2019 |

Realiza la inserción en la tablas de modo que la información quede almacenada.

___Guarda algunas de las entradas para el informe___.

>__Nota__: Ayudate de los [apuntes](https://github.com/jpexposito/code-learn/blob/main/primero/bae/unidad-5/sqlite/02_insert_select.md).

<details>
<summary style=" color: red;" > RESULTADO</summary>

**sqlite> insert into Propietarios ( nombre, apellido, dni)
   ...> values ('Juan' , 'Perez', '12345678A'),
   ...> ('Maria','Lopez','87654321B'),
   ...> ('Carlos','Ruiz','11111111C');**


**sqlite> insert into Vehiculos(marca,modelo,anio)
   ...> values
   ...> ('Ford','Fiesta',2019),
   ...> ('Toyota','Corolla',2018),
   ...> ('Nissan','Sentra',2020);
sqlite> select * from Vehiculos;**

| id_vehiculo | marca  | modelo  | anio | id_propietario |
|-------------|--------|---------|------|----------------|
| 1           | Ford   | Fiesta  | 2019 |                |
| 2           | Toyota | Corolla | 2018 |                |
| 3           | Nissan | Sentra  | 2020 |                |

sqlite> 
## aqui me di cuenta que m efalto id_propietario.

**sqlite> UPDATE Vehiculos SET id_propietario = 1 WHERE id_vehiculo = 1;
UPDATE Vehiculos SET id_propietario = 2 WHERE id_vehiculo = 2;
UPDATE Vehiculos SET id_propietario = 3 WHERE id_vehiculo = 3;**

sqlite> select * from Vehiculos;

| id_vehiculo | marca  | modelo  | anio | id_propietario |
|-------------|--------|---------|------|----------------|
| 1           | Ford   | Fiesta  | 2019 | 1              |
| 2           | Toyota | Corolla | 2018 | 2              |
| 3           | Nissan | Sentra  | 2020 | 3              |
</details>

### Paso 3: Realizar las siguientes 10 consultas de datos

- Seleccionar todos los propietarios
<details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select * from Propietarios;

| id |  nombre  | apellido  |    dni    |
|----|----------|-----------|-----------|
| 1  | Juan     | Perez     | 12345678A |
| 2  | Maria    | Lopez     | 87654321B |
| 3  | Carlos   | Ruiz      | 11111111C |
| 4  | Laura    | Gomez     | 22222222D |
| 5  | Pedro    | Martinez  | 33333333E |
| 6  | Ana      | Fernandez | 44444444F |
| 7  | Diego    | Sanchez   | 55555555G |
| 8  | Sofia    | Torres    | 66666666H |
| 9  | Javier   | Leon      | 77777777I |
| 10 | Lucia    | Castillo  | 88888888J |
| 11 | Luis     | Gonzalez  | 99999999K |
| 12 | Marta    | Diaz      | 10101010L |
| 13 | Victor   | Vargas    | 11111112M |
| 14 | Elena    | Castro    | 12121212N |
| 15 | Roberto  | Blanco    | 13131313O |
| 16 | Natalia  | Paredes   | 14141414P |
| 17 | Fernando | Herrera   | 15151515Q |
| 18 | Clara    | Soto      | 16161616R |
| 19 | Sergio   | Mendoza   | 17171717S |
| 20 | Patricia | Navarro   | 18181818T |

</details>
- Listar todos los vehículos.
  <details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select * from Vehiculos;

| id_vehiculo |   marca    |   modelo   | anio | id_propietario |
|-------------|------------|------------|------|----------------|
| 1           | Ford       | Fiesta     | 2019 | 1              |
| 2           | Toyota     | Corolla    | 2018 | 2              |
| 3           | Nissan     | Sentra     | 2020 | 3              |
| 4           | Chevrolet  | Spark      | 2017 | 4              |
| 5           | Honda      | Civic      | 2016 | 5              |
| 6           | Ford       | Mustang    | 2021 | 6              |
| 7           | Toyota     | RAV4       | 2019 | 7              |
| 8           | Volkswagen | Golf       | 2020 | 8              |
| 9           | Honda      | CR-V       | 2018 | 9              |
| 10          | Nissan     | Altima     | 2017 | 10             |
| 11          | Chevrolet  | Malibu     | 2019 | 11             |
| 12          | Toyota     | Camry      | 2020 | 12             |
| 13          | Honda      | Accord     | 2018 | 13             |
| 14          | Ford       | Explorer   | 2021 | 14             |
| 15          | Nissan     | Rogue      | 2017 | 15             |
| 16          | Volkswagen | Jetta      | 2019 | 16             |
| 17          | Chevrolet  | Equinox    | 2018 | 17             |
| 18          | Toyota     | Highlander | 2020 | 18             |
| 19          | Honda      | Odyssey    | 2016 | 19             |
| 20          | Nissan     | Murano     | 2019 | 20             |

</details>
- Seleccionar solo los nombres y apellidos de los propietarios.
<details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select nombre, apellido from Propietarios;

|  nombre  | apellido  |
|----------|-----------|
| Juan     | Perez     |
| Maria    | Lopez     |
| Carlos   | Ruiz      |
| Laura    | Gomez     |
| Pedro    | Martinez  |
| Ana      | Fernandez |
| Diego    | Sanchez   |
| Sofia    | Torres    |
| Javier   | Leon      |
| Lucia    | Castillo  |
| Luis     | Gonzalez  |
| Marta    | Diaz      |
| Victor   | Vargas    |
| Elena    | Castro    |
| Roberto  | Blanco    |
| Natalia  | Paredes   |
| Fernando | Herrera   |
| Clara    | Soto      |
| Sergio   | Mendoza   |
| Patricia | Navarro   |

sqlite> 
</details>
- Listar todas las marcas y modelos de los vehículos.
<details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select marca, modelo from Vehiculos;

|   marca    |   modelo   |
|------------|------------|
| Ford       | Fiesta     |
| Toyota     | Corolla    |
| Nissan     | Sentra     |
| Chevrolet  | Spark      |
| Honda      | Civic      |
| Ford       | Mustang    |
| Toyota     | RAV4       |
| Volkswagen | Golf       |
| Honda      | CR-V       |
| Nissan     | Altima     |
| Chevrolet  | Malibu     |
| Toyota     | Camry      |
| Honda      | Accord     |
| Ford       | Explorer   |
| Nissan     | Rogue      |
| Volkswagen | Jetta      |
| Chevrolet  | Equinox    |
| Toyota     | Highlander |
| Honda      | Odyssey    |
| Nissan     | Murano     |

sqlite> 
</details>
- Seleccionar solo los propietarios con apellido "Perez".
<details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select * from Propietarios
   ...> where apellido = 'Perez';

| id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 1  | Juan   | Perez    | 12345678A |
</details>
- Listar todos los vehículos con año 2019.
<details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select * from Vehiculos
   ...> where anio = 2019;


| id_vehiculo |   marca    | modelo | anio | id_propietario |
|-------------|------------|--------|------|----------------|
| 1           | Ford       | Fiesta | 2019 | 1              |
| 7           | Toyota     | RAV4   | 2019 | 7              |
| 11          | Chevrolet  | Malibu | 2019 | 11             |
| 16          | Volkswagen | Jetta  | 2019 | 16             |
| 20          | Nissan     | Murano | 2019 | 20             |

</details>
- Seleccionar propietarios que tienen vehículos de la marca "Toyota".
<details > 
<summary style="color: red;"> RESULTADO </summary>
**sqlite> select * from Propietarios P 
   ...> inner join Vehiculos V on V.id_vehiculo = P.id
   ...> where V.marca = 'Toyota';**

| id | nombre | apellido |    dni    | id_vehiculo | marca  |   modelo   | anio | id_propietario |
|----|--------|----------|-----------|-------------|--------|------------|------|----------------|
| 2  | Maria  | Lopez    | 87654321B | 2           | Toyota | Corolla    | 2018 | 2              |
| 7  | Diego  | Sanchez  | 55555555G | 7           | Toyota | RAV4       | 2019 | 7              |
| 12 | Marta  | Diaz     | 10101010L | 12          | Toyota | Camry      | 2020 | 12             |
| 18 | Clara  | Soto     | 16161616R | 18          | Toyota | Highlander | 2020 | 18             |

</details>

- Listar vehículos con marca "Ford" y modelo "Fiesta".
  <details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select * from Vehiculos 
   ...> where marca = 'Ford' and modelo = 'Fiesta';

| id_vehiculo | marca | modelo | anio | id_propietario |
|-------------|-------|--------|------|----------------|
| 1           | Ford  | Fiesta | 2019 | 1              |


</details>
- Seleccionar propietarios con DNI "12345678A".
<details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select * From Propietarios
   ...> where dni = '12345678A';

| id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 1  | Juan   | Perez    | 12345678A |
</details>
- Listar vehículos que pertenecen al propietario con ID 5.
  <details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select *  from Vehiculos
inner join Propietarios P ON Vehiculos.id_propietario = P.id
where P.id = 5;

| id_vehiculo | marca | modelo | anio | id_propietario | id | nombre | apellido |    dni    |
|-------------|-------|--------|------|----------------|----|--------|----------|-----------|
| 5           | Honda | Civic  | 2016 | 5              | 5  | Pedro  | Martinez | 33333333E |

</details>

### Paso 4: Realiza los siguientes updates

- Actualizar el nombre de un propietario con DNI "12345678A".
<details > 
<summary style="color: red;"> RESULTADO </summary>
**sqlite> select * from Propietarios
   ...> where dni='12345678A';**

| id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 1  | Juan   | Perez    | 12345678A |

**sqlite> update Propietarios set nombre='JOHN ACTUALIZADO'
   ...> where dni='12345678A';
sqlite> select * from Propietarios
   ...> where dni='12345678A';**

| id |      nombre      | apellido |    dni    |
|----|------------------|----------|-----------|
| 1  | JOHN ACTUALIZADO | Perez    | 12345678A |

</details>
- Modificar el año de un vehículo con ID 3 a 2022.
  <details > 
<summary style="color: red;"> RESULTADO </summary>
**sqlite> select * from Vehiculos
   ...> where id_vehiculo=5;**

| id_vehiculo | marca | modelo | anio | id_propietario |
|-------------|-------|--------|------|----------------|
| 5           | Honda | Civic  | 2016 | 5              |

**sqlite> update Vehiculos set anio = 2022
   ...> where id_vehiculo = 5;
sqlite> select * from Vehiculos
   ...> where id_vehiculo=5;**

| id_vehiculo | marca | modelo | anio | id_propietario |
|-------------|-------|--------|------|----------------|
| 5           | Honda | Civic  | 2022 | 5              |

</details>
- Cambiar el modelo de todos los vehículos Nissan a "Micra".
<details > 
<summary style="color: red;"> RESULTADO </summary>
**sqlite> select * from Vehiculos
   ...> where marca='Nissan';**

| id_vehiculo | marca  | modelo | anio | id_propietario |
|-------------|--------|--------|------|----------------|
| 3           | Nissan | Sentra | 2020 | 3              |
| 10          | Nissan | Altima | 2017 | 10             |
| 15          | Nissan | Rogue  | 2017 | 15             |
| 20          | Nissan | Murano | 2019 | 20             |

**sqlite> update Vehiculos set modelo='Micra'
   ...> where marca='Nissan';
sqlite> select * from Vehiculos
   ...> where marca='Nissan';**

| id_vehiculo | marca  | modelo | anio | id_propietario |
|-------------|--------|--------|------|----------------|
| 3           | Nissan | Micra  | 2020 | 3              |
| 10          | Nissan | Micra  | 2017 | 10             |
| 15          | Nissan | Micra  | 2017 | 15             |
| 20          | Nissan | Micra  | 2019 | 20             |

</details>
- Actualizar el apellido de un propietario con ID 7 a "Gomez".
  <details > 
<summary style="color: red;"> RESULTADO </summary>
**sqlite> select * from Propietarios
   ...> where id=7;**

| id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 7  | Diego  | Sanchez  | 55555555G |

**sqlite> update Propietarios set apellido='Gomez'
   ...> where id=7;
sqlite> select * from Propietarios
   ...> where id=7;**

| id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 7  | Diego  | Gomez    | 55555555G |

</details>
- Modificar la marca de un vehículo con modelo "Fiesta" a "Renault".
<details > 
<summary style="color: red;"> RESULTADO </summary>
sqlite> select * from Vehiculos
   ...> where modelo='Fiesta';

| id_vehiculo | marca | modelo | anio | id_propietario |
|-------------|-------|--------|------|----------------|
| 1           | Ford  | Fiesta | 2019 | 1              |

**sqlite> update Vehiculos set marca='Renault'
   ...> where modelo='Fiesta';
sqlite> select * from Vehiculos
   ...> where modelo='Fiesta';**

| id_vehiculo |  marca  | modelo | anio | id_propietario |
|-------------|---------|--------|------|----------------|
| 1           | Renault | Fiesta | 2019 | 1              |



</details>

</div>

