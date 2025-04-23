<div align="justify">

# Code, Learn & Practice("Simulacro consultas bbdd 2")



## Objetivo

Simulacro de examen se provee de los siguientes ficheros:

- [examen_multitabla.sql](files/simulacro_multitabla.sql). Fichero que contiene la especificación de la BBDD e inserts para la realización del examen.
- [XX_consultas_multitabla.sql](files/XX_consultas_multitabla_simulacro.sql). Conjunto de consultas a realizar por el alumno. Dentro se encuentra la rúbrica del examen.
Se debe de entregar el fichero XX_consultas_multitabla.sql con el nombre y apellidos correspondiente de cada alumno.

### Consultas Básicas (8 consultas - 1.6 puntos)

1. Listar todos los libros disponibles.
   > **Pista**: Select *
2. Mostrar socios de Madrid ordenados por apellido.
   > **Pista**: order.   
3. Libros publicados después de 1950
      > **Pista**: where
4. Bibliotecarios con más de 3 años de antigüedad
      > **Pista**: saber la fecha actual
5. Préstamos realizados en 2023
      > **Pista**: where like|Expresion regular
6. Socios sin segundo apellido.
      > **Pista**: Apellido2 = NULL
7. Libros del género "Realismo mágico"
      > **Pista**: Where
8. Préstamos no devueltos. 
   > **Pista**: fecha_devolucion = NULL

### Consultas Multitabla (WHERE) (8 consultas - 2.4 puntos)

1. Préstamos con nombres de socio y libro (sin JOIN)
      > **Pista**: where id claves tablas.
2. Libros prestados a socios de Barcelona (sin JOIN)
      > **Pista**: where id claves tablas.
3. Socios que han tomado prestado "Cien años de soledad" (sin JOIN)
      > **Pista**: where id claves tablas and edad
4. Bibliotecarios que han gestionado préstamos (sin JOIN)
      > **Pista**: where id claves tablas.
5. Préstamos con retraso.
      > **Pista**: where id claves tablas && fecha_devolucion > fecha_prestamo + 14 días.
6. Socios que nunca han tomado prestado un libro (sin LEFT JOIN)
      > **Pista**: where id claves tablas.
7. Libros más prestados (sin JOIN)
      > **Pista**: where id claves tablas and top
8. Autores cuyos libros han sido prestados (sin JOIN)
      > **Pista**: where id claves tablas.

### Consultas Multitabla (JOIN) (8 consultas - 2.4 puntos)

1. Préstamos con nombres de socio y libro.
   > **Pista**: JOIN.
2. Libros prestados a socios de Barcelona.
   > **Pista**: JOIN.
3. Socios que han tomado prestado "Cien años de soledad".
   > **Pista**: JOIN.
4. Bibliotecarios que han gestionado préstamos.
   > **Pista**: JOIN.
5. Préstamos con datos completos (socio, libro, bibliotecario)
6. Socios con sus préstamos activos.
   > **Pista**: JOIN.
7. Libros nunca prestados.
   > **Pista**: LEFT|RIGHT JOIN en función del orden de las tablas.
8. Autores con número de libros prestados.
   > **Pista**: JOIN + GROUP BY.

## Consultas Resumen (8 consultas - 2.4 puntos)

1. Número de socios por ciudad.
2. Promedio de antigüedad de bibliotecarios.
3. Cantidad de préstamos por mes en 2023.
4. Libros más populares (por veces prestados).
5. Socios más activos (por préstamos realizados).
6. Porcentaje de libros disponibles.
7. Días promedio de préstamo.
8. Número de préstamos por categoría de socio.

### Subconsultas (8 consultas - 1.2 puntos)

1. Socios que han prestado libros de Gabriel García Márquez.
  > **Pista**: WHERE + IN|EXIST.
1. Libros con préstamos superiores al promedio.
     > **Pista**: WHERE + > + AVG .
2. Socios con todos los préstamos devueltos a tiempo.
     > **Pista**: WHERE + IN|EXIST.
3. Bibliotecarios que no han gestionado préstamos.
     > **Pista**: WHERE + IN|EXIST O NOT IN|EXIST.
4. Socios que han prestado más libros que el promedio.
      > **Pista**: WHERE + > + AVG .
5. Libros disponibles que nunca han sido prestados.
   > **Pista**: WHERE + NOT IN|EXIST.
6. Socios con préstamos en todas las categorías de libros.
   > **Pista**: WHERE + IN|EXIST.
7. Bibliotecarios que han gestionado préstamos de todos los socios de Madrid.
   > **Pista**: WHERE + IN|EXIST.
</div>