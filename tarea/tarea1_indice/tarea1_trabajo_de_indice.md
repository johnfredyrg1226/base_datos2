## Tarea 1 de trabajo con índices

**Un instituto de enseñanza guarda los siguientes datos de sus alumnos:**

**número de inscripción, comienza desde 1 cada año,
año de inscripción,
nombre del alumno,
documento del alumno,
domicilio,
ciudad,
provincia,
clave primaria: número de inscripto y año de inscripción.
Se pide:**



#### 1.Elimine la tabla "alumno" si existe.
**Nota:Muestra el comando y la salida.**

```sql
sqlite> drop table if exists alumno;
sqlite> 
```

#### 2.Cree la tabla definiendo una clave primaria compuesta (año de inscripción y número de inscripción).
**Nota:Muestra el comando y la salida.**

```sql
drop table if exists alumno;

create table alumno(
    numero_de_incripcion integer,
    anio_incripcion integer,
    nombre text,
    documento text,
    domicilio text,
    ciudad text,
    provincia text,
    primary key (numero_de_incripcion, anio_incripcion));
sqlite> 

```

##### Define los siguientes indices:
**Un índice único por el campo "documento" y un índice común por ciudad y provincia.
Nota:Muestra el comando y la salida. Justifica el tipo de indice en un comentario.**

```sql
sqlite> create unique index idx_documento on alumno(documento);
sqlite> 

** El tipo de indice es unique ya que no deja que se dupliquen numeros en la columna y son unicos


create index idx_ciudad_provincia on alumno (ciudad, provincia);
sqlite>  la salida no me da nada esto indica que la operacion es correcta.

** El tipo de indice seria compuesto o multicolumna asi se filtran los datos utilizando 
varias columnas, se suelen utilizar con el where. ejemplo:select * from alumno where ciudad = 'valor1' and provincia = 'valor2';

```

#### Vea los índices de la tabla.
**Nota:Muestra el comando y la salida "show index".**

```sql
El show index no funciona con sqlite debo de utilizar sqlite> pragma index_list('alumno');

pragma index_list('alumno');
+-----+---------------------------+--------+--------+---------+
| seq |           name            | unique | origin | partial |
+-----+---------------------------+--------+--------+---------+
| 0   | idx_ciudad_provincia      | 0      | c      | 0       |
| 1   | idx_documento             | 1      | c      | 0       |
| 2   | sqlite_autoindex_alumno_1 | 1      | pk     | 0       |
+-----+---------------------------+--------+--------+---------+

```

#### Intente ingresar un alumno con clave primaria repetida.
**Nota:Muestra el comando y la salida.**

```sql
Para hacer este apartada dobo de insertar un alumno.

insert into alumno(
    numero_de_incripcion,
    anio_incripcion,
    nombre,
    documento,
    domicilio,
    ciudad,
    provincia
) values(
    1,2025,'john','12345678X','calle el mar 11','madrid','madrid'
);

se hace un select...

sqlite> select * from alumno;
+----------------------+-----------------+--------+-----------+-----------------+--------+-----------+
| numero_de_incripcion | anio_incripcion | nombre | documento |    domicilio    | ciudad | provincia |
+----------------------+-----------------+--------+-----------+-----------------+--------+-----------+
| 1                    | 2025            | john   | 12345678X | calle el mar 11 | madrid | madrid    |
+----------------------+-----------------+--------+-----------+-----------------+--------+-----------+
sqlite> 

ahora se inserta otro alumno conla clave primaria igual.

insert into alumno(
    numero_de_incripcion,
    anio_incripcion,
    nombre,
    documento,
    domicilio,
    ciudad,
    provincia
) values(
    1,2025,'David','87654321X','calle madrid 11','madrid','madrid'
);

Runtime error: UNIQUE constraint failed: alumno.numero_de_incripcion, alumno.anio_incripcion (19)
sqlite> 
SIGNIFICA ERROR EN TIEMPO DE EJECUCION. FALLÓ DE RESTRICCIÓN DE UNICIDAD. O REGLA QUE NO PERMITE DUPLICADOS.

```


#### Intente ingresar un alumno con documento repetido.
**Nota:Muestra el comando y la salida.***

```SQL
insert into alumno(
    numero_de_incripcion,
    anio_incripcion,
    nombre,
    documento,
    domicilio,
    ciudad,
    provincia
) values(
    2,2025,'David','12345678X','calle madrid 11','madrid','madrid'
);

Runtime error: UNIQUE constraint failed: alumno.documento (19)


```

### Ingrese varios alumnos de la misma ciudad y provincia.
**Nota:Muestra el comando y la salida.**

```sql
insert into alumno(
    numero_de_incripcion,
    anio_incripcion,
    nombre,
    documento,
    domicilio,
    ciudad,
    provincia
) values
    (6,2025,'Fran','12345678T','calle mendez 3','madrid','madrid'),
    (7,2020,'Esa','12365487H','calle junior 1','madrid','madrid'),
    (8,2020,'Audry','87652314D','calle candelaria','madrid','madrid');

no sale nada ya que es correcta.
sqlite> select * from alumno;
+----------------------+-----------------+--------+-----------+------------------+--------+-----------+
| numero_de_incripcion | anio_incripcion | nombre | documento |    domicilio     | ciudad | provincia |
+----------------------+-----------------+--------+-----------+------------------+--------+-----------+
| 1                    | 2025            | john   | 12345678X | calle el mar 11  | madrid | madrid    |
| 6                    | 2025            | Fran   | 12345678T | calle mendez 3   | madrid | madrid    |
| 7                    | 2020            | Esa    | 12365487H | calle junior 1   | madrid | madrid    |
| 8                    | 2020            | Audry  | 87652314D | calle candelaria | madrid | madrid    |
+----------------------+-----------------+--------+-----------+------------------+--------+-----------+

```

Elimina los indices creados, y muestra que ya no se encuentran.
Nota:Muestra el comando y la salida.

```sql
Muestro los indices. 
**pragma index_list('alumno');**
+-----+---------------------------+--------+--------+---------+
| seq |           name            | unique | origin | partial |
+-----+---------------------------+--------+--------+---------+
| 0   | idx_ciudad_provincia      | 0      | c      | 0       |
| 1   | idx_documento             | 1      | c      | 0       |
| 2   | sqlite_autoindex_alumno_1 | 1      | pk     | 0       |
+-----+---------------------------+--------+--------+---------+

y los elimino 

drop index idx_documento;
drop index idx_ciudad_provincia;

sqlite> pragma index_list('alumno'); 
+-----+---------------------------+--------+--------+---------+
| seq |           name            | unique | origin | partial |
+-----+---------------------------+--------+--------+---------+
| 0   | sqlite_autoindex_alumno_1 | 1      | pk     | 0       |
+-----+---------------------------+--------+--------+---------+


```