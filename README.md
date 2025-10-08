<!-- ───────────────────────────────  HEADER  ─────────────────────────────── -->
# 🌌  **M a y a D B**  🌌  

<pre>
███╗   ███╗  █████╗    ██╗   ██╗   █████╗    ██████╗    ██████╗    
████╗ ████║ ██╔══██╗   ╚██╗ ██╔╝  ██╔══██╗   ██╔══██╗   ██╔══██╗   
██╔████╔██║ ███████║    ╚████╔╝   ███████║   ██║  ██║   ██████╔╝   
██║╚██╔╝██║ ██╔══██║     ╚██╔╝    ██╔══██║   ██║  ██║   ██╔══██╗   
██║ ╚═╝ ██║ ██║  ██║      ██║     ██║  ██║   ██████╔╝   ██████╔╝   
╚═╝     ╚═╝ ╚═╝  ╚═╝      ╚═╝     ╚═╝  ╚═╝   ╚═════╝    ╚═════╝    
</pre>

> **MayaDB** es una base de datos especializada en autorización y gestión avanzada de accesos, inspirada en el modelo **Google Zanzibar**.  
> Diseñada para simplificar reglas de acceso jerárquicas y relaciones complejas, te permite administrar permisos **granulares**.
---

MayaDB es una base de datos especializada en autorización y gestión avanzada de accesos, inspirada en el modelo Google Zanzibar, reconocido por su efectividad y uso masivo en la infraestructura interna de Google. Esta solución ha sido creada para facilitar la administración de permisos granulares y relaciones complejas en aplicaciones modernas, simplificando significativamente el manejo de reglas de acceso sofisticadas y jerárquicas.

## Características principales

### Inspirado en Google Zanzibar

MayaDB adopta el modelo probado de Google Zanzibar, garantizando así la fiabilidad y eficacia a gran escala. Esto permite manejar grandes volúmenes de relaciones y consultas de autorización con alta eficiencia, tal como lo hacen aplicaciones globales líderes que requieren sistemas robustos y escalables.

### Gestión de Relaciones Complejas

La fortaleza de MayaDB reside en su capacidad para modelar y administrar relaciones altamente detalladas y flexibles. A través de namespaces (espacios de nombres) y relaciones explícitas, permite definir claramente cómo usuarios, roles, grupos y recursos interactúan entre sí. Por ejemplo, es posible establecer permisos dinámicos donde un usuario puede acceder a ciertos documentos únicamente en contextos específicos, dependiendo del rol, del grupo o incluso del estado interno del sistema.

### Escalabilidad y Rendimiento

Diseñada pensando en aplicaciones modernas con grandes demandas, MayaDB puede gestionar miles de solicitudes por segundo, proporcionando respuestas rápidas con latencias muy bajas. Esta capacidad es esencial para aplicaciones críticas que deben mantener un rendimiento constante independientemente de la carga o la cantidad de usuarios.

### API Flexible y Fácil Integración

MayaDB ofrece una API clara y fácil de usar, compatible tanto con REST como con su propio protocolo "maya", lo que simplifica la integración en diversos entornos de desarrollo y arquitecturas modernas como microservicios y sistemas distribuidos.

### Implementaciones Distribuidas y Replicadas

Aunque aún en proceso de estabilización para entornos productivos críticos, MayaDB está diseñada para operar en entornos distribuidos, soportando configuraciones replicadas que eventualmente permitirán alta disponibilidad y tolerancia a fallos.

## Casos de uso típicos

MayaDB es particularmente adecuada para aplicaciones que requieren un alto grado de precisión y complejidad en la gestión de permisos, tales como:

* **Aplicaciones Empresariales:** Para controlar accesos internos complejos y regulados, definiendo claramente roles, grupos y jerarquías internas.
* **Software colaborativo:** Aplicaciones que permiten compartir recursos (como documentos o proyectos) entre usuarios con niveles de permisos detallados y dinámicos.
* **Plataformas de Seguridad:** Donde es crucial el cumplimiento de estrictas regulaciones de privacidad y seguridad, como GDPR, HIPAA, o regulaciones financieras.

## Instalación

### Descargar ejecutables

1. Abre la página de [Releases de MayaDB](https://github.com/juanamv/MAYADB/releases).  
2. Descarga el binario correspondiente a tu sistema operativo (Windows, Linux, macOS).  
3. Si viene en un comprimido (`.zip`, `.tar.gz`), descomprímelo en la carpeta de tu elección.

---

### Generar certificados TLS (para conexiones seguras)

> **Importante:** Nunca compartas tu **clave privada** (`key.pem`). Sólo distribuye el certificado público (`cert.pem`).  
> **Importante:** Si tienes problemas al generar los certificados, puedes usar HTTP; en ese protocolo MayaDB no requiere certificados.

> **Recomendación (¡muy importante!):**
> Para **pruebas y desarrollo local**, se recomienda **HTTP**, ya que aunque el servidor QUIC está listo, **el cliente oficial aún está en desarrollo**. Si no cuentas con certificados o necesitas la mínima fricción, trabaja sobre HTTP y omite la creación de `cert.pem`/`key.pem`.

#### Par auto-firmado (pruebas)

```bash
openssl req -x509 -newkey rsa:2048 \
  -keyout key.pem     \
  -out cert.pem       \
  -days 365           \
  -nodes              \
  -subj "/CN=localhost"
chmod 600 key.pem
````

* `key.pem`: clave privada (permiso `600`).
* `cert.pem`: certificado público (compartible).

---

### Configurar variables de entorno

MayaDB necesita dos credenciales de inicio:

* `MAYA_USER`
* `MAYA_PASS`

#### Linux / macOS (bash, zsh…)

Edita tu `~/.bashrc` o `~/.zshrc`:

```bash
export MAYA_USER="tu_usuario"
export MAYA_PASS="tu_contraseña_segura"
```

Luego:

```bash
source ~/.bashrc   # o ~/.zshrc
```

#### Windows

##### Interfaz gráfica
1. Abre el menú **Inicio** y busca **Variables de entorno** → selecciona **Editar las variables de entorno del sistema**.
2. Haz clic en **Variables de entorno…**.
3. Bajo **Variables de usuario** (o **Variables del sistema** si lo prefieres), pulsa **Nueva…**.

   * **Nombre de la variable**: `MAYA_USER`
   * **Valor de la variable**: `tu_usuario`
4. Repite **Nueva…** para `MAYA_PASS` con tu contraseña.


##### PowerShell (Usuario)

```powershell
[Environment]::SetEnvironmentVariable(
  "MAYA_USER", "tu_usuario", "User"
)
[Environment]::SetEnvironmentVariable(
  "MAYA_PASS", "tu_contraseña_segura", "User"
)
```

Abre una nueva consola para aplicar.

##### CMD

```cmd
setx MAYA_USER "tu_usuario"
setx MAYA_PASS "tu_contraseña_segura"
```

Abre una nueva ventana de CMD.

---

### Ejecutar MayaDB

Desde la carpeta donde esté el binario (`mayadb` o `mayadb.exe`):

```bash
./mayadb
```

Y ya tendrás tu servidor MayaDB corriendo con TLS y credenciales en entorno.

> **Nota:**
>
> * En el repositorio hay un `env.json` para cambiar `protocol` entre `http` o `quic`.
> * Si modificas `protocol`, reinicia el servicio.

#### Inicialización con parámetros CLI (nuevo flujo)

Ahora el binario acepta sobreescritura directa desde la línea de comandos. Esto permite ajustar el servicio sin editar `env.json` ni depender exclusivamente de variables de entorno.

Parámetros soportados:

| Flag                    | Descripción                                                                                | Predeterminado                |
|-------------------------|--------------------------------------------------------------------------------------------|-------------------------------|
| `--port <u16>`          | Puerto de escucha.                                                                         | `8080` (HTTP) / `5000` (QUIC) |
| `--protocol <http|quic>`| Protocolo expuesto. Se recomienda `http` en desarrollo.                                   | `quic`                        |
| `--host <cadena>`       | Dirección de enlace (`127.0.0.1`, `0.0.0.0`, hostname).                                   | `localhost`                   |
| `--path <ruta>`         | Carpeta para LMDB. Se crea si no existe.                                                  | `./MAYA_DB`                   |
| `--user <cadena>`       | Usuario root inicial (sustituye `MAYA_USER`).                                             | cadena vacía                  |
| `--pass <cadena>`       | Contraseña root inicial (sustituye `MAYA_PASS`).                                          | cadena vacía                  |
| `--max-readers <u32>`   | Límite de lectores LMDB concurrentes.                                                     | `512`                         |
| `--map-size <bytes>`    | Tamaño máximo del mapa LMDB (en bytes).                                                   | valor por defecto interno     |
| `--generate-certs`      | Si se especifica, genera `cert.pem`/`key.pem` y finaliza sin levantar el servidor.        | `false`                       |

Ejemplo de arranque personalizado:

```bash
./mayadb \
  --protocol http \
  --port 8080 \
  --host 0.0.0.0 \
  --path ./MAYA_DB \
  --user admin \
  --pass "admin-secret"
```

Otros escenarios comunes:

- **CLI mínima (solo HTTP, credenciales embebidas):**

  ```bash
  ./mayadb --protocol http --user root --pass root
  ```

- **Servidor QUIC en puerto 5001, directorio dedicado:**

  ```bash
  ./mayadb \
    --protocol quic \
    --port 5001 \
    --path /var/lib/mayadb \
    --user quic_admin \
    --pass "quic-secret"
  ```

- **Modo generación de certificados (no levanta servicio):**

  ```bash
  ./mayadb --generate-certs
  # Resultado: cert.pem y key.pem en el directorio actual.
  ```

Si omites un flag, se utilizan los valores de `env.json` o los predeterminados en el binario. Esta modalidad facilita automatizaciones en contenedores, pipelines y entornos multi-stage.

---

### Probar conexión (HTTP)

Si estás usando **HTTP**, puedes usar cualquier cliente REST (Postman, cURL, etc.):

* **Método:** `POST`
* **URL:**

  ```
  http://<host>:<puerto>/q-exec
  ```
* **Body (JSON):**

  ```json
  {
    "version":    "1",
    "user":       "root",
    "password":   "root",
    "db_name":    "dbname",
    "db_version": "1.1:alpha",
    "query":      "Consulta"
  }
  ```

1. Abre Postman (o tu cliente favorito).
2. Selecciona `POST` e introduce la URL `http://localhost:3000/q-exec` (ajusta host/puerto).
3. En la pestaña **Body**, elige `raw` → `JSON` y pega el JSON de ejemplo.
4. Envía la petición y revisa la respuesta.


## Uso Básico

MayaDB utiliza un lenguaje llamado CLRA (Custom Language for Relations and Authorization) para definir esquemas claros y estructurados. Estos esquemas permiten especificar de manera precisa cómo están organizados los recursos, los usuarios y sus relaciones dentro del sistema.

### Definir un esquema con CLRA

Para iniciar con MayaDB, debes definir claramente un esquema que represente las entidades y relaciones específicas de tu aplicación.

Ejemplo básico de esquema:

```clra
db: dbname;
version: 1.1:alpha;

ns User {
    self;
};

ns Group {
    relation owner = User::self;
};

ns Task {
    relation assignee = Group::member;
};
```

### Componentes de un esquema

#### Headers

Los encabezados definen el contexto general del esquema, estableciendo dos elementos fundamentales:

```clra
db: dbname;
version: 1.1:alpha;
```

* `db`: Indica el nombre de la base de datos interna en la cual el esquema será aislado.
* `version`: Define la versión del esquema, permitiendo gestionar evoluciones y cambios futuros del esquema sin conflictos.

#### Namespace

Los namespaces (espacios de nombres) son elementos fundamentales en CLRA que agrupan propiedades y relaciones. Se utilizan para definir claramente las entidades que se gestionarán en MayaDB:

```clra
ns User {
    self;
};
```

* `ns`: Define un espacio de nombres (namespace).
* `User`: Es el nombre del namespace, que debe iniciar siempre con una letra mayúscula.
* `self;`: Palabra reservada que indica que la referencia de este namespace apunta directamente hacia sí misma. Esto implica que es un nodo inicial o final, lo que evita que se creen relaciones adicionales directamente desde este namespace.

#### Relations

Las relaciones especifican cómo los diferentes namespaces interactúan y se conectan entre sí. Se utilizan para definir dependencias claras y permisos jerárquicos:

Ejemplo:

```clra
ns Group {
    relation owner = Group::self;
};
```

* `relation`: Palabra clave para definir una relación.
* `owner`: Nombre dado a la relación, que especifica claramente el tipo de interacción o propiedad entre namespaces.
* `Group::self`: Define que esta relación apunta específicamente a una entidad del namespace `Group`.

Se pueden crear relaciones más complejas utilizando operadores lógicos como `|` para especificar múltiples posibles entidades válidas para una relación:

```clra
relation owner = Group::owner | User::self;
```

* Aquí se establece claramente que la entidad `owner` puede referirse a un propietario del namespace `Group` o directamente a un usuario del namespace `User`. Esto permite validar y gestionar permisos complejos con mayor flexibilidad y precisión.

#### JSON Types

Los `JSON Types` permiten definir claramente metadatos adicionales en un namespace, facilitando la gestión y el almacenamiento de información complementaria que no necesariamente forma parte directa de las relaciones, pero que sí es útil o necesaria dentro del contexto de una entidad.

Ejemplo de definición:

```clra
json types {
    name: string required default = "name";
    age: number required;
    email: string required default = "example@example.com" email_format;
};
```

* **name**: Este campo es una cadena de texto (`string`), requerido, y posee un valor predeterminado de "name".
* **age**: Campo numérico (`number`), requerido, que debe proporcionarse explícitamente al crear o actualizar una entidad.
* **email**: Cadena de texto (`string`) requerida con un valor predeterminado específico, que además tiene una restricción adicional: debe cumplir un formato válido de correo electrónico. MayaDB verificará automáticamente esta condición antes de aceptar cualquier entidad que use este campo.

##### Ventajas de los JSON Types

* **Eficiencia y rapidez:** Permiten almacenar información útil directamente dentro del namespace, evitando la necesidad de mantener una base de datos adicional y sincronizarla constantemente.
* **Accesibilidad universal:** Estos metadatos están disponibles desde cualquier punto de la base de datos, simplificando considerablemente las consultas que requieran información contextual adicional.
* **Flexibilidad:** Aunque no son obligatorios, su uso permite definir claramente qué información adicional puede o debe acompañar a cada entidad, facilitando validaciones más complejas y precisas.

##### Tipos de datos soportados

MayaDB maneja estrictamente los siguientes tipos de datos en los `JSON Types`:

* `string`: texto o cadenas de caracteres.
* `number`: números (no distingue entre enteros y decimales).
* `boolean`: valores verdaderos o falsos.
* `array`: listas homogéneas de elementos del mismo tipo.
* `object`: estructuras más complejas que pueden contener múltiples campos internos.

Debido a que no existen tipos específicos como `int` o `float`, se recomienda usar `number` para cualquier dato numérico. Además, los arrays deben ser homogéneos, es decir, todos los elementos deben ser del mismo tipo.

##### Buenas prácticas y recomendaciones

* **Evitar estructuras demasiado complejas:** Aunque es posible anidar objetos dentro de arrays y viceversa, se recomienda limitar la complejidad de las estructuras para facilitar las actualizaciones frecuentes y agilizar las consultas.
* **Mantener la información en primer nivel:** MayaDB indexa eficientemente los campos en el nivel superior del JSON. Por lo tanto, los datos que necesitan actualizaciones constantes o rápidas deben mantenerse lo más cerca posible del nivel raíz.
* **Validación estricta:** MayaDB realiza automáticamente comprobaciones estrictas en la creación de entidades. Si se proporciona un dato con un tipo incorrecto o en un formato inválido, MayaDB retornará un error claro, asegurando así la consistencia y la integridad de los datos.


### Annotations \[check]

Las anotaciones `@check` permiten implementar validaciones avanzadas y específicas en las relaciones definidas dentro de los namespaces. Estas anotaciones facilitan la creación de reglas de acceso condicionales y dinámicas basadas en estados internos, roles de usuarios, o condiciones ambientales.

Ejemplo de anotación con validaciones avanzadas:

```clra
ns User {
    relation owner = User::self @check{
        AllowIf: ($role == "admin" OR $role == "moderator") AND #system.status == "active"
        DenyIf: NOT (::resource.permissions NOT_IN $user.permissions)
    }
};
```

#### Explicación detallada del ejemplo:

* **AllowIf:** Esta condición permite que la relación exista únicamente si el usuario tiene un rol específico (`admin` o `moderator`) y el sistema está activo (`#system.status == "active"`).
* **DenyIf:** Esta condición niega automáticamente la relación si los permisos del recurso están incluidos en los permisos del usuario (la lógica de doble negación se utiliza aquí para demostrar flexibilidad en validaciones complejas).

#### Orden y flujo de ejecución:

Las validaciones en `@check` siguen un flujo predeterminado basado en el principio de **"Implicit Deny"**, lo cual significa que, por defecto, todas las relaciones se deniegan a menos que explícitamente se permitan. Por lo tanto, aunque en el ejemplo anterior la condición `AllowIf` está escrita antes de `DenyIf`, en realidad el flujo interno es:

1. Primero se evalúa siempre la condición `DenyIf`. Si esta condición es verdadera, la relación se deniega inmediatamente, sin evaluar `AllowIf`.
2. Luego se evalúa la condición `AllowIf`. Si esta condición se cumple, la relación es permitida.
3. Si ninguna de las condiciones anteriores se cumple, la relación se deniega por defecto.

#### Acceso a información adicional:

Las anotaciones permiten acceder a diversos tipos de información para realizar validaciones más complejas:

* **Variables de entorno (`#system`)**: Puedes consultar estados globales del sistema, por ejemplo, si el sistema está activo o en mantenimiento. Estas variables siempre son consideradas tipo "string".
* \*\*\*\*Metadatos del namespace (`::`)\*\*: Permite acceder directamente a los datos almacenados previamente como `JSON Types` dentro del namespace consultado, facilitando la verificación de información específica de entidades o datos guardados previamente.
* **Metadatos de usuario (`$user`)**: Se pueden utilizar datos adicionales enviados al momento de realizar la consulta, como permisos o roles específicos asignados al usuario actual.

#### Precauciones y recomendaciones:

* **Uso moderado de variables de entorno:** Cada consulta de variables ambientales implica una interacción adicional con el sistema, lo que puede afectar negativamente el rendimiento en sistemas con alta carga o muchas peticiones simultáneas.
* **Profundidad de relaciones:** Dado que cada validación se ejecuta secuencialmente en todas las relaciones involucradas, se recomienda mantener un control sobre la profundidad y complejidad de las relaciones para evitar impactos negativos en el rendimiento.
* **Metadatos JSON:** Durante las validaciones, es posible enviar metadatos serializados en formato JSON estándar que pueden ser utilizados en `@check` para realizar validaciones aún más precisas y complejas.

#### Sintaxis utilizada en `@check`:

* **`AllowIf`**: Define una condición específica bajo la cual la relación será explícitamente permitida.
* **`DenyIf`**: Establece condiciones específicas bajo las cuales la relación será explícitamente denegada.
* **`#system`**: Permite acceder a variables ambientales o del sistema.
* **`::resource`**: Permite acceder a metadatos específicos del recurso dentro del namespace actual.
* **`$user`**: Permite acceder a información adicional sobre el usuario, enviada al realizar la consulta.


### Annotations \[script] (Experimental)

Las anotaciones `@script` permiten realizar validaciones avanzadas mediante scripts personalizados escritos en JavaScript, facilitando escenarios complejos o específicos que no pueden manejarse con la validación estándar (`@check`). Actualmente, esta característica es experimental y no se recomienda utilizarla en entornos de producción.

Ejemplo básico de anotación con script:

```clra
ns User {
    relation owner = User::self @script{
        async main() {
            // Aquí puedes escribir JavaScript asíncrono para validaciones avanzadas.
        }
    }
};
```

#### Casos de uso para scripts

Los scripts son especialmente útiles en casos en los que:

* Se requieren validaciones dependientes de condiciones externas.
* Es necesario consultar información desde bases de datos externas o servicios API externos.
* Se debe actualizar dinámicamente el estado de namespaces o recursos.

#### Funcionamiento y precauciones

* **Naturaleza no determinista:** El uso de scripts rompe con el principio de validaciones deterministas, ya que su resultado puede variar dependiendo de factores externos, como respuestas de servicios remotos o cambios en otras bases de datos.
* **Rendimiento:** La ejecución de scripts es significativamente más lenta en comparación con las validaciones en `@check`, debido al tiempo que requiere iniciar y ejecutar código JavaScript dentro de una máquina virtual.
* **Gestión de estado:** MayaDB puede reutilizar la máquina virtual JavaScript para diferentes ejecuciones, lo que implica un riesgo de que los datos residuales de ejecuciones anteriores afecten validaciones posteriores. Por ello, es crucial asegurarse de que los scripts limpien o sobrescriban cualquier estado temporal para mantener la integridad y consistencia de los resultados.

#### Buenas prácticas

* **No almacenar datos persistentes en scripts:** Evita mantener cualquier estado temporal o datos permanentes en la ejecución del script para prevenir contaminación cruzada entre ejecuciones.
* **Limitación en el uso:** Reserva los scripts para escenarios específicos que requieren una lógica particularmente compleja o dependiente de recursos externos, y utiliza las anotaciones `@check` para validaciones regulares o deterministas.
* **Monitoreo y auditoría:** Debido a su naturaleza experimental, implementa monitoreo exhaustivo y auditorías regulares de cualquier uso de scripts, asegurando que no introduzcan vulnerabilidades o problemas de rendimiento inesperados en tu sistema.

#### Implementación de APIs (Próxima versión)

Hasta ahora, la anotación `@script` no dispone de una API pública para interactuar directamente con MayaDB ni realizar peticiones HTTP desde JavaScript. Esto significa que los scripts no pueden, en su estado actual, consultar ni modificar datos de la base de datos ni comunicarse con servicios externos. **A partir de MayaDB 0.2.0** se añadieron los helpers descritos en la sección “APIs JavaScript embebidas (beta)”, pero permanecen limitados a operaciones de lectura y no habilitan escritura ni llamadas HTTP externas.

En la siguiente versión de MayaDB se incluirán:

* **API REST**: Endpoints dedicados para invocar y gestionar la ejecución de scripts de validación de forma segura y controlada.
* **SDK JavaScript**: Un paquete cliente que expondrá métodos asincrónicos para:

  * Cargar y ejecutar scripts de validación.
  * Acceder a metadatos de entidades dentro de namespaces.
  * Realizar llamadas a servicios externos respetando las políticas de ejecución de MayaDB.

Estas nuevas APIs estarán diseñadas para integrarse de manera nativa con la anotación `@script`, permitiendo que el código JavaScript pueda:

1. Consultar metadatos de namespaces a través de llamadas asincrónicas.
2. Invocar endpoints internos para validar parte del flujo de autorización.
3. Realizar peticiones HTTP seguras hacia servicios externas, manteniendo aislamiento e integridad.

Mientras llegan estas funcionalidades, mantén los scripts limitados a validaciones puramente lógicas y planea la transición de las validaciones más complejas a las nuevas APIs cuando estén disponibles.


#### Definición de tipos (`json types`)

```clra
json types {
    name:  string required  default = "name";
    age:   number required;
    email: string required  default = "example@example.com" email_format;
}
```

* **name**  Cadena obligatoria. Valor por defecto `"name"`.
* **age**   Número obligatorio.
* **email** Cadena obligatoria en formato e‑mail. Valor por defecto `"example@example.com"`.

---

### Operaciones sobre entidades

Las entidades viven dentro de un *namespace* y se identifican por un ID único (`Namespace::ID`). MayaDB no está pensado para realizar consultas complejas; las operaciones son directas sobre una entidad completa.

#### Crear una entidad

```clra
ENTITY CREATE Video::videoID { name: "user123", age: 1 }
```

* **`ENTITY CREATE`**

  * `Video` → namespace
  * `videoID` → ID de la entidad
  * `{ … }` → metadatos iniciales

---

#### Leer una entidad

```clra
ENTITY GET Video::videoID
```

Devuelve todos los metadatos almacenados para la entidad. No admite filtros ni proyecciones.

---

#### Actualizar una entidad

```clra
ENTITY UPDATE Namespace::ID SET name = "Iron Man";
ENTITY UPDATE Namespace::ID SET age = 42, active = true;
```

La cláusula `SET` acepta:

| Tipo de operación                             | Ejemplo                              |
| --------------------------------------------- | ------------------------------------ |
| Asignación directa                            | `name = "Iron Man"`                  |
| Múltiples asignaciones                        | `age = 42, active = true`            |
| Incremento / decremento numérico              | `stats.score += -7.5`                |
| Operaciones aritméticas con expresiones       | `measure /= (sum.total - 3.14)`      |
| Manipulación de arrays                        | `inventory.items[3].qty -= 1`        |
| Appendix / prepend / pop / shift / remove     | `users[*].tags APPEND ["new","vip"]` |
| Asignación masiva con comodín (`*`)           | `*.status = "pending"`               |

> **Nota:** Las rutas tipo `matrix.rows[0].values`, rangos `[1:3]`, comodines `[*]` y operadores sobre listas (`POP`, `SHIFT`, `REMOVE`, etc.) permiten actualizaciones muy específicas dentro de estructuras JSON anidadas.

---

#### Eliminar una entidad

```clra
ENTITY DELETE Team::teamID
```

Borra por completo la entidad indicada. Al igual que con `GET`, hay que especificar el *namespace* y el ID de forma explícita.

---

#### Comandos

| Acción     | Sintaxis básica                     |
| ---------- | ----------------------------------- |
| Crear      | `ENTITY CREATE Namespace::ID { … }` |
| Leer       | `ENTITY GET    Namespace::ID`       |
| Actualizar | `ENTITY UPDATE Namespace::ID SET …` |
| Eliminar   | `ENTITY DELETE Namespace::ID`       |

Cada comando actúa sobre **una única entidad**; MayaDB no soporta búsquedas, filtros ni uniones entre entidades.


### Gestión de **Links**

Los *links* son bordes en el grafo de MayaDB: conectan entidades que viven en *namespaces* distintos y expresan la **relación** que existe entre ellas. Por diseño, un link:

* **Indica dirección** `Origen → relación → Destino`
* **Puede caducar**  TTL (Time‑to‑Live) opcional
* **No se edita**   Si la relación cambia, se borra y se crea de nuevo

Cuando MayaDB evalúa permisos (`LINK GET`), recorre estos bordes para deducir si un actor tiene derecho sobre un recurso. Las secciones siguientes explican cada operación con sintaxis, reglas y ejemplos completos.

---

#### Crear un link (`LINK CREATE`)

```clra
LINK CREATE User::Alice.user -> owner -> Group::Engineering WITH TTL "1d"
```

| Elemento             | Significado                                            |
| -------------------- | ------------------------------------------------------ |
| `User::Alice.user`   | **Origen** (namespace `User`, id `Alice`, tipo `user`) |
| `owner`              | **Relación** (nombre lógico definido en el esquema)    |
| `Group::Engineering` | **Destino** (namespace `Group`, id `Engineering`)      |
| `TTL "1d"`           | El link expira 24 h después de su creación             |

**Por qué usar TTL**
En vínculos temporales ―por ejemplo, acceso a un proyecto durante un *sprint*― basta con fijar la caducidad y olvidar limpiezas manuales; MayaDB invalidará el borde automáticamente.

> **Reglas de creación**
>
> * El par Origen‑Destino **ya debe existir**; no se crean entidades implícitas.
> * El nombre de la relación debe coincidir con el declarado en el esquema (`ns … { relation … }`).
> * El TTL se escribe en notación ISO‑8601 restringida (`"72h"`, `"30m"`, etc.) o como fecha absoluta (`"2025‑05‑20T12:00:00Z"`).

---

#### Actualizar un link

No está permitido. Para cambiar la relación:

1. `LINK DELETE …`
2. `LINK CREATE …` con los parámetros nuevos

Prohibir ediciones evita ciclos de vida incoherentes y simplifica la verificación de permisos (un link es siempre **atómico**: existe o no).

---

#### Eliminar un link (`LINK DELETE`)

```clra
LINK DELETE User::Alice.user -> owner -> Group::Engineering
```

Borra la arista que enlaza `Alice` con `Engineering` bajo la relación `owner`. Si el link había caducado, esta orden lo elimina igualmente (idempotente).

---

#### Listar links (`LINK LIST`)

```clra
LINK LIST FROM User::Alice.user
```

Devuelve **todas** las relaciones salientes desde `User::Alice.user` que sigan vigentes. No existen filtros por tipo de relación ni por destino; la intención es obtener el “panel de control” completo de la entidad origen.

---

#### Resolver permisos (`LINK GET`)

##### Concepto

`LINK GET` es la consulta de **autorización** en MayaDB. Busca un camino válido (orientado y no caducado) entre el origen y el destino a través de las relaciones declaradas, aplicando las reglas y las anotaciones `@check` que encuentre en cada salto.

##### Ejemplo completo

```clra
-- Construcción del grafo
LINK CREATE User::Alice.user           -> owner   -> Group::Engineering;
LINK CREATE Group::Engineering.owner   -> admin   -> Team::Platform;
LINK CREATE Team::Platform.admin       -> member  -> Project::Apollo;
LINK CREATE Project::Apollo.member     -> assignee -> Task::Deploy;

-- Consulta de permiso
LINK GET User::Alice.user -> assignee -> Task::Deploy
```

**Lectura paso a paso**

| Salto | Relación   | Se evalúa…                              | Resultado   |
| ----- | ---------- | --------------------------------------- | ----------- |
| 1     | `owner`    | ¿Existe link que no haya expirado?      | ✔️          |
| 2     | `admin`    | Idem + reglas `@check` en `Team::admin` | (ver abajo) |
| 3     | `member`   | …                                       | ✔️          |
| 4     | `assignee` | …                                       | ✔️          |

Si **todos** los eslabones dan positivo, la respuesta global es “Permitido”.

#### Evaluación de anotaciones `@check`

Esquema simplificado:

```clra
ns Team {
    relation admin = Group::owner @check{
        AllowIf: (::name == "team_name")
        DenyIf:  (::projects_count == 0)
    };
}
```

* MayaDB ejecuta el bloque `@check` **en el momento** de cruzar el borde.
* Las expresiones se evalúan sobre los metadatos de la entidad destino (`Team::Platform`).
* Si alguna regla `DenyIf` se cumple, el camino queda anulado y `LINK GET` devuelve *Denied*.

---

#### Buenas prácticas al modelar relaciones

1. **Nombrar las relaciones con semántica de permisos** (p.ej. `owner`, `admin`, `viewer`).
2. **Usar TTL para accesos acotados** (demostraciones, tareas puntuales).
3. **Aislar reglas de negocio en `@check`** en vez de hard‑codear lógica en la aplicación cliente.
4. **Mantener las entidades pequeñas**: los filtros `@check` se ejecutan sobre los metadatos; si éstos son livianos, la verificación es rápida.
5. **Registrar la versión del esquema** (`version: 1.1:alpha`) para trazar cambios en producción.

---

#### Resumen operativo

| Acción            | Comando                                | Notas clave                                 |
| ----------------- | -------------------------------------- | ------------------------------------------- |
| Crear link        | `LINK CREATE A -> rel -> B [WITH TTL]` | TTL opcional                                |
| Eliminar link     | `LINK DELETE A -> rel -> B`            | Idempotente                                 |
| Listar links      | `LINK LIST FROM A`                     | Sin filtros adicionales                     |
| Verificar permiso | `LINK GET A -> relFinal -> C`          | Recorre múltiple saltos con reglas `@check` |
| Cambiar relación  | `DELETE` → `CREATE`                    | Actualizar **no** está soportado            |

Con esta estructura podrás describir, inspeccionar y depurar la autorización basada en grafos de MayaDB de manera consistente y transparente.

---

## APIs JavaScript embebidas (beta)

Aunque la sección anterior mencionaba la ausencia de una API pública para scripts, desde **MayaDB 0.2.0** se expone un conjunto limitado de helper functions pensadas exclusivamente para lectura. El runtime sigue en fase **BETA**, por lo que la interfaz puede cambiar sin previo aviso y no se garantiza compatibilidad hacia atrás.

### Funciones disponibles

| Helper                              | Parámetros (JSON/string)                                                                 | Resultado                                          |
|--------------------------------------|-------------------------------------------------------------------------------------------|----------------------------------------------------|
| `await fetchKey(key)`                | Cadena con la clave LMDB exacta.                                                          | Cadena con el contenido bruto.                     |
| `await fetchLinkForward(payload)`    | JSON serializado con `db`, `version`, `code`, `from_namespace`, `from_entity`, `from_role`, `to_namespace`, `to_entity`, `relation`.| JSON string con TTL (`ttl`), `from`, `to`, `relation`. |
| `await fetchEntityData(payload)`     | JSON con `db`, `version`, `code`, `namespace`, `entity`.                                 | JSON string con los atributos almacenados.         |

Ejemplo de uso dentro de `@script` (recordar que el script debe exportar `async function main()`):

```javascript
async function main() {
  const entity = JSON.parse(await fetchEntityData(JSON.stringify({
    db: "demo",
    version: "1",
    code: "alpha",
    namespace: "User",
    entity: "alice"
  })));

  if (entity.status !== "active") {
    return { authorized: false, value: { reason: "inactive" } };
  }

  const link = JSON.parse(await fetchLinkForward(JSON.stringify({
    db: "demo",
    version: "1",
    code: "alpha",
    from_namespace: "User",
    from_entity: "alice",
    from_role: "owner",
    to_namespace: "Group",
    to_entity: "engineering",
    relation: "member"
  })));

  return { authorized: true, value: { entity, link } };
}
```

### Consideraciones y limitaciones

- **Solo lectura**: actualmente no hay helpers para crear, actualizar o eliminar datos desde JS.
- **Errores propagados**: si se consulta una clave inexistente, se recibe un error JavaScript (capturable con `try/catch`).
- **Estado compartido**: el motor puede reciclar instancias; evita almacenar datos en variables globales.
- **Rendimiento**: cada helper ejecuta operaciones LMDB y serializaciones JSON; úsalos con moderación.

> **Importante**: debido a que el runtime JS continúa en beta, se recomienda limitar su uso a prototipos o decoradores ligeros y mantener la lógica principal en `@check` o en la aplicación cliente.
