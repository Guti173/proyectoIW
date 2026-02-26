```
# proyectoIW

========================================
MODELO DE DATOS
========================================

USUARIO
----------------------------------------
- id (PK)
- username (String, único)
- email (String, único)
- password (String cifrada)
- nombre (String)
- apellido (String)
- fotoPerfil (String / URL)
- estadoCuenta (Enum: ACTIVO, BLOQUEADO)


SERIE
----------------------------------------
- id (PK)
- titulo (String)
- descripcion (Text)
- fechaEstreno (Date)
- fechaFin (Date, nullable)
- imagenPortada (String / URL)
- numneroEpisodios (Integer)
- estado (Enum: EN_EMISION, FINALIZADA)
- mediaValoracion (Decimal) (calculada)
- totalValoraciones (Integer)


GENERO
----------------------------------------
- id (PK)
- nombre (String, único)
- descripcion (Text)


RELACIÓN SERIE – GENERO (N:N)
----------------------------------------
- id (PK)
- serie (FK → Serie)
- genero (FK → Genero)


LISTAUSUARIO
----------------------------------------
- id (PK)
- usuario (FK → Usuario)
- serie (FK → Serie)
- tipoLista (Enum: VIENDO, FAVORITA, PENDIENTE, FINALIZADA)
- fechaAgregado (DateTime)

Relación:
- Usuario 1–N ListaUsuario
- Serie 1–N ListaUsuario

Entre usuario y serie relación una con toda la lista de series.


PROGRESOSERIE
----------------------------------------
- id (PK)
- usuario (FK → Usuario)
- serie (FK → Serie)
- episodiosVistos (Integer)
- fechaInicio
- fechaFin
- ultimaActualizacion (DateTime)

Relación:
- Usuario 1–N ProgresoSerie
- Serie 1–N ProgresoSerie


VALORACION
----------------------------------------
- id (PK)
- usuario (FK → Usuario)
- serie (FK → Serie)
- puntuacion (Integer 1–5)

Restricción lógica:
- Un usuario solo puede valorar una serie una vez.


COMENTARIO
----------------------------------------
- id (PK)
- contenido (Text)
- fechaPublicacion (DateTime)
- usuario (FK → Usuario)
- serie (FK → Serie)
- estado (Enum: ACTIVO, REPORTADO, ELIMINADO)


LIKECOMENTARIO
----------------------------------------
- id (PK)
- usuario (FK → Usuario)
- comentario (FK → Comentario)

Restricción:
- Un usuario solo puede dar like una vez por comentario.


AMISTAD
----------------------------------------
- id (PK)
- solicitante (FK → Usuario)
- receptor (FK → Usuario)
- estado (Enum: PENDIENTE, ACEPTADA, RECHAZADA)
- fechaSolicitud (DateTime)
- fechaRespuesta (DateTime)

Es una autorrelación N–N de Usuario.


REPORTECOMENTARIO
----------------------------------------
- id (PK)
- usuario (FK → Usuario)
- comentario (FK → Comentario)
- motivo (Text)
- fechaReporte (DateTime)
- estado (Enum: PENDIENTE, REVISADO)


========================================
RELACIONES
========================================

- Usuario 1–N ListaUsuario
- Usuario 1–N ProgresoSerie
- Usuario 1–N Valoracion
- Usuario 1–N Comentario
- Usuario 1–N LikeComentario
- Usuario 1–N ReporteComentario
- Usuario N–N Usuario (Amisad)

- Serie 1–N ListaUsuario
- Serie 1–N ProgresoSerie
- Serie 1–N Valoracion
- Serie 1–N Comentario
- Serie N–N Genero
```
