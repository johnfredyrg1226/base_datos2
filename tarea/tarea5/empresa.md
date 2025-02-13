<div align="justify">

# Code, Learn & Practice(MR: Construye el modelo relacional basado en la descripción que se aporta)

## Descripción

Una empresa necesita organizar la siguiente información referente a su organización interna.
La empresa está organizada en una serie de departamentos. Cada departamento tiene un
código, nombre y presupuesto anual. Cada departamento está ubicado en un centro de trabajo. La información que se desea guardar del centro de trabajo es el código de centro, nombre, población y dirección del centro.
La empresa tiene una serie de empleados. Cada empleado tiene un teléfono, fecha de
alta en la empresa, NIF y nombre. De cada empleado también interesa saber el número de hijos que tiene y el salario de cada empleado.
A esta empresa también le interesa tener guardada información sobre los hijos de los
empleados. Cada hijo de un empleado tendrá un código, nombre y fecha de nacimiento.
Se desea mantener también información sobre las habilidades de los empleados (por ejemplo, mercadotecnia, trato con el cliente, fresador, operador de telefonía, etc…). Cada
habilidad tendrá una descripción y un código”.
Se pretende diseñar el __modelo E/R__ y el modelo relacional teniendo en cuenta los siguientes aspectos:

- Un empleado está asignado a un único departamento. Un departamento estará compuesto por uno o más empleados.
- Cada departamento se ubica en un único centro de trabajo. Estos se componen de
uno o más departamentos.
- Un empleado puede tener varios hijos.
- Un empleado puede tener varias habilidades, y una misma habilidad puede ser
poseída por empleados diferentes.
- Un centro de trabajo es dirigido por un empleado. Un mismo empleado puede dirigir centros de trabajo distintos.

___Construye a través de diagrams.io.___
<div align="justify">

![EMPRESA](https://github.com/johnfredyrg1226/base_datos2/blob/main/tarea/tarea5/empresas.drawio.png)


## Modelo Relacional: Organización Empresarial

### Descripción

Una empresa necesita organizar su información interna de la siguiente manera:

- **Departamentos**: Cada departamento tiene un código, nombre y presupuesto anual, y se ubica en un centro de trabajo.
- **Centros de trabajo**: Se identifican por su código, nombre, población y dirección, y pueden contener múltiples departamentos.
- **Empleados**: Cada empleado tiene un NIF, nombre, teléfono, fecha de alta en la empresa, número de hijos y salario. Además, cada empleado pertenece a un único departamento.
- **Hijos de empleados**: Se identifican por un código, nombre y fecha de nacimiento.
- **Habilidades**: Cada empleado puede poseer múltiples habilidades, identificadas por un código y descripción. Estas pueden ser compartidas por diferentes empleados.

### Relaciones Clave y Cardinalidades

- Un **empleado** (*1,1*) pertenece a un único **departamento**, pero un **departamento** (*1,N*) puede tener múltiples **empleados**.
- Un **departamento** (*1,1*) se ubica en un único **centro de trabajo**, pero un **centro** (*1,N*) puede albergar varios **departamentos**.
- Un **empleado** (*1,N*) puede tener varios **hijos**, pero un **hijo** (*1,1*) pertenece a un solo **empleado**.
- Un **empleado** (*1,N*) puede tener múltiples **habilidades**, y una misma **habilidad** (*1,N*) puede ser compartida por varios **empleados**. (Relación muchos a muchos)
- Un **centro de trabajo** (*1,1*) es dirigido por un único **empleado**, pero un **empleado** (*1,N*) puede dirigir más de un **centro**.

### Tablas Relacionales

#### Tabla: `CentroTrabajo`
- **CodigoCentro** (PK)
- **Nombre**
- **Poblacion**
- **Direccion**
- **NIFEmpleado** (FK) → `Empleado` (Empleado que dirige el centro)

#### Tabla: `Departamento`
- **CodigoDepartamento** (PK)
- **Nombre**
- **PresupuestoAnual**
- **CodigoCentro** (FK) → `CentroTrabajo`

#### Tabla: `Empleado`
- **NIF** (PK)
- **Nombre**
- **Telefono**
- **FechaAlta**
- **NumHijos**
- **Salario**
- **CodigoDepartamento** (FK) → `Departamento`

#### Tabla: `Hijo`
- **CodigoHijo** (PK)
- **Nombre**
- **FechaNacimiento**
- **NIFEmpleado** (FK) → `Empleado`

#### Tabla: `Habilidad`
- **CodigoHabilidad** (PK)
- **Descripcion**

#### Tabla: `EmpleadoHabilidad` (Intermedia para relación N:M)
- **NIFEmpleado** (FK) → `Empleado`
- **CodigoHabilidad** (FK) → `Habilidad`
</div>