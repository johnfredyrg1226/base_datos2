<div >


# Code, Learn & Practice Base de datos (Ejercicios de Normalización de Bases de Datos (1FN y 2FN)")


## **Ejercicio 1: Lista de Productos**

### **Tabla Inicial: Productos**

| ID_Producto | Nombre_Producto | Proveedores      | Categoría   | Precio |
|------------|----------------|-----------------|------------|--------|
| 1          | Laptop         | Dell, HP        | Tecnología | 1000   |
| 2          | Mouse          | Logitech        | Accesorios | 25     |

### **Tareas:**

1. Aplicar **1FN**, eliminando los valores multivaluados en "Proveedores".
2. Aplicar **2FN**, asegurando que cada campo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación


 <details>
<summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# Tabla: Productos  
| ID_Producto | Nombre_Producto | Categoría   | Precio |
|------------|----------------|------------|--------|
| **1**      | **Laptop**      | **Tecnología** | **1000**   |
| 2          | Mouse          | Accesorios | 25     |

# Tabla: Producto_Proveedores  
| ID_Producto | Proveedor  |
|------------|-----------|
| **1**      | **Dell**   |
| 1     | HP     |
| **2**          | **Logitech**  |
</details>



---

## **Ejercicio 2: Pedidos de Clientes**

### **Tabla Inicial: Pedidos**

| ID_Pedido | Cliente   | Dirección       | Producto     | Cantidad | Precio |
|----------|----------|---------------|-------------|----------|--------|
| 101      | Juan Pérez | Calle 123     | Laptop      | 1        | 1000   |
| 102      | Ana López | Av. Central   | Teclado     | 2        | 50     |

### **Tareas:**

1. Aplicar **1FN**, separando valores repetidos y creando nuevas tablas si es necesario.
2. Aplicar **2FN**, asegurando que las dependencias parciales sean eliminadas.

> Verifica generando el modelo Entidad/Relación

---
<details>
 <summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# **tabla: Cliente**
| ID_Cliente | Cliente    | Dirección     |
|------------|------------|---------------|
| 101        | Juan Pérez | Calle 123     |
| 102        | Ana López  | Av. Central   |



### **2. Tabla: `Pedidos`**  
(Contiene la información sobre los pedidos, pero sin incluir los productos directamente)

| ID_Pedido | ID_Cliente |  
|-----------|------------|
| 101       | 101        |
| 102       | 102        |



### **3. Tabla: Pedido_Productos**  
(Contiene los productos de cada pedido, separando las multivaluaciones y las cantidades de productos)

| ID_Pedido | ID_Producto | Cantidad | Precio_Unitario |  
|-----------|-------------|----------|-----------------|  
| 101       | 1           | 1        | 1000            |  
| 102       | 2           | 2        | 50              |  


### **4. Tabla: Productos**  
(Contiene solo la información de los productos, sin repetirse en los pedidos)

| ID_Producto | Producto | Precio  |
|-------------|----------|---------|
| 1           | Laptop   | 1000    |
| 2           | Teclado  | 25      |

Este modelo ya está en una forma **bien normalizada**.

</details>
---



## **Ejercicio 3: Registro de Empleados**

### **Tabla Inicial: Empleados**

| ID_Empleado | Nombre     | Teléfonos         | Departamento |
|------------|------------|------------------|--------------|
| 1          | Carlos R.  | 12345, 67890     | Ventas       |
| 2          | Laura M.   | 54321            | Finanzas     |

### **Tareas:**

1. Aplicar **1FN**, eliminando los valores multivaluados en "Teléfonos".
2. Aplicar **2FN**, asegurando que cada atributo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación
<details>
 <summary style="cursor: pointer; color: red;">RESULTADO:</summary>


# Tabla Empleado
| Id_empleado | Nombre | Departamento |
|-------------|--------|--------------|
|   1   | Carlos R  |   ventas      |
|   2   | Laura M   |  finanzas     |

# Tabla Telefonos
| Id_empleado |  Telefono |
|-------------|--------------|
|   1   |    12345 |
|   1   |   67890   |
|   2   |  54321   |
</details>


---

## **Ejercicio 4: Reservas de Hotel**

### **Tabla Inicial: Reservas**

| ID_Reserva | Cliente    | Habitación | Fechas              | Precio |
|------------|-----------|------------|---------------------|--------|
| 5001      | Pedro G.  | 101        | 01/02, 02/02, 03/02 | 300    |
| 5002      | María T.  | 202        | 10/03, 11/03       | 200    |

### **Tareas:**

1. Aplicar **1FN**, eliminando los valores multivaluados en "Fechas".
2. Aplicar **2FN**, asegurando que las dependencias parciales sean eliminadas.

> Verifica generando el modelo Entidad/Relación
<details>
 <summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# Tabla Empleado
| Id_empleado | Nombre | Departamento |
|-------------|--------|--------------|
|   1   | Carlos R  |   ventas      |
|   2   | Laura M   |  finanzas     |

# Tabla Telefonos
| Id_empleado |  Telefono |
|-------------|--------------|
|   1   |    12345 |
|   1   |   67890   |
|   2   |  54321   |
</details>
---

## **Ejercicio 5: Inscripciones a Cursos**

### **Tabla Inicial: Inscripciones**

| ID_Inscripción | Estudiante | Curso        | Profesor    | Horarios |
|---------------|------------|--------------|------------|----------|
| 3001         | Luis R.    | Matemáticas  | Prof. Pérez | Lunes 10AM, Miércoles 2PM |
| 3002         | Ana S.     | Física       | Prof. Gómez | Martes 3PM |

### **Tareas:**

1. Aplicar **1FN**, eliminando valores multivaluados en "Horarios".
2. Aplicar **2FN**, asegurando que cada campo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación
<details>
 <summary style="cursor: pointer; color: red;">RESULTADO:</summary>
 <details>
<summary style="cursor: pointer; color: red;">RESULTADO:</summary>

</details>
|   1           |   prof. Pérez |
|   2           |   prof. Gómez |

# tabla: **Curso**
|   Id_curso    |   Curso   | 
|---------------|-----------|
|   20          |   Matematicas |  
|   21          | Física    |

# tabla: **Horario**
|   ID_curso    | Horario   |
|--------------|--------------------|
|   20          | Lunes 10 AM   |
|   20          | Miercoles 2PM |
|   21          | Martes 3PM    |

# tabla: **Alumno**
| ID_ Alumno   |   ID_Incripción    |   Nombre  |
|--------------|--------------------|-----------|
|   100         |   3001            |   Luis R. |
|   101          |  3002            |   Ana S.  |

</details>
---

## **Ejercicio 6: Ventas de Tienda**

### **Tabla Inicial: Ventas**

| ID_Venta | Cliente    | Productos Comprados | Total |
|----------|------------|---------------------|-------|
| 8001     | Juan P.   | Celular, Funda      | 500   |
| 8002     | Andrea M. | Laptop              | 1000  |

### **Tareas:**

1. Aplicar **1FN**, separando valores multivaluados en "Productos Comprados".
2. Aplicar **2FN**, asegurando que cada atributo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación

<details>
<summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# tabla: ** cliente **
| id_Cliente    |   Cliente |
|---------------|-----------|
|   01          |   Juan P  |
|   02          |   Andre M |

# tabla: **Producto **
| id_Producto|  Producto    |
|   1001    |   Celular      |
|   1002    |   Funda       |
|   1003    |   Laptop      |

# tabla: **Venta ** 
| ID_Venta  |   total   |
|-----------|-----------|
|   8001    |   500     |
|   8002    |   1000     |

# tabla: **Venta_Producto**  (Tabla intermedia)
| ID_Venta | id_Producto |
|----------|-------------|
| 8001     | 1001        |
| 8001     | 1002        |
| 8002     | 1003        |


</details>

---

## **Ejercicio 7: Biblioteca de Libros**

### **Tabla Inicial: Libros**

| ID_Libro | Título | Autores          | Género  |
|----------|--------|-----------------|---------|
| 101      | El Quijote | Cervantes   | Novela  |
| 102      | 1984       | Orwell       | Ciencia Ficción |

### **Tareas:**

1. Aplicar **1FN**, eliminando valores multivaluados en "Autores".
2. Aplicar **2FN**, asegurando que cada atributo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación

<details>
<summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# tabla: **Libro**
| Id_Libro  | Titulo     | Género              |
|-----------|------------|---------------------|
| 101       | El Quijote | Novela              |
| 102       | 1984       | Ciencia Ficción     |

# tabla: **Autores**
| Id_autor  | Autor      |
|-----------|------------|
| 01        | Cervantes  |
| 02        | Orwell     |

# tabla: **Libro_Autor** (Tabla intermedia para la relación N:M)
| Id_Libro  | Id_autor   |
|-----------|------------|
| 101       | 01         |
| 102       | 02         |


</details>
---

## **Ejercicio 8: Facturación de Servicios**

### **Tabla Inicial: Facturas**

| ID_Factura | Cliente   | Servicios Contratados | Costo Total |
|------------|-----------|----------------------|-------------|
| 9001       | Juan P.   | Internet, TV        | 50          |
| 9002       | Ana M.    | Teléfono            | 20          |

### **Tareas:**

1. Aplicar **1FN**, separando valores multivaluados en "Servicios Contratados".
2. Aplicar **2FN**, asegurando que cada atributo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación
<details>
<summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# tabla: ** Cliente**
|   Id_cliente  |   Cliente |   
|---------------|-----------|
|   01          |   Juan P. |
|   02          |   Ana M.  |

# tabla **Servicios**
| Id_servicio   |   Serv_Contratados    |  precio   |
|---------------|-----------------------|-----------|
|   50          |   internet            |  50       |
|   51          |   tv                  |   50      |
|   52          |   telefono            |   20      |

# tabla: ** Id_factura**
| Id_factura    |   Id_cliente  |   Costo_total |
|---------------|---------------|---------------|
|   9001        |   01          |   50          |
|   9002        |   02          |   20          |

# tabla: **Factura_Servicio** (Tabla intermedia para relación N:M)
| Id_factura | Id_servicio |
|------------|------------|
| 9001       | 1001       |
| 9001       | 1002       |
| 9002       | 1003       |


</details>

---

## **Ejercicio 9: Gestión de Vehículos**

### **Tabla Inicial: Vehículos**

| ID_Vehículo | Marca   | Modelos          | Año |
|------------|--------|----------------|-----|
| 5001       | Toyota  | Corolla, Yaris  | 2022 |
| 5002       | Honda   | Civic          | 2023 |

### **Tareas:**

1. Aplicar **1FN**, eliminando valores multivaluados en "Modelos".
2. Aplicar **2FN**, asegurando que cada atributo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación

<details>
<summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# Tabla: **Marca**
| ID_Marca | Marca   |
|----------|--------|
| 01       | Toyota |
| 02       | Honda  |

# Tabla: **Modelo**
| ID_Modelo | Modelo  | ID_Marca | Año  |
|-----------|--------|----------|------|
| 1001      | Corolla | 01       | 2022 |
| 1002      | Yaris   | 01       | 2022 |
| 1003      | Civic   | 02       | 2023 |

</details>

---

## **Ejercicio 10: Gestión de Proyectos**

### **Tabla Inicial: Proyectos**

| ID_Proyecto | Nombre       | Miembros        | Presupuesto |
|------------|-------------|----------------|------------|
| 7001       | Web App     | Juan, Ana      | 5000       |
| 7002       | E-commerce  | Pedro, María   | 10000      |

### **Tareas:**

1. Aplicar **1FN**, eliminando valores multivaluados en "Miembros".
2. Aplicar **2FN**, asegurando que cada atributo dependa completamente de la clave primaria.

> Verifica generando el modelo Entidad/Relación

<details>
<summary style="cursor: pointer; color: red;">RESULTADO:</summary>

# Tabla: **Proyecto**
| ID_Proyecto | Nombre      | Presupuesto |
|------------|-------------|------------|
| 7001       | Web App     | 5000       |
| 7002       | E-commerce  | 10000      |

# Tabla: **Miembro**
| ID_Miembro | Nombre  |
|------------|---------|
| 01         | Juan    |
| 02         | Ana     |
| 03         | Pedro   |
| 04         | María   |

# Tabla: **Proyecto_Miembro** (relación N:M)
| ID_Proyecto | ID_Miembro |
|------------|------------|
| 7001       | 01         |
| 7001       | 02         |
| 7002       | 03         |
| 7002       | 04         |

</details>


 </div>


