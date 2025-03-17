<div align="justify">

## Code, Learn & Practice(Base de datos (Trabajo con funciones en BBDD")

<div align="center">
<img src="https://i0.wp.com/hunna.org/wp-content/uploads/2014/06/huellas.jpg?resize=324%2C215" width="500px"/>
</div>

## Objetivo

_Practicar la creación y manipulación de una base de datos SQLite3 desde la línea de comandos_.

## Descripción

## Pasos

### Paso 1: Creación de la BBDD

Crea con el siguente contenido el fichero __empleados-dump.sql__.

```sql
CREATE TABLE empleados (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT,
    salario REAL,
    departamento TEXT
);

INSERT INTO empleados (nombre, salario, departamento) VALUES ('Juan', 50000, 'Ventas');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('María', 60000, 'TI');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Carlos', 55000, 'Ventas');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Ana', 48000, 'Recursos Humanos');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Pedro', 70000, 'TI');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Laura', 52000, 'Ventas');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Javier', 48000, 'Recursos Humanos');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Carmen', 65000, 'TI');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Miguel', 51000, 'Ventas');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Elena', 55000, 'Recursos Humanos');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Diego', 72000, 'TI');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Sofía', 49000, 'Ventas');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Andrés', 60000, 'Recursos Humanos');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Isabel', 53000, 'TI');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Raúl', 68000, 'Ventas');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Patricia', 47000, 'Recursos Humanos');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Alejandro', 71000, 'TI');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Natalia', 54000, 'Ventas');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Roberto', 49000, 'Recursos Humanos');
INSERT INTO empleados (nombre, salario, departamento) VALUES ('Beatriz', 63000, 'TI');
```
<details>
<summary style="color: red"> Resultado </summary>
<div align="center">
    <img src="https://raw.githubusercontent.com/johnfredyrg1226/base_datos2/main/tarea/Tema3_Realizacion_consultas_SQLite3/imagenes/Captura%20desde%202025-03-16%2022-15-18.png" width="500px"/>
</div>

</details>


  
### Paso 2 Lectura del fichero sql

Entra en sqlite a través del siguiente comando:

```sql
sqlite3 tarea3.db 
```

Haciendo un __.read__ del fichero __sql__, de nombre __empleados-db.sql__, realiza la creación e inserción de información de la __BBDD__.
<details>
<summary style="color: red"> Resultado </summary>
<div align="center">
    <img src="https://raw.githubusercontent.com/johnfredyrg1226/base_datos2/main/tarea/Tema3_Realizacion_consultas_SQLite3/imagenes/Captura%20desde%202025-03-16%2022-12-30.png
    " width="500px"/>
</div>

```sql
jramg23@jramg23-GL62-7QF:~$ ls
base-de-datos.db  empleado-dum.sql  Música      snap       tarea3.db
Descargas         Escritorio        Plantillas  tarea1.db  Vídeos
Documentos        Imágenes          Público     tarea2.db
jramg23@jramg23-GL62-7QF:~$ sqlite3 tarea3.db
SQLite version 3.45.1 2024-01-30 16:01:20
Enter ".help" for usage hints.
sqlite> .read empleado-dum.sql
sqlite> .tables
empleados

```
</details>

### Paso 3: Realización de consultas

Realiza las siguientes consultas, y muestra el resultado obtenido:

- Funciones UPPER y LOWER:
  - Muestra el nombre de todos los empleados en mayúsculas.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select upper(nombre) as nombre_mayuscula from empleados;
```

| nombre_mayuscula |
|------------------|
| JUAN             |
| MARíA            |
| CARLOS           |
| ANA              |
| PEDRO            |
| LAURA            |
| JAVIER           |
| CARMEN           |
| MIGUEL           |
| ELENA            |
| DIEGO            |
| SOFíA            |
| ANDRéS           |
| ISABEL           |
| RAúL             |
| PATRICIA         |
| ALEJANDRO        |
| NATALIA          |
| ROBERTO          |
| BEATRIZ          |


</details>

<details>
<summary style= "color: red"> Resultado </summary>
```sql
s
```
</details>
- Funciones Numéricas:
  - Calcula el valor absoluto del salario de todos los empleados.
- <details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select abs(salario) as valor_absoluto from empleados;
```
| valor_absoluto |
|----------------|
| 50000.0        |
| 60000.0        |
| 55000.0        |
| 48000.0        |
| 70000.0        |
| 52000.0        |
| 48000.0        |
| 65000.0        |
| 51000.0        |
| 55000.0        |
| 72000.0        |
| 49000.0        |
| 60000.0        |
| 53000.0        |
| 68000.0        |
| 47000.0        |
| 71000.0        |
| 54000.0        |
| 49000.0        |
| 63000.0        |

</details>
- Funciones de Fecha y Hora:
  - Muestra la fecha actual.
  <details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select current_date;
```
| current_date |
|--------------|
| 2025-03-17   |

```sql
sqlite> select date('now');
```
| date('now') |
|-------------|
| 2025-03-17  |

```sql
**Esto para ver la fecha con partes de la tablaa.**
sqlite> select nombre,salario, current_date from empleados;
```

|  nombre   | salario | current_date |
|-----------|---------|--------------|
| Juan      | 50000.0 | 2025-03-17   |
| María     | 60000.0 | 2025-03-17   |
| Carlos    | 55000.0 | 2025-03-17   |
| Ana       | 48000.0 | 2025-03-17   |
| Pedro     | 70000.0 | 2025-03-17   |
| Laura     | 52000.0 | 2025-03-17   |
| Javier    | 48000.0 | 2025-03-17   |
| Carmen    | 65000.0 | 2025-03-17   |
| Miguel    | 51000.0 | 2025-03-17   |
| Elena     | 55000.0 | 2025-03-17   |
| Diego     | 72000.0 | 2025-03-17   |
| Sofía     | 49000.0 | 2025-03-17   |
| Andrés    | 60000.0 | 2025-03-17   |
| Isabel    | 53000.0 | 2025-03-17   |
| Raúl      | 68000.0 | 2025-03-17   |
| Patricia  | 47000.0 | 2025-03-17   |
| Alejandro | 71000.0 | 2025-03-17   |
| Natalia   | 54000.0 | 2025-03-17   |
| Roberto   | 49000.0 | 2025-03-17   |
| Beatriz   | 63000.0 | 2025-03-17   |


</details>
- Funciones de Agregación:
  - Calcula el promedio de salarios de todos los empleados.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select avg(salario) from empleados;
```
| avg(salario) |
|--------------|
| 57000.0      |

</details>
  - Convierte la cadena '123' a un valor entero.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select cast('123' as integer);
```
| cast('123' as integer) |
|------------------------|
| 123                    |

**sqlite> select '123' + 0;**

| '123' + 0 |
|-----------|
| 123       |
</details>
- Funciones de Manipulación de Cadenas:
  - Concatena el nombre y el departamento de cada empleado.
  <details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre || departamento from empleados;
```
|  nombre || departamento  |
|--------------------------|
| JuanVentas               |
| MaríaTI                  |
| CarlosVentas             |
| AnaRecursos Humanos      |
| PedroTI                  |
| LauraVentas              |
| JavierRecursos Humanos   |
| CarmenTI                 |
| MiguelVentas             |
| ElenaRecursos Humanos    |
| DiegoTI                  |
| SofíaVentas              |
| AndrésRecursos Humanos   |
| IsabelTI                 |
| RaúlVentas               |
| PatriciaRecursos Humanos |
| AlejandroTI              |
| NataliaVentas            |
| RobertoRecursos Humanos  |
| BeatrizTI                |

</details>
- Funciones de Manipulación de Cadenas (CONCAT_WS):
  - Concatena el nombre y el departamento de cada empleado con un guion como separador.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre || '-' || departamento as nombre_departamento from empleados;
```
|    nombre_departamento    |
|---------------------------|
| Juan-Ventas               |
| María-TI                  |
| Carlos-Ventas             |
| Ana-Recursos Humanos      |
| Pedro-TI                  |
| Laura-Ventas              |
| Javier-Recursos Humanos   |
| Carmen-TI                 |
| Miguel-Ventas             |
| Elena-Recursos Humanos    |
| Diego-TI                  |
| Sofía-Ventas              |
| Andrés-Recursos Humanos   |
| Isabel-TI                 |
| Raúl-Ventas               |
| Patricia-Recursos Humanos |
| Alejandro-TI              |
| Natalia-Ventas            |
| Roberto-Recursos Humanos  |
| Beatriz-TI                |
</details>
- Funciones de Control de Flujo (CASE):
  - Categoriza a los empleados según sus salarios.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre,salario, case
   ...> when salario <50000 then 'bajo'
   ...> when salario between 50000 and 70000 then 'medio'
   ...> when salario > 70000 then 'alto'
   ...> end as Salarios_por_categotia
   ...> from empleados;
```
|  nombre   | salario | Salarios_por_categotia |
|-----------|---------|------------------------|
| Juan      | 50000.0 | medio                  |
| María     | 60000.0 | medio                  |
| Carlos    | 55000.0 | medio                  |
| Ana       | 48000.0 | bajo                   |
| Pedro     | 70000.0 | medio                  |
| Laura     | 52000.0 | medio                  |
| Javier    | 48000.0 | bajo                   |
| Carmen    | 65000.0 | medio                  |
| Miguel    | 51000.0 | medio                  |
| Elena     | 55000.0 | medio                  |
| Diego     | 72000.0 | alto                   |
| Sofía     | 49000.0 | bajo                   |
| Andrés    | 60000.0 | medio                  |
| Isabel    | 53000.0 | medio                  |
| Raúl      | 68000.0 | medio                  |
| Patricia  | 47000.0 | bajo                   |
| Alejandro | 71000.0 | alto                   |
| Natalia   | 54000.0 | medio                  |
| Roberto   | 49000.0 | bajo                   |
| Beatriz   | 63000.0 | medio                  |


</details>
- Funciones de Agregación (SUM):
  - Calcula la suma total de salarios de todos los empleados.
<details>
<summary style= "color: red"> Resultado </summary>
```sql
sqlite> select sum(salario) as Media_Salario from empleados;
```
| Media_Salario |
|---------------|
| 1140000.0     |

</details>
- Funciones Numéricas (ROUND):
  - Redondea el salario de todos los empleados a dos decimales.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre, round(salario, 2) as Salario_redondeado
   ...> from empleados;
```

|  nombre   | Salario_redondeado |
|-----------|--------------------|
| Juan      | 50000.0            |
| María     | 60000.0            |
| Carlos    | 55000.0            |
| Ana       | 48000.0            |
| Pedro     | 70000.0            |
| Laura     | 52000.0            |
| Javier    | 48000.0            |
| Carmen    | 65000.0            |
| Miguel    | 51000.0            |
| Elena     | 55000.0            |
| Diego     | 72000.0            |
| Sofía     | 49000.0            |
| Andrés    | 60000.0            |
| Isabel    | 53000.0            |
| Raúl      | 68000.0            |
| Patricia  | 47000.0            |
| Alejandro | 71000.0            |
| Natalia   | 54000.0            |
| Roberto   | 49000.0            |
| Beatriz   | 63000.0            |

</details>
- Funciones de Manipulación de Cadenas (LENGTH):
  - Muestra la longitud de cada nombre de empleado.
<details>
<summary style= "color: red"> Resultado </summary>

```sql
sqlite> select nombre, length(nombre) as log_nombre
   ...> from empleados;
```

|  nombre   | log_nombre |
|-----------|------------|
| Juan      | 4          |
| María     | 5          |
| Carlos    | 6          |
| Ana       | 3          |
| Pedro     | 5          |
| Laura     | 5          |
| Javier    | 6          |
| Carmen    | 6          |
| Miguel    | 6          |
| Elena     | 5          |
| Diego     | 5          |
| Sofía     | 5          |
| Andrés    | 6          |
| Isabel    | 6          |
| Raúl      | 4          |
| Patricia  | 8          |
| Alejandro | 9          |
| Natalia   | 7          |
| Roberto   | 7          |
| Beatriz   | 7          |

</details>
- Funciones de Agregación (COUNT):
  - Cuenta el número total de empleados en cada departamento.

<details>
<summary style= "color: red"> Resultado </summary>
```sql
s
```
</details>- Funciones de Fecha y Hora (CURRENT_TIME):
  - Muestra la hora actual.
<details>
<summary style= "color: red"> Resultado </summary>
```sql
s
```
</details>
- Funciones de Conversión (CAST):
  - Convierte el salario a un valor de punto flotante.
<details>
<summary style= "color: red"> Resultado </summary>
```sql
s
```
</details>
- Funciones de Manipulación de Cadenas (SUBSTR):
  - Muestra los primeros tres caracteres de cada nombre de empleado.

- __Order By__ and __Like__.
  - Empleados en el departamento de 'Ventas' con salarios superiores a 52000.
  - Empleados cuyos nombres contienen la letra 'a' y tienen salarios ordenados de manera ascendente.
  - Empleados en el departamento 'Recursos Humanos' con salarios entre 45000 y 55000.
  - Empleados con salarios en orden descendente, limitando a los primeros 5 resultados.
  - Empleados cuyos nombres comienzan con 'M' o 'N' y tienen salarios superiores a 50000.
  - Empleados en el departamento 'TI' o 'Ventas' ordenados alfabéticamente por nombre.
  - Empleados con salarios únicos (eliminando duplicados) en orden ascendente.
  - Empleados cuyos nombres terminan con 'o' o 'a' y están en el departamento 'Ventas'.
  - Empleados con salarios fuera del rango de 55000 a 70000, ordenados por departamento.
  - Empleados en el departamento 'Recursos Humanos' con nombres que no contienen la letra 'e'.

### Generación Informe

Genera un informe con cada una de las consultas y los resuldos obtenidos tras su ejecución. El informe se debe de realizar en __markdown, y enviar el enlace__.

</div>