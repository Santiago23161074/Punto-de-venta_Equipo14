# Punto-de-venta_Equipo14
Un punto de venta en el cual usamos una base de datos, implementado en el entorno de MySQL Workbench, y usando 100% el lenguaje de java, usado en Netbeans


# 🛒 Sistema de Gestión de Ventas - Java Swing

Este proyecto es una aplicación de escritorio desarrollada en Java usando la biblioteca **Swing**, orientada a la gestión de ventas y administración de productos, clientes, proveedores y personal. Ha sido diseñado para facilitar el control y operación de una pequeña empresa comercial.

---

## 📘 Introducción

Esta aplicación ofrece un sistema de autenticación de usuarios, recuperación de contraseña por correo, administración de productos, clientes, proveedores y la realización de ventas a través de un carrito. Utiliza una arquitectura modular dividida en **vista** y **conexión**, facilitando el mantenimiento y ampliación del sistema.

---

## ⚙️ Características principales

| Funcionalidad               | Descripción |
|----------------------------|-------------|
| 👤 Autenticación            | Inicio de sesión con validación y recuperación de contraseña. |
| 📝 Registro de usuarios     | Interfaz para registro de nuevos usuarios. |
| 📦 Gestión de productos     | Alta, baja y modificación de productos. |
| 🧾 Carrito de compras       | Simulación de compras con resumen final. |
| 🧍 Gestión de personal      | Control de empleados desde la interfaz. |
| 👥 Gestión de clientes      | Registro y administración de clientes. |
| 🚚 Gestión de proveedores   | Interfaz para administración de proveedores. |
| 📧 Envío de correos         | Sistema de recuperación mediante correo electrónico. |
| 💾 Conexión con base de datos | Manejada por múltiples clases especializadas. |

---

## 🧱 Estructura del Proyecto

```plaintext
Prueba_Proyecto/
│
├── src/
│   ├── Conexion/
│   │   ├── Conexion_Base.java
│   │   ├── Conexion_Clientes.java
│   │   ├── Conexion_Personal.java
│   │   ├── Conexion_Producto.java
│   │   ├── Conexion_Proveedor.java
│   │   ├── Conexion_Ventas.java
│   │   ├── Correo_Creado.java
│   │   ├── Validacion.java
│   │   └── Prueba.java
│   │
│   └── Vista/
│       ├── Login.java
│       ├── Registro.java
│       ├── Recuperar_Contraseña.java
│       ├── SistemaPrueba.java
│       └── Carrito.java
│
├── build.xml                # Script de construcción con Apache Ant
├── manifest.mf             # Manifest para empaquetado JAR
└── build/                  # Carpeta de compilación
```

---

## 🚀 Cómo ejecutar el proyecto

### Prerrequisitos

- Java JDK 8 o superior
- Apache Ant (opcional, para compilar con `build.xml`)
- IDE recomendado: NetBeans

### Pasos

```bash
1. Clona o descomprime este repositorio.
2. Abre NetBeans y selecciona "Abrir Proyecto".
3. Ejecuta el archivo `SistemaPrueba.java` o compila con Ant.
4. Asegúrate de configurar correctamente la conexión a la base de datos.
```

---

## 🖼️ Interfaz Gráfica (Vista esperada)

Aunque no se incluyen capturas, la interfaz está construida con `Java Swing`, y contiene:

- Formularios para login y registro.
- Ventanas de administración de clientes, productos y ventas.
- Tabla con productos seleccionados para simular compras (Carrito).
- Ventana de recuperación de contraseña vía correo electrónico.

---

## 🧩 Dependencias

| Componente      | Uso                                |
|----------------|-------------------------------------|
| Java Swing      | Construcción de interfaces gráficas |
| JavaMail (posible) | Envío de correos electrónicos     |
| JDBC            | Conexión con base de datos          |

---

## 👨‍💻 Autores

- 📌 **Desarrollador Principal:** *[Tu nombre aquí]*  
- 🛠️ Proyecto académico / prototipo funcional

---

## 📜 Licencia

Este proyecto está bajo la licencia MIT. Puedes usarlo, modificarlo y distribuirlo libremente, dando crédito al autor original.

---

¡Gracias por visitar este proyecto! 😊

