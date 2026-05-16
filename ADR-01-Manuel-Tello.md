# ADR-01: [LootearApp]

| Campo  | Valor |
|--------|-------|
| Autor  | [Manuel Tello May] |
| Fecha  | 15/05/2026|
| Estado | `Propuesto`|

---

## Contexto

Se va a desarrollar una app para videojugadores activos, esta aplicación permite a cada jugador registar los juegos que demanden más tiempo, esta permite configurar recordatorios de los materiales que require recolectar constantemente (farmear) para contruir objetos o armas especificos dentro de cada juego, la aplicacion procesará esos datos para crear una rutina de recoleccion optimizada para los materiales necesitados.
Para esto voy a implemantar las siguientes entidades: jugador, plataforma, notificaciones, juego_plataforma y cantidad_material.

---

## Decisión

Decidi implementar un diseño MVC que me permita comunicarme con una aplicacion web y tal vez en algun futuro pasar a una aplicacion móvil, el almacenamiento de los datos se guardara en una base de datos con el fin de llevar un correcto conteo de los materiales que se necesiten y ademas los juegos y la plataforma a la que pertenezcan.

### ¿Por qué?

Consistencia: La entidad juego_plataforma funciona como una relacion la cual permite saber en que consola se juega cada juego.
Optimización de rutinas: Al usar el MVC se pueden separar las rutinas utilizando el controlado y el modelo, de la intrerfaz del usuario.
Notificaciones: El sistema de notificaciones estaria gestionado por un servicio en segundo plano el cual va a consultar las alertas pendientes.

### Alternativas consideradas

| Alternativa                                                 Por qué la descarté |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------|
|Microservicios                       | La descarte por el tamaño del proyecto, agregar esta arquitectura saldria más costosa que mantener el proyecto|
| Base de datos no relacional         | El uso de ese tipo de base de datos en mi proyecto significa tener duplicidad en los datos y las rutinas podrian verse afectadas                 |
| Arquitectura monolitica             | La descarte porque mi idea es que el proyecto poco a poco vaya captando más jugadores por lo tanto para lograr esto necesito almacenar los datos en un servidor para que los jugadores puedan acceder a sus rutinas.               |

--
## Consecuencias

**✅ Lo que gano:**

- Consecuencia **técnica** : Al dividir las rutinas de la interfaz, puedo realizar modificaciones de optimizacion para el farmeo sin que el jugador necesite actulizar la app obligatoriamente.
- Consecuencia sobre el **proceso o el equipo** : Se puede desarrollar en pararelo, se pueden desarrollar las pantallas de visualizacion y la estructura lógica de la aplicación por separado sin afectar lo demás.

**⚠️ Lo que sacrifico o asumo:**

- **Limitación técnica** : Sobrecarga de peticiones HTTP
- **Deuda o riesgo** : Podra presentanse mucha latencia si los inventarios aumentan demasiado.

## Diagrama

Diagrama en mermaid.

![Diagrama del sistema]( https://mermaid.ai/d/d3a332e6-7c0d-4d70-935f-020c922a3d7f)
