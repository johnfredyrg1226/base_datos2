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
mysql> drop table if exists cliente;
Query OK, 0 rows affected, 1 warning (0.00 sec)

```

#### Cree la tabla si clave primaria y incluye a posteriori esta.
**Nota:Muestra el comando y la salida.**

```sql
mysql> drop table if exists cliente;
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> 
mysql> create table cliente(
    ->     documento varchar(30) not null,
    ->     nombre varchar(30) not null,
    ->     domicilio varchar(30),
    ->     ciudad varchar(20),
    ->     provincia varchar(20),
    ->     telefono varchar(11)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> alter table cliente add primary key (documento);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0


```

#### Define los siguientes indices:
**Un índice único por el campo "documento" y un índice común por ciudad y provincia. >Nota:Muestra el comando y la salida. Justifica el tipo de indice en un comentario.
Vea los índices de la tabla.
Nota:Muestra el comando y la salida "show index".**

```sql
create unique index idx_documento on cliente (documento);

mysql> create unique index idx_ciudad_provincia on cliente(ciudad, provincia);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0


mysql> show index from cliente;
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table   | Non_unique | Key_name             | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| cliente |          0 | PRIMARY              |            1 | documento   | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
| cliente |          0 | idx_ciudad_provincia |            1 | ciudad      | A         |           0 |     NULL | NULL   | YES  | BTREE      |         |               |
| cliente |          0 | idx_ciudad_provincia |            2 | provincia   | A         |           0 |     NULL | NULL   | YES  | BTREE      |         |               |
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
3 rows in set (0.00 sec)

```

#### Agregue un índice único por el campo "telefono".
**Nota:Muestra el comando y la salida.**

```sql
mysql> create unique index idx_telefono on  cliente(telefono);
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0


mysql> show index from cliente;
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table   | Non_unique | Key_name             | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| cliente |          0 | PRIMARY              |            1 | documento   | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
| cliente |          0 | idx_ciudad_provincia |            1 | ciudad      | A         |           0 |     NULL | NULL   | YES  | BTREE      |         |               |
| cliente |          0 | idx_ciudad_provincia |            2 | provincia   | A         |           0 |     NULL | NULL   | YES  | BTREE      |         |               |
| cliente |          0 | idx_telefono         |            1 | telefono    | A         |           0 |     NULL | NULL   | YES  | BTREE      |         |               |
+---------+------------+----------------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+

```

### Elimina los índices.
**Nota:Muestra el comando y la salida.**

```sql
mysql> drop index idx_telefono on cliente;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> drop index idx_ciudad_provincia on cliente;
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0


mysql> show index from cliente;
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table   | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| cliente |          0 | PRIMARY  |            1 | documento   | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+


```