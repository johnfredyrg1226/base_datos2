# Code, Learn & Practice (E/R)

## Descripción

La liga de fútbol profesional ha decidido informatizar sus instalaciones creando una base de datos para guardar la información de los partidos que se juegan en la liga.

Se desea guardar en primer lugar los datos de los jugadores. De cada jugador se quiere guardar el nombre, fecha de nacimiento y posición en la que juega (portero, defensa, centrocampista…). Cada jugador tiene un código de jugador que lo identifica de manera única.

De cada uno de los equipos de la liga es necesario registrar el nombre del equipo, nombre del estadio en el que juega, el aforo que tiene, el año de fundación del equipo y la ciudad de la que es el equipo. Cada equipo también tiene un código que lo identifica de manera única. Un jugador solo puede pertenecer a un único equipo. De cada partido que los equipos de la liga juegan hay que registrar la fecha en la que se juega el partido, los goles que ha metido el equipo de casa y los goles que ha metido el equipo de fuera. Cada partido tendrá un código numérico para identificar el partido.

También se quiere llevar un recuento de los goles que hay en cada partido. Se quiere almacenar el minuto en el que se realiza el gol y la descripción del gol. Un partido tiene varios goles y un jugador puede meter varios goles en un partido.

Por último, se quiere almacenar, en la base de datos, los datos de los presidentes de los equipos de fútbol (DNI, nombre, apellidos, fecha de nacimiento, equipo del que es presidente y año en el que fue elegido presidente). Un equipo de fútbol tan sólo puede tener un presidente, y una persona sólo puede ser presidente de un equipo de la liga.

Diseña el modelo entidad-relación resultante a través de diagrams.io.

## Diagrama Entidad-Relación

![Diagrama ER]()
🔹 Entidades y Relaciones
Jugador (CódigoJugador, Nombre, FechaNacimiento, Posición, CódigoEquipo)

Relación: Pertenece a (1,1) → (0,N) Equipo
Equipo (CódigoEquipo, Nombre, Estadio, Aforo, AñoFundación, Ciudad)

Relación: Tiene (1,1) → (1,1) Presidente
Relación: Juega (1,N) → (1,1) Partido (como local o visitante)
Presidente (DNI, Nombre, Apellidos, FechaNacimiento, AñoElección, CódigoEquipo)

Relación: Es presidente de (1,1) → (1,1) Equipo
Partido (CódigoPartido, Fecha, GolesLocal, GolesVisitante, CódigoEquipoLocal, CódigoEquipoVisitante)

Relación: Se juega entre (1,N) → (1,1) Equipo
Gol (CódigoGol, Minuto, Descripción, CódigoPartido, CódigoJugador)

Relación: Es marcado en (1,N) → (1,1) Partido
Relación: Es marcado por (1,N) → (1,1) Jugador

# Modelo Relacional de Fútbol

## Tablas

### Jugador
- **CódigoJugador** (PK)
- **Nombre**
- **FechaNacimiento**
- **Posición**
- **CódigoEquipo** (FK)

**Relación:**
- Un jugador *pertenece* a un equipo (**1,1 → 0,N**)

### Equipo
- **CódigoEquipo** (PK)
- **Nombre**
- **Estadio**
- **Aforo**
- **AñoFundación**
- **Ciudad**

**Relaciones:**
- Un equipo *tiene* un presidente (**1,1 → 1,1**)
- Un equipo *juega* partidos como local o visitante (**1,N → 1,1**)

### Presidente
- **DNI** (PK)
- **Nombre**
- **Apellidos**
- **FechaNacimiento**
- **AñoElección**
- **CódigoEquipo** (FK)

**Relación:**
- Un presidente *es presidente de* un equipo (**1,1 → 1,1**)

### Partido
- **CódigoPartido** (PK)
- **Fecha**
- **GolesLocal**
- **GolesVisitante**
- **CódigoEquipoLocal** (FK)
- **CódigoEquipoVisitante** (FK)

**Relación:**
- Un partido *se juega entre* equipos (**1,N → 1,1**)

### Gol
- **CódigoGol** (PK)
- **Minuto**
- **Descripción**
- **CódigoPartido** (FK)
- **CódigoJugador** (FK)

**Relaciones:**
- Un gol *es marcado en* un partido (**1,N → 1,1**)
- Un gol *es marcado por* un jugador (**1,N → 1,1**)

