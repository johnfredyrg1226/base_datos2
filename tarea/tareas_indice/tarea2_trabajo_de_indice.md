# Tarea 2 de trabajo con índices

**Una empresa guarda los siguientes datos de sus clientes, con los siguientes campos:**

**documento char (8) not null,
nombre varchar(30) not null,
domicilio varchar(30),
ciudad varchar(20),
provincia varchar (20),
telefono varchar(11)
Se pide:**

#### Elimine la tabla "cliente" si existe.
**Nota:Muestra el comando y la salida.**

```sql
drop table if exists cliente;
```

#### Cree la tabla si clave primaria y incluye a posteriori esta.
**Nota:Muestra el comando y la salida.**

```sql
drop table if exists cliente;

create table cliente(
    documento varchar(30) not null,
    nombre varchar(30) not null,
    domicilio varchar(30),
    ciudad varchar(20),
    provincia varchar(20),
    telefono varchar(11)
);
comando de salida sqlite>

<span style="color:red"> **SQLite no diferencia entre CHAR, VARCHAR o TEXT internamente, pero es válido para mantener compatibilidad con otras bases de datos.**</span>

create table cliente(
    documento varchar(30) not null primary key,
    nombre varchar(30) not null,
    domicilio varchar(30),
    ciudad varchar(20),
    provincia varchar(20),
    telefono varchar(11)
);

```

#### Define los siguientes indices:
**Un índice único por el campo "documento" y un índice común por ciudad y provincia. >Nota:Muestra el comando y la salida. Justifica el tipo de indice en un comentario.
Vea los índices de la tabla.
Nota:Muestra el comando y la salida "show index".**

```sql
create unique index idx_documento on cliente('documento');
sqlite> 

pragma index_list('cliente');
+-----+----------------------------+--------+--------+---------+
| seq |            name            | unique | origin | partial |
+-----+----------------------------+--------+--------+---------+
| 0   | idx_documento              | 1      | c      | 0       |
| 1   | sqlite_autoindex_cliente_1 | 1      | pk     | 0       |
+-----+----------------------------+--------+--------+---------+
```

#### Agregue un índice único por el campo "telefono".
**Nota:Muestra el comando y la salida.**

```sql
create unique index idx_telefono on  cliente('telefono');

sqlite> pragma index_list('cliente');
+-----+----------------------------+--------+--------+---------+
| seq |            name            | unique | origin | partial |
+-----+----------------------------+--------+--------+---------+
| 0   | idx_telefono               | 1      | c      | 0       |
| 1   | idx_documento              | 1      | c      | 0       |
| 2   | sqlite_autoindex_cliente_1 | 1      | pk     | 0       |
+-----+----------------------------+--------+--------+---------+
```

### Elimina los índices.
**Nota:Muestra el comando y la salida.**

```sql
drop index idx_telefono;
drop index idx_documento;

sqlite> pragma index_list('cliente');
+-----+----------------------------+--------+--------+---------+
| seq |            name            | unique | origin | partial |
+-----+----------------------------+--------+--------+---------+
| 0   | sqlite_autoindex_cliente_1 | 1      | pk     | 0       |
+-----+----------------------------+--------+--------+---------+

```