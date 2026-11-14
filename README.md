# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-14
Este diagrama entidad-relación (o modelo relacional) representa la estructura lógica de un **sistema de gestión de recetas de cocina y comunidad culinaria** (como un portal o red social de cocina), diseñado para administrar los perfiles de los miembros, las recetas publicadas, sus ingredientes, pasos de elaboración y las reseñas o valoraciones de los usuarios.

A continuación se detalla qué representa cada tabla y cómo se relacionan entre sí:

### 1. Entidades Principales (Tablas)

* **`MIEMBRO`**: Almacena la información de los usuarios registrados en la plataforma.


* *Campos:* `ID_USUARIO` (Clave Primaria), `TIPO_PERFIL`, `NOMBRE`, `CORREO` y `CONTRASENA`.




* **`RECETA`**: Contiene la información principal de cada platillo compartido.


* *Campos:* `ID_RECETAS` (Clave Primaria), `DIFICULTAD`, `PORCIONES`, `TITULO`, `DESCRIPCION`, `TIEMPO_PREPARACION` e `ID_USUARIO` (Clave Foránea que indica qué miembro creó la receta).




* **`PASOS`**: Detalla el procedimiento o el paso a paso secuencial para la elaboración de la receta.


* *Campos:* `ID_PASOS` (Clave Primaria), `DESCRIPCION`, `NUMERO_PASO`, `IMAGEN_OPCIONAL` e `ID_RECETA` (Clave Foránea).




* **`INGREDIENTE`**: Almacena el catálogo de alimentos y componentes disponibles en el sistema.


* *Campos:* `ID_INGREDIENTE` (Clave Primaria), `NOMBRE`, `UNIDAD_MEDIDA`, `INFORMACION_NUTRICIONAL` y `MODO_USO`.




* **`DETALLE_RECETA`**: Es una tabla intermedia que resuelve una relación de muchos a muchos (N:M) entre `RECETA` e `INGREDIENTE`.


* *Campos:* `ID_RECETA` y `ID_INGREDIENTE` (ambas forman la Clave Primaria compuesta y actúan como Claves Foráneas), además del atributo `CANTIDAD` necesaria de ese ingrediente para la receta.




* **`RESEÑA`**: Registra las valoraciones, calificaciones y comentarios de los usuarios sobre las recetas.


* *Campos:* `ID_RESEÑA` (Clave Primaria), `PUNTUACION`, `COMENTARIO`, `FECHA_PUBLICACION`, `ID_RECETA` e `ID_USUARIO` (Claves Foráneas que indican qué usuario hizo la reseña y a qué receta pertenece).





---

### 2. Relaciones Principales

* **Creación de recetas:** Un miembro puede publicar múltiples recetas, pero cada receta pertenece a un único autor (relación de 1 a N).


* **Composición de la receta:** Una receta se divide en múltiples `PASOS` secuenciales y utiliza una lista de `INGREDIENTES` específicos gestionados a través de la tabla intermedia `DETALLE_RECETA`.


* **Interacción y retroalimentación:** Los miembros pueden puntuar y comentar las recetas publicadas mediante el sistema de `RESEÑAS` (relaciones de 1 a N).
<img width="1132" height="712" alt="EJERCICIO 14-MR drawio" src="https://github.com/user-attachments/assets/d713f0b7-d38e-4342-80ed-792980434cfe" />
Este diagrama muestra el **proceso completo de normalización de bases de datos** aplicado a un sistema de gestión de recetas de cocina y comunidad culinaria, transformando una estructura inicial desnormalizada (Forma Normal 0) hasta llegar al diseño relacional optimizado en Tercera Forma Normal (3FN).

A continuación se detalla cada una de las fases representadas:

---

### 1. Fase Normal 0 (FN0) — Tabla No Normalizada

* **Qué se hace:** Se parte de una **única tabla plana y masiva** que concentra toda la información mezclada en una sola estructura: datos de los usuarios, recetas creadas, y grupos repetitivos anidados en celdas (como pasos de preparación e ingredientes con sus cantidades).
* **Problema:** Contiene colecciones y grupos de datos repetitivos dentro de las celdas, generando una alta redundancia y dificultando la administración o consulta de la información.

---

### 2. Primera Forma Normal (1FN)

* **Qué se hace:** Se eliminan los grupos repetitivos asegurando que **todos los atributos sean atómicos** (cada celda contiene un único valor), expandiendo los registros para que cada fila represente una combinación individual y libre de valores anidados.
* **Resultado:** Se obtiene una tabla tabular plana donde cada campo es indivisible, aunque todavía existe una alta duplicidad de datos en los perfiles de usuario y las recetas.

---

### 3. Segunda Forma Normal (2FN)

* **Qué se hace:** Se parte de la 1FN y se eliminan las **dependencias parciales**. Se separan los atributos basándose en sus claves principales correspondientes, desglosando la información en cuatro tablas independientes y normalizadas:
* **`TABLA MIEMBRO`**: Almacena los perfiles de los usuarios.


* **`TABLA RECETA`**: Contiene la información general de los platillos.


* **`TABLA INGREDIENTE`**: Gestiona el catálogo de alimentos y sus propiedades nutricionales.


* **`TABLA DETALLE_RECETA`**: Tabla intermedia que relaciona de forma limpia las recetas con sus ingredientes y cantidades específicas.





---

### 4. Tercera Forma Normal (3FN)

* **Qué se hace:** Se eliminan las **dependencias transitivas**, asegurando que ningún atributo no clave dependa de otro atributo no clave. El diseño se consolida en un modelo relacional robusto y totalmente normalizado, interconectado mediante claves foráneas (FK), lo que garantiza la integridad referencial para la plataforma culinaria:
* **`TABLA MIEMBRO`**: Gestiona los usuarios y credenciales de acceso.


* **`TABLA RECETA`**: Administra los datos de las preparaciones y tiempos.


* **`TABLA INGREDIENTE`**: Mantiene el catálogo de componentes alimenticios.


* **`TABLA DETALLE_RECETA`**: Resuelve la relación de muchos a muchos (N:M) entre recetas e ingredientes con sus respectivas cantidades.


* **`TABLA RESEÑA`**: Registra las valoraciones, puntuaciones y comentarios realizados por los miembros sobre las recetas.
<img width="3882" height="2520" alt="EJERCICIO 14-FASES DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/4c0b4b03-654e-479b-bc7f-80e4dd34a8ac" />

