# 🎓 Proyecto Gestor Académico
Autores:  
- Calero Villarreal Jonathan Christian  
- Doicela Pingos Bryan Stalin  
- Méndez Clavijo Carlos Manuel  
- Peña Bastidas Natasha Naomi  

Universidad Técnica de Ambato  
Av. Los Chasquis y Río Payamino  
📧 decanato.fcial@uta.edu.ec

## 📄 Resumen

Este documento presenta la implementación de una API para la conexión a una página web en C# (Visual Studio 2022 y Visual Studio Code), como parte del desarrollo de un proyecto de Programación Avanzada. Se aplican conceptos clave como la conexión a una base de datos, diseño de páginas web con HTML, scripts y CSS, optimizando el uso y desempeño de una aplicación web para la gestión académica.

## 🧾 Abstract

This document presents the implementation of an API for connecting to a webpage in C# (Visual Studio 2022 and Visual Studio Code) as part of an advanced programming implementation topic. Key concepts such as database connection, creating and designing a webpage with Visual Studio Code using HTML, scripts, and CSS are covered to optimize the use and performance of the web application.

---
## 📌 Introducción

El manejo de una API en programación avanzada permite la conexión de datos a una base de datos, facilitando la gestión de información en aplicaciones como páginas web. En este informe se describen funcionalidades como operaciones CRUD, consultas SQL y diseño web con HTML y CSS.

---

## 🎯 Objetivo General

Crear una aplicación web con métodos de consulta SQL y conectarla mediante una API a una página web.

### ✅ Objetivos Específicos

- Aplicar los conocimientos obtenidos en clases para el desarrollo.
- Implementar estructuras de búsqueda SQL.
- Manejar validaciones y excepciones para evitar errores en las conexiones y consultas.
- Diseñar la página web utilizando Visual Studio Code.

---

## 🛠️ Metodología

### 1. Desarrollo

#### 📌 Base de datos en SQL Server  

Para crear la base de datos en SQL Server:


1. Abrir SQL Server Management Studio y debemos conectar a la base de datos
2. En el panel izquierdo, hacer clic derecho en **Databases** > **New Database**.  
3. Asignar un nombre a la base de datos y presionar **Add**.
 

#### 🔑 Comandos clave en SQL

📌Nota: En esta parte vamos a ver los principales comandos en base a sql y su estructuración ya que tomamos en base a esto todas las demás tablas y consultas que se podrán dar.

```sql
-- Crear tabla
CREATE TABLE Estudiantes (
    Id INT PRIMARY KEY,
    Nombre NVARCHAR(50),
    Apellido NVARCHAR(50)
);

-- Insertar registros
INSERT INTO Estudiantes (Id, Nombre, Apellido)
VALUES (1, 'Juan', 'Pérez');

-- Consulta general
SELECT * FROM Estudiantes;

-- Actualizar datos
UPDATE Estudiantes
SET Nombre = 'Carlos'
WHERE Id = 1;

-- Eliminar datos
DELETE FROM Estudiantes
WHERE Id = 1;

-- Eliminar tabla
DROP TABLE Estudiantes;

-- Eliminar base de datos
DROP DATABASE SistemaGestionEstudiantes;

```
- Estas consultas o comando son en general lo más comunes en consultas o manejo en sql server (SSMS).

## 🧩 API y conexión a la base de datos

### Conexión:
Para realizar la conexión de la base de datos correspondientes debemos tener en cuenta el nombre del sql server, que fue asignada al proceso de la instalación. Lo definimos y agregamos el acceso al archivo .json.
### Plantilla:
```sql
{
    "Logging": {
        "LogLevel": {
            "Default": "Information",
            "Microsoft.AspNetCore": "Warning"
        }
    },
    "AllowedHosts": "*",
    "ConnectionStrings": {
        "Connection": "Data Source=”Nombre del usuario en sql server”;Initial Catalog=SistemaGestionEstudiantes;Integrated Security=True;TrustServerCertificate=True"
    }
}

```
## 🕹️ Controladores para el sql

Para el proyecto usamos un controlador mvc en blanco, es un componente dentro del patrón de arquitectura Modelo-Vista-Controlador, que, al crearse, no tiene ninguna lógica o funcionalidad definida.
Para el manejo correcto de los datos en sql en la inserción de un nuevo dato, usamos validaciones y excepciones.

### Plantilla:

```sql
namespace GestionCursosAPI.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class EstudiantesController : ControllerBase {
        private readonly IConfiguration _configuration;

        public EstudiantesController(IConfiguration configuration) {
            _configuration = configuration;
        }
}
```
- IConfiguration: se usa para la cadena de conexión en el json.

## 🌐 Métodos HTTP que maneja un controlador:
### GET :
Sirve para consultar o recuperar información.
### POST:
Se usa para crear nuevos recursos.
### PUT:
Sirve para actualizar completamente un recurso existente.
### DELETE: 
Se utiliza para eliminar un recurso existente.

## 📝	Models API
En la carpeta se define las propiedades de cada sección de nuestro gestor académico.

### Plantilla:
```sql
public class NombreDeLaClase {
    public int Id { get; set; }
    public string Nombre { get; set; } 
    public string Apellido { get; set; }  ….
}
```
---
## 🎨Diseño General (HTML Y CSS)

-	El HTML crea la estructura visual: títulos, menús, formularios, tablas, etc.
-	Usa un menú lateral con íconos (📚, 👨‍🏫, etc.) que permite cambiar entre secciones
  
## 💡Lógica con JavaScript
Este es el núcleo del sistema y se encarga de:

### 🧑‍💻 Cambiar entre secciones del sistema

Funciones como showStudents(), showProfessors() ocultan todas las secciones y muestran solo la que corresponde.  Esta acción se realiza para cada campo que conforma toda esta gestión. 

### Plantilla:
```sql
function show_NombreAtributo() {
  hideAllSections();
  document.getElementById("Nombre_de_lista-list").style.display = "block";
  fetchNombreAtributo();  Llamada genérica que deberías reemplazar por la función correspondiente
}
```
## 🧷 Conexion con API
Se realiza la conexión con una página web con una API REST para recibir datos desde el servidor y usarlos en el navegador. 
Ejemplos como este conectan con la API REST (https://localhost:7198/api/...) para obtener o enviar información. 

### Plantilla:
```sql
fetch("https://localhost:7198/api/.....")
  .then(response => response.json())
  .then(data => {
    // mostrar los datos en la tabla
  });
```
## 🔍 Manejo de formularios
Este código se encarga de gestionar el envío de un formulario en una página web sin recargar la página. En la cual al revisar el formulario nos ayuda a prevenir el comportamiento por defecto del navegador, además de capturar los datos ingresados por el usuario en las cuales se envían los datos al servidor utilizando fetch() con una solicitud HTTP POST al endpoint de una API para después de que los datos se envíen correctamente con la función fetch_Nombre_De_Objeto para la actualización de la lista a mostrar en pantalla. 
Cada sección tiene un formulario. 
Por ejemplo:
```sql
<form id="studentForm">
  <input type="text" id="nombre" required>
  <input type="text" id="apellido" required>
  <button type="submit">Guardar</button>
</form>

------ Y su lógica asociada es:

document.getElementById("studentForm").addEventListener("submit", function (event) {
  event.preventDefault();
  const data = {
    nombre: document.getElementById("nombre").value,
    apellido: document.getElementById("apellido").value
  };

  fetch("https://localhost:7198/api/estudiantes", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data)
  }).then(() => {
    fetchStudents(); // recarga la lista
    this.reset(); // limpia el formulario
  });
});
```
## 🚀 Gestión Dinámica de Estudiantes, Materias y Profesores
Forma parte del sistema de gestión académica y permite cargar dinámicamente información en formularios según selecciones previas del usuario.

### Plantilla:
```sql
function cargar_NombreFormulario(Id_Formulario2) {
fetch(`https://localhost:7198/api/Nombre_Formulario1/Nombre_Formulario2/${Id_Formulario2}`)
    .then(response => response.json())
    .then(Nombre_Formulario1 => {
      const selectElement = document.getElementById("Nombre_Formulario1");
      selectElement.innerHTML = "<option value=''>-- Selecciona una opción --</option>";

      Nombre_Formulario1.forEach(item => {
        const option = document.createElement("option");
        option.value = item.id;
        option.textContent = item.nombre;
        selectElement.appendChild(option);
      });
    })
    .catch(error => console.log("Error al obtener Nombre_Formulario1:", error));
}
```
### Reemplazar:
- NombreFormulario por el nombre de tu función.
- Nombre_Formulario1 por el nombre de la entidad que se va a llenar (por ejemplo, estudiante, materia...).
- Nombre_Formulario2 por el filtro usado (como carrera, semestre...).
- Id_Formulario2 por el ID que usarás como parámetro.

📌 NOTA:  Asegúrate de que el campo item.nombre y item.id coincidan con la estructura real del JSON que devuelve tu API.

---
## 📋 Módulo de Gestion de Cursos

En este apartado nos permitira al usuario gestionar cursos academicoa a través de una interfaz dinamica que se comunica con una API REST.

### Funcionalidades

- ✅ Crear nuevos cursos mediante un formulario.
- 📋 Mostrar todos los cursos en una tabla.
- ✏️ Editar cursos directamente en la tabla.
- ❌ Eliminar cursos con confirmación.

### 🛠️ Descripcion Técnica

- Se utiliza `fetch()` para realizar peticiones `POST`, `GET`, `PUT` y `DELETE` hacia `/api/cursos`.
- La tabla se actualiza automáticamente tras cada operación gracias a la función `cargarCursos()`.
- Al editar un curso, se intercambian dinámicamente elementos `span` e `input` para facilitar la edición en línea.
- Mensajes visuales indican el éxito o error de las operaciones.

## 📋 Módulo de Gestion de Estudiantes

Nos permite listar, editar, eliminar y filtrar estudiantes desde una interfaz web, comunicándose con una API REST.

### Funcionalidades

- 📋 Listar estudiantes en una tabla dinámica con sus datos personales y la carrera asociada.
- ✏️ Editar estudiantes en línea, incluyendo datos como:
  - Nombre y apellido
  - Fecha de nacimiento
  - Email, dirección y teléfono
  - Carrera asociada
    
- ✏️ Editar estudiantes, ya sea desde la tabla (modo en línea) o cargando los datos en el formulario para modificarlos.
- ❌ Eliminar estudiantes con confirmación.
- 🔍 Filtrar estudiantes por carrera usando un selector desplegable
- 🔄 Actualización automática de la tabla tras cada operación.
- 📥 Cargar carreras desde el backend para el formulario de registro de estudiantes.
  
### 🛠️ Detalles Técnicos:

- Se utiliza fetch() para realizar peticiones HTTP:
   - GET para obtener estudiantes.
   - POST para registrar uno nuevo.
   - PUT para actualizar datos.
   - DELETE para eliminar por ID.

- Las carreras se gestionan mediante un arreglo auxiliar (carreras) que enlaza carreraId con el nombre mostrado.
-  La función `cargarCarrerasFormulario()` se encarga de obtener las carreras disponibles y llenar el `<select>` correspondiente en el formulario.
- Al editar desde la tabla, los span se reemplazan por input y select, y se muestran botones de "Guardar" y "Cancelar".
- Las fechas de nacimiento se formatean en estilo DD/MM/AAAA con toLocaleDateString.
- Incluye manejo de errores con alertas y mensajes personalizados para mejorar la experiencia del usuario.

## 📋 Módulo de Gestion de Docentes

Nos permite listar, editar, eliminar y filtrar profesores desde una interfaz web, comunicándose con una API REST.

### Funcionalidades

- ➕ Registrar profesores mediante un formulario con los siguientes campos:
   - Nombre y apellido
   - Fecha de nacimiento
   - Email, dirección y teléfono
- 📋 Listar todos los profesores en una tabla dinámica.
- ✏️ Editar profesores en línea desde la tabla, con opción de cancelar o guardar cambios.
- ❌ Eliminar profesores con confirmación de seguridad.
- 🔄 Actualización automática de la tabla luego de cualquier acción.
  
### 🛠️ Detalles Técnicos:

- Se usa fetch() para interactuar con el endpoint /api/profesores mediante:
   - GET para obtener la lista.
   - POST para registrar un nuevo profesor.
   - PUT para editar un profesor existente.
   - DELETE para eliminar por ID.

- Cada fila de la tabla contiene botones que cambian entre modo visual y modo edición.
- Los campos visuales (span) se convierten en campos editables (input) al activar la edición.
- La fecha de nacimiento se presenta en formato local (DD/MM/AAAA) usando toLocaleDateString().
- Las acciones se reflejan automáticamente en la tabla gracias a la función obtenerProfesores() que recarga la información.

## 📋 Módulo de Asignación de Materias a Carreras y Profesores

Permite asignar materias a carreras específicas junto a un profesor responsable.

### Funcionalidades

- ➕ **Asignar materias a carreras** indicando:
  - La carrera
  - La materia
  - El profesor encargado
  - El semestre correspondiente
- 📋 **Listar todas las asignaciones** en una tabla con nombres de referencia (carrera, materia y profesor).
- ❌ **Eliminar asignaciones existentes** con confirmación.
- 🔄 **Recarga automática** de la tabla luego de registrar o eliminar una asignación.

### 🛠️ Detalles técnicos:
- Utiliza `fetch()` para acceder a los siguientes endpoints:
  - `GET /api/MatriculaCarrera`: lista todas las asignaciones.
  - `POST /api/MatriculaCarrera`: crea una nueva asignación.
  - `DELETE /api/MatriculaCarrera/{id}`: elimina una asignación.
- Al cargar la tabla, se hace una consulta paralela (`Promise.all`) a:
  - `/api/Carreras` para obtener nombres de carreras.
  - `/api/Cursos` para obtener nombres de materias.
  - `/api/Profesores` para mostrar nombres completos de los docentes.
- Los formularios desplegables se rellenan automáticamente con las opciones disponibles.
- Los datos son renderizados dinámicamente en el `tbody` de una tabla HTML con botones de acción por fila.

## 🧾 Módulo de Matrícula de Estudiantes

En este espacio nos permite realizar la matrícula de estudiantes en materias específicas según su carrera, semestre y el profesor asignado. Todo el proceso es interactivo y se realiza con validación y carga dinámica desde la API.

### Funcionalidades clave:

- 🔄 **Carga dinámica de carreras** desde `/api/matricula/carreraMatricula`.
- 🎓 **Filtrado automático de estudiantes** por carrera.
- 📘 **Filtrado de materias** según carrera y semestre.
- 👨‍🏫 **Filtrado de profesores** por carrera, semestre y materia.
- ⏰ **Selección de horario y fecha** de matrícula.
- 📥 **Registro de matrícula** al hacer submit en el formulario:
  - Valida los campos.
  - Consulta el ID de `materiaPorCarrera`.
  - Envía los datos al endpoint `POST /api/Matricula`.
  - Muestra mensajes de éxito o error al usuario.

### 🛠️ Detalle técnico:
1. Al seleccionar una **carrera**, se filtran los estudiantes, materias y profesores disponibles.
2. Al cambiar el **semestre**, se actualizan las materias y profesores.
3. Al elegir una **materia**, se filtran los profesores disponibles.
4. El formulario final recoge:
   - Estudiante
   - Carrera
   - Semestre
   - Materia
   - Profesor
   - Horario
   - Fecha
5. El sistema consulta el ID exacto de `materiaPorCarrera` y, si existe, registra la matrícula.

✅ Este módulo asegura una matrícula precisa, dinámica y validada en todo momento.

---
## 🎨 Estilos (styles.css)
Define el diseño visual de la interfaz del sistema web de gestion academico. Presenta una apariencia moderna y oscura, con detalles en colores brillantes para destacar elementos claves.

### 🖌️ Diseño General
Fondo con **degradado lineal** en tonos oscuros (`#0f2027`, `#203a43`, `#2c5364`) para dar una estética profesional.
- Tipografía sencilla (`sans-serif`) y colores blancos para buen contraste y legibilidad.
- Distribución de componentes en **diseño horizontal** mediante `flex`, alineando `sidebar` y `main-content`.

### 🧑‍🎨 Sidebar (Barra lateral)
- Fondo sólido en color `#111827`.
- Ancho reducido a `130px` para una apariencia compacta.
- Menú vertical con enlaces destacados en color `#f43f5e`.

### 🖌️ Contenido Principal
- Fondo `#1e293b`, con secciones como `students-list`, `professors-list` y `courses-list` estilizadas en `#2d3748`.
- Espaciado cómodo mediante `padding` y esquinas redondeadas (`border-radius: 8px`).

### 🧱 Tablas
- Estilo personalizado para encabezados (`th`) y celdas (`td`) con tonos oscuros (`#374151`) y texto blanco.
- Diseño limpio con `border-collapse` y buen espaciado interno (`padding: 10px`).

### 🔲Botones
- Estilos diferenciados para cada tipo de acción:
  - `edit-btn`: color rosa (`#f43f5e`).
  - `delete-btn`: color rojo (`#ef4444`).
  - `new-btn`: color verde (`#10b981`), con texto en blanco y fuente en **negrita**.

📄 Este archivo CSS permite que la aplicación tenga una apariencia moderna, profesional y visualmente atractiva.
