<div>


# <img src=../../../../../images/computer.png width="40"> Code, Learn & Practice(Base de datos (Gestión Tienda)")

# 

La siguiente tabla muestra la información de una tienda con sus productos.

## Base de Datos No Normalizada: Tienda

| ProductoID | Nombre          | Categorias                  | Precio | ClienteID | NombreCliente | DireccionesEnvio                    |
|------------|-----------------|-----------------------------|--------|-----------|---------------|-------------------------------------|
| 1          | Laptop HP       | Electrónicos, Informática   | 800    | 101       | Juan          | Calle 1, Ciudad A / Calle 2, Ciudad A |
| 2          | Camiseta Nike    | Ropa, Deportes              | 30     | 102       | María         | Calle 3, Ciudad B                    |
| 3          | Libro "Dune"     | Libros, Ciencia Ficción     | 20     | 101       | Juan          | Calle 1, Ciudad A                     |

Se pide:

- Verifica y transforma a __1FN__ justificando la respuesta.
- Verifica y transforma a __2FN__ justificando la respuesta.
- Verifica y transforma a __3FN__ justificando la respuesta.

<details>
 <summary style="cursor: pointer; color: red;">RESULTADO:</summary>

## **Tablas en 1FN:**

## **Tabla: Producto**
| Producto_ID | Nombre        | Precio |
|------------|--------------|--------|
| 1          | Laptop HP    | 800    |
| 2          | Camiseta Nike| 30     |
| 3          | Libro Dune   | 20     |

## **Tabla: Categoría**  
| Producto_ID | Categoría        |
|------------|------------------|
| 1          | Electrónicos     |
| 1          | Informática      |
| 2          | Ropa            |
| 2          | Deportes        |
| 3          | Libros          |
| 3          | Ciencia Ficción |

## **Tabla: Cliente**  
| Cliente_ID | Nombre_Cliente |
|-----------|---------------|
| 101       | Juan          |
| 102       | María         |

## **Tabla: Dirección de Envio**  
| Cliente_ID | Dirección           |
|-----------|---------------------|
| 101       | Calle 1, Ciudad A   |
| 101       | Calle 2, Ciudad A   |
| 102       | Calle 3, Ciudad B   |


## **Justificación 1FN:**  
Se eliminaron **grupos repetidos** (Direcciones y Categorías en una misma celda) y cada atributo contiene **un solo valor atómico**.
---

## **2FN (Segunda Forma Normal)**
- La tabla ya estaba en **1FN**.  
- Se eliminaron dependencias parciales: **NombreCliente** solo depende de **ClienteID**, así que se separó en su propia tabla.  
- **Dirección de envío** se separó porque podría tener múltiples direcciones.


## **Justificación 2FN:**  
- Todos los atributos dependen completamente de la clave primaria de su respectiva tabla.  
- No hay dependencias parciales (es decir, todos los datos de cada tabla dependen enteramente de su clave).  
---

## **3FN (Tercera Forma Normal)**
## **Correcciones realizadas:**
- **Direcciones de Envío** tiene una dependencia transitiva con la ciudad, así que se creó una tabla **Ciudad**.  

## **Tablas en 3FN:**

## **Tabla: Ciudad**  
| Ciudad_ID | Nombre_Ciudad |
|----------|--------------|
| 1        |     Ciudad A     |
| 2        |    Ciudad B     |

## **Tabla: Dirección de Envio**  
| Cliente_ID | Dirección | Ciudad_ID |
|-----------|----------|-----------|
| 101       |   Calle 1  |  1    |
| 101       |   Calle 2  |  1      |
| 102       |   Calle 3  |  2     |


## **Justificación 3FN:**  
- Se eliminó la **dependencia transitiva** de las direcciones con la ciudad al crear una nueva tabla **Ciudad**.  
- Ahora, **Ciudad** no depende de **Cliente_ID**, sino de su propia clave primaria.
---












**<h2>formas normales</h2>**
 **Primera Forma Normal (1FN)**
🔹 Regla principal: Eliminar valores repetidos y asegurar que todos los atributos sean atómicos (indivisibles).
🔹 Requisitos:

- Cada columna debe contener solo un valor por celda.
- No puede haber grupos repetidos (como listas o conjuntos de datos en una misma - celda).
- Se debe identificar una clave primaria.

**Segunda Forma Normal (2FN)**
🔹 Regla principal: Eliminar dependencias parciales (un campo debe depender de toda la clave primaria, no de una parte).
🔹 Requisitos:

- Debe estar en 1FN.
- Si hay clave compuesta, los atributos no clave deben depender completamente de toda la clave primaria.

**Tercera Forma Normal (3FN)**
🔹 Regla principal: Eliminar dependencias transitivas (un campo no clave debe depender directamente de la clave primaria, no de otro campo no clave).
🔹 Requisitos:

Debe estar en 2FN.
Ningún atributo no clave debe depender de otro atributo no clave.






</details>


 </div>