# Punto-de-venta_Equipo14
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

## Paquete de coneccciones

#🔌Clase Conexion_Base.java
La clase Conexion_Base es el núcleo de acceso a la base de datos. Proporciona métodos esenciales para establecer y cerrar la conexión con un servidor MySQL. Esta clase es fundamental para que las demás clases que interactúan con la base de datos puedan funcionar correctamente.

#🧠 Propósito
Permitir la conexión y desconexión al sistema gestor de base de datos MySQL usando JDBC (Java Database Connectivity). Es utilizada como base para que otras clases de conexión accedan al mismo punto centralizado de configuración.

