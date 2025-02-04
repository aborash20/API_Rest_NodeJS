# **Documento Técnico de la API REST - Gestión de Clientes**

## **Resumen del Proyecto**

Esta API REST está diseñada para gestionar la información de clientes, permitiendo realizar operaciones básicas como agregar, listar y obtener estadísticas sobre los mismos. La información de los clientes se guarda temporalmente en un archivo JSON. 

## **Tecnologías Utilizadas**

- **Node.js**: Entorno de ejecución para JavaScript.
- **Express.js**: Framework para Node.js para la creación de aplicaciones web.
- **JSON**: Utilizado como sistema de almacenamiento temporal para los datos.
- **Git**: Control de versiones utilizado para el desarrollo del proyecto.

## **Requisitos Previos**

Para ejecutar este proyecto, necesitas tener instalados los siguientes programas:

- **Node.js**: Puedes descargarlo desde [aquí](https://nodejs.org/).
- **Git**: Puedes instalarlo desde [aquí](https://git-scm.com/).

## **Estructura del Proyecto**

La estructura del proyecto es la siguiente:

```
api-clientes/
│
├── data/
│   └── clientes.json   # Almacenará los datos de los clientes
│
├── src/
│   ├── controllers/
│   │   └── clientesController.js  # Lógica de los servicios de la API
│   ├── routes/
│   │   └── clientesRoutes.js     # Rutas de la API
│   ├── app.js          # Configuración del servidor Express
│   └── repository.js   # Manejo de lectura y escritura de datos (clientes.json)
├── .gitignore          # Archivos a ser ignorados por Git
└── package.json        # Configuración de dependencias y scripts
```

### **Descripción de Archivos**

1. **`src/app.js`**: Es el archivo principal que configura el servidor Express. Aquí se definen las rutas y los middlewares.
2. **`src/repository.js`**: Contiene funciones para leer y escribir datos en el archivo `clientes.json`, el cual simula una base de datos.
3. **`src/controllers/clientesController.js`**: Contiene la lógica de los servicios, como la creación de un cliente, listado de clientes, ordenación, y estadísticas.
4. **`src/routes/clientesRoutes.js`**: Define las rutas de la API y las asocia a los controladores correspondientes.
5. **`data/clientes.json`**: Contiene la información de los clientes en formato JSON.

## **Servicios de la API**

### **1. Crear un Cliente**

- **Método**: `POST`
- **Ruta**: `/clientes`
- **Descripción**: Permite crear un nuevo cliente con los datos proporcionados.
- **Cuerpo de la solicitud**:
  ```json
  {
    "nombre": "Juan Pérez",
    "documento": "12345678",
    "correo": "juan@example.com",
    "fechaNacimiento": "1990-05-15",
    "zonaHoraria": "GMT-3"
  }
  ```
- **Respuesta**:
  - **Código 201**: Si el cliente fue creado correctamente.
  - **Código 400**: Si faltan datos requeridos.

### **2. Listar Clientes Ordenados Alfabéticamente**

- **Método**: `GET`
- **Ruta**: `/clientes/alfabeticamente`
- **Descripción**: Retorna la lista de clientes ordenada alfabéticamente por nombre.
- **Respuesta**:
  ```json
  [
    {
      "nombre": "Ana Martínez",
      "documento": "23456789",
      "correo": "ana@example.com",
      "fechaNacimiento": "1985-03-12",
      "zonaHoraria": "GMT-3"
    },
    {
      "nombre": "Juan Pérez",
      "documento": "12345678",
      "correo": "juan@example.com",
      "fechaNacimiento": "1990-05-15",
      "zonaHoraria": "GMT-3"
    }
  ]
  ```

### **3. Listar Clientes Ordenados por Edad**

- **Método**: `GET`
- **Ruta**: `/clientes/edad`
- **Descripción**: Retorna la lista de clientes ordenada por edad (de menor a mayor).
- **Respuesta**:
  ```json
  [
    {
      "nombre": "Juan Pérez",
      "edad": 34
    },
    {
      "nombre": "Ana Martínez",
      "edad": 39
    }
  ]
  ```

### **4. Obtener Estadísticas de Clientes**

- **Método**: `GET`
- **Ruta**: `/clientes/estadisticas`
- **Descripción**: Retorna la cantidad total de clientes y el promedio de edad de todos los clientes.
- **Respuesta**:
  ```json
  {
    "cantidad": 2,
    "promedioEdad": 36.5
  }
  ```

## **Manejo de Datos (Archivo JSON)**

Los datos de los clientes se almacenan de forma temporal en el archivo `data/clientes.json`. Cada vez que un cliente es creado, los datos se agregan a este archivo. Los servicios de listado y estadísticas leen directamente este archivo.

El archivo tiene el siguiente formato:

```json
[
  {
    "nombre": "Juan Pérez",
    "documento": "12345678",
    "correo": "juan@example.com",
    "fechaNacimiento": "1990-05-15",
    "zonaHoraria": "GMT-3"
  },
  {
    "nombre": "Ana Martínez",
    "documento": "23456789",
    "correo": "ana@example.com",
    "fechaNacimiento": "1985-03-12",
    "zonaHoraria": "GMT-3"
  }
]
```

## **Flujo de Trabajo con Git**

1. **Creación del Repositorio**:
   - Se inicializa el repositorio con `git init` y se realiza el primer commit con los archivos base del proyecto.

2. **Implementación de los Servicios**:
   - Se desarrollan los primeros tres servicios en la rama principal (`main`).
   - Se hace un commit y se sube el código a la rama `main` con:
     ```bash
     git add .
     git commit -m "Primeros tres servicios implementados"
     git push origin main
     ```

3. **Rama `clientes-promedio`**:
   - Se crea una nueva rama `clientes-promedio` para agregar el servicio de estadísticas.
   - Se implementa el servicio y se hace commit.
   - Finalmente, se realiza un `merge` de la rama `clientes-promedio` a `main`:
     ```bash
     git checkout main
     git merge clientes-promedio
     ```

## **Cómo Ejecutar el Proyecto**

1. **Clonar el Repositorio**:
   ```bash
   git clone https://github.com/tu_usuario/api-clientes.git
   cd api-clientes
   ```

2. **Instalar Dependencias**:
   ```bash
   npm install
   ```

3. **Ejecutar el Servidor**:
   ```bash
   node src/app.js
   ```

El servidor estará corriendo en `http://localhost:3000`.

## **Conclusión**

Este proyecto implementa una API REST simple para gestionar clientes, permitiendo realizar operaciones de creación, ordenación, y estadísticas. Los datos se almacenan temporalmente en un archivo JSON, lo que lo hace adecuado para pruebas o proyectos pequeños. El uso de Git y ramas permite organizar el flujo de trabajo y la implementación de nuevas funcionalidades de forma ordenada.

---

Este documento puede servir como base para la comprensión del proyecto y facilitar su ejecución o ampliación en el futuro.
