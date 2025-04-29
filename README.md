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

El proyecto busca resolver la ineficiencia en la gestión académica que se presenta en algunas instituciones, donde aún se utilizan métodos poco prácticos como hojas de Excel para llevar el control de estudiantes, docentes, materias y carreras. A través de una aplicación web conectada a una API, se propone automatizar y dinamizar la administración de estos datos, ofreciendo una solución centralizada, segura y con validaciones integradas.

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

1. Abrir SQL Server Management Studio y conectar al servidor.
2. En el panel izquierdo, hacer clic derecho en *Databases* > *New Database*.  
3. Asignar un nombre a la base de datos y presionar *Add*.

#### 🔑 Comandos clave en SQL

sql
-- Crear tabla
CREATE TABLE Estudiantes (
    Id VARCHAR(10) PRIMARY KEY,
    Nombre VARCHAR(50),
    Apellido VARCHAR(50),
    FechaNacimiento DATE,
    Email VARCHAR(100),
    Direccion VARCHAR(100),
    Telefono VARCHAR(15),
    CarreraId VARCHAR(10)
);

-- Insertar registros
INSERT INTO Estudiantes (Id, Nombre, Apellido)
VALUES ('1234567890', 'Juan', 'Pérez');

-- Consulta general
SELECT * FROM Estudiantes;

-- Actualizar datos
UPDATE Estudiantes
SET Nombre = 'Carlos'
WHERE Id = '1234567890';

-- Eliminar datos
DELETE FROM Estudiantes
WHERE Id = '1234567890';

-- Eliminar tabla
DROP TABLE Estudiantes;

-- Eliminar base de datos
DROP DATABASE SistemaGestionEstudiantes;


- Estas consultas o comando son en general lo más comunes en consultas o manejo en sql server (SSMS).

## 🧩 API y conexión a la base de datos

### Conexión:
Para conectar la base de datos al proyecto API, se debe configurar la cadena de conexión en el archivo appsettings.json.
### Plantilla:
sql
{
    "Logging": {
        "LogLevel": {
            "Default": "Information",
            "Microsoft.AspNetCore": "Warning"
        }
    },
    "AllowedHosts": "*",
    "ConnectionStrings": {
        "Connection": "Data Source=SERVIDOR_SQL;Initial Catalog=SistemaGestionEstudiantes;Integrated Security=True;TrustServerCertificate=True"
    }
}

Controladores para el SQL
Para el proyecto se utilizaron controladores MVC en blanco, que gestionan el envío y la recepción de datos entre la base de datos y la interfaz web. Se implementaron validaciones en los controladores para evitar errores comunes como duplicación de datos o ingreso inválido.

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
}

IConfiguration: se usa para acceder a la cadena de conexión en el appsettings.json.
## Métodos HTTP que maneja un controlador
GET: Recupera datos (ej. obtener lista de estudiantes).

POST: Inserta nuevos datos (ej. registrar nuevo curso).

PUT: Actualiza un registro existente.

DELETE: Elimina un registro por ID.

## Models API
En la carpeta Models se definen las estructuras que representan cada entidad (Estudiantes, Profesores, Cursos, Carreras). Estas clases permiten mapear los datos entre la base de datos, el backend y el frontend.

public class Estudiante {
    public string Id { get; set; }
    public string Nombre { get; set; } 
    public string Apellido { get; set; }
    public DateTime FechaNacimiento { get; set; }
    public string Email { get; set; }
    public string Direccion { get; set; }
    public string Telefono { get; set; }
    public string CarreraId { get; set; }
}

## Interfaz de Usuario
La interfaz fue construida con HTML, CSS y JavaScript. Incluye:

Menú lateral con navegación por secciones (Estudiantes, Profesores, Cursos).

Formularios dinámicos que se conectan con la API.

Tablas interactivas con opciones de edición y eliminación.

Estilo moderno y responsive para distintos dispositivos.

## Resultados
El sistema permite realizar todas las operaciones CRUD para las entidades académicas, con validaciones, carga dinámica de datos y diseño intuitivo. Se logra un flujo eficiente de información y se mejora la experiencia del usuario y la administración académica.
