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

# Paquete de coneccciones

## 🔌Clase Conexion_Base.java
La clase Conexion_Base es el núcleo de acceso a la base de datos. Proporciona métodos esenciales para establecer y cerrar la conexión con un servidor MySQL. Esta clase es fundamental para que las demás clases que interactúan con la base de datos puedan funcionar correctamente.

🧠 Propósito
Permitir la conexión y desconexión al sistema gestor de base de datos MySQL usando JDBC (Java Database Connectivity). Es utilizada como base para que otras clases de conexión accedan al mismo punto centralizado de configuración.

# 🧱 Estructura de la Clase

| 🧩 Atributo               | Descripción |
|----------------------------|-------------|
| bd           | Nombre de la base de datos a la que se conectará (proyecto_tap_14).|
| url     | Dirección del servidor MySQL (localhost en el puerto 3306). |
| user   |Usuario con permisos para acceder a la base de datos (root). |
| password     | Contraseña del usuario (⚠️ sensible).
| driver     | Driver JDBC de MySQL (com.mysql.cj.jdbc.Driver). |
| cx     | Objeto de tipo Connection para manejar la conexión actual.|

# 🔧 Métodos Públicos

| 🧩 Método               | Descripción |
|----------------------------|-------------|
| Conectar()           | 	Carga el driver JDBC, y establece una conexión con la base de datos.|
| Desconectar()     | Cierra la conexión activa si está abierta. |

---

# 👥 Clase `Conexion_Clientes.java`

La clase `Conexion_Clientes` se encarga de **gestionar operaciones CRUD (Crear, Leer, Actualizar y Eliminar)** sobre la tabla `clientes` de la base de datos. Utiliza la clase `Conexion_Base` para establecer la conexión y ejecuta consultas SQL mediante `PreparedStatement`.


---

## 🧠 Propósito

Permitir la interacción directa entre la aplicación Java y la tabla `clientes` de una base de datos MySQL. Ofrece métodos para:

- 📋 Listar clientes
- ➕ Insertar nuevos registros
- 🗑️ Eliminar registros
- 📝 Modificar datos existentes
- 📧 Consultar correos
- 🔍 Obtener datos por correo

---

## 🧱 Atributos

| Atributo | Tipo | Descripción |
|---------|------|-------------|
| `cx` | `Connection` | Objeto que mantiene la conexión activa. |
| `CB` | `Conexion_Base` | Instancia utilizada para conectarse a la base de datos. |

---

## 🛠️ Métodos Públicos

| Método | Descripción |
|--------|-------------|
| `ListarClientes()` | Devuelve una lista de arreglos de strings con datos completos de los clientes. |
| `ListarClientesCorreo()` | Retorna una lista de correos de los clientes. |
| `InsertarCliente(...)` | Inserta un nuevo cliente en la base de datos (verifica duplicados por nombre completo). |
| `EliminarCliente(...)` | Elimina un cliente con nombre, apellido paterno y materno específicos. |
| `ModificarCliente(...)` | Modifica los datos de un cliente validando duplicados. |
| `DatosCliente(correo)` | Devuelve un arreglo con los datos de un cliente a partir de su correo. |

---

# ✅ Verificación antes de insertar
Evita duplicados mediante:
`SELECT COUNT(*) FROM clientes WHERE Nombre = ? AND ApellidoPaterno = ? AND ApellidoMaterno = ?`

# ✅ Verificación antes de modificar
Evita duplicar nombres de otros clientes al actualizar datos:

`SELECT COUNT(*) FROM clientes 
WHERE Nombre = ? AND ApellidoPaterno = ? AND ApellidoMaterno = ?
AND NOT (Nombre = ? AND ApellidoPaterno = ? AND ApellidoMaterno = ?)`

---

# 👥 Clase `Conexion_Personal.java`

`Conexion_Personal` es una clase Java que gestiona operaciones CRUD sobre la tabla `personal` en una base de datos relacional, conectándose mediante JDBC. Está pensada como parte de un sistema de administración de personal en una aplicación más amplia (por ejemplo, un punto de venta o sistema empresarial)

# 🧩 Dependencias
- Conexion_Base – Clase auxiliar que proporciona una conexión a la base de datos.

- JDBC (java.sql.*)

- java.util.List, ArrayList

- java.util.logging – Para el registro de errores SQL.

# ⚙️ Funcionalidades
📋 Consultas
- CargosDisponibles(), Retorna una lista con los nombres de todos los cargos disponibles.

- ObtenerPersonal(), Devuelve una lista con todos los empleados registrados y sus cargos.

- ObtenerPersonalCargo(String cargoNombre),Devuelve una lista de empleados que pertenecen a un cargo específico.

- BuscarCajero(String usuario),Retorna el nombre completo de un empleado basado en su correo.

- BuscarCorreo(String usuario, String nombre, String cargo), Verifica si existe un empleado con ese nombre, correo y cargo.

# ➕ Inserción
-  InsertarPersonal(String nombre, String apPaterno, String apMaterno, String contraseña, String correo, String cargo), Inserta un nuevo empleado en la base de datos si no existe duplicado.

# 🗑️ Eliminación
- EliminarPersonal(String correo, String cargo),Elimina un empleado basado en su correo y cargo.

# ✏️ Modificación
- ModificarPersonal(...), Actualiza los datos de un empleado, con validación de duplicados.

- ModificarContraseña(String correo, String nuevaContraseña, String cargo), Actualiza la contraseña de un empleado si el correo y cargo coinciden.

# 🔐 Autenticación
- VerificarCredenciales(String correo, String contraseña), Verifica si las credenciales de inicio de sesión son válidas.
--- 
# 📦 Clase Conexion_Producto
La clase Conexion_Producto gestiona todas las operaciones relacionadas con productos dentro de una base de datos, incluyendo inserciones, eliminaciones, modificaciones, ventas, cancelaciones y consultas. Forma parte del paquete Conexion y utiliza una instancia de Conexion_Base para conectarse a la base de datos.

# 📚 Métodos Principales
✅ boolean InsertarProducto(...)
Inserta un nuevo producto en la base de datos si no existe previamente con el mismo nombre, código y proveedor.

- Requiere que el proveedor exista en la tabla proveedor.

- Requiere que la categoría exista en la tabla categoria.

- ❌ boolean EliminarProducto(String Nombre, int Codigo)
Elimina un producto identificado por su nombre y código.

- ✏️ boolean ModificarProducto(...)
Actualiza los datos de un producto existente, identificándolo por nombre y código originales. Verifica que no haya duplicados por nombre con otro código.

- 🔍 List<String[]> ListarProductosTipo(String Tipo)
Retorna una lista de productos disponibles (cantidad > 0) filtrados por tipo de categoría.

- 📋 List<String[]> ListarProductos()
Retorna una lista de todos los productos con cantidad mayor que cero, incluyendo nombre de categoría y proveedor.

- 📂 List<String> CategoriasDisponibles()
Obtiene todas las categorías disponibles desde la base de datos.

- 🛒 boolean VentaProducto(int codigoProducto, int cantidadARestar)
Resta una cantidad específica a un producto, siempre que haya stock suficiente.

- ↩️ boolean CancelarCompra(int codigoProducto, int cantidadAReponer)
Restaura la cantidad de un producto después de cancelar una compra.

# 🔗 Requisitos de Base de Datos
Esta clase espera que existan las siguientes tablas:

- producto (nombre, codigo, categoria, descripcion, proveedor, cantidad, precio)

- categoria (id, categoria)

- proveedor (id, nombre, apellido_paterno, apellido_materno)

# 🧱 Dependencias
- Conexion_Base — Clase utilizada para establecer conexión con la base de datos.

- java.sql.* — Para operaciones con la base de datos (JDBC).

- java.util.* — Para listas dinámicas.

---

## 📦 Clase Conexion_Proveedor
La clase `Conexion_Proveedor` pertenece al paquete Conexion y se encarga de gestionar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre la tabla proveedor en una base de datos relacional. Utiliza la clase `Conexion_Base` para establecer la conexión con la base de datos.

## 🧩 Dependencias

| Librería | Uso |
|--------|-------------|
| `java.sql.Connection` | Conexión con la base de datos. |
| `java.sql.PreparedStatement` | Preparar sentencias SQL seguras |
| `java.sql.ResultSet` | 	Recibir resultados de consultas SQL|
| `java.util.logging.Logger` | Manejo de errores SQL |
| `java.util.ArrayList` | Registro de errores y eventos |
| `java.util.List` | Estructura para almacenar resultados |

#  🧾 Explicación 
La clase 🔌 Conexion_Proveedor se encarga de realizar operaciones sobre la tabla proveedor de una base de datos, como parte del módulo de conexión en una aplicación Java. Utiliza JDBC para interactuar con la base de datos, y depende de una clase auxiliar llamada Conexion_Base que gestiona la conexión.

📌 Funcionalidades principales:
- Insertar proveedores evitando duplicados por nombre completo.

- Eliminar proveedores según su nombre, apellido paterno y materno.

- Modificar proveedores validando que el nuevo nombre no exista ya.

- Listar nombres completos de proveedores.

- Listar todos los datos de los proveedores en forma de lista.

Es útil como una capa intermedia entre la base de datos y la interfaz de usuario, encapsulando la lógica de acceso a los datos de proveedores.

---

# 🧾 Clase `Conexion_Ventas` - Módulo de Gestión de Ventas

Este archivo Java forma parte del sistema de punto de venta y se encarga de manejar la lógica relacionada con **ventas**, incluyendo registros, cancelaciones, generación de reportes y creación de archivos PDF.

📌 Descripción general
La clase Conexion_Ventas se comunica con la base de datos mediante JDBC para realizar operaciones sobre las tablas ventas, detalleventa, producto, clientes y personal.

📂 Dependencias
- `Conexion_Base`: Encargada de establecer la conexión a la base de datos.

- `Correo_Creado`: Utilizada para la generación de PDF con los detalles de venta.

# ⚙️ Métodos principales

| Método | Descripción|
|--------|-------------|
| `boolean EliminarVenta(int)` |Cancela una venta: elimina registros y repone stock. |
| `boolean registrarVenta(...)` |Registra una venta y sus detalles en la base de datos.|
| `List<String[]> obtenerReporteVentas()` | Obtiene un reporte de todas las ventas realizadas.|
| `void generarPDFVenta(int)` | Genera un archivo PDF con los datos completos de una venta específica.|

📄 Detalles de cada método
🔻 EliminarVenta(int idVenta)
- Elimina una venta completa y repone el stock de productos involucrados.


- Usa transacciones (commit/rollback) para garantizar la integridad de los datos.

🧾 registrarVenta(String correoCliente, String usuarioCajero, List<String[]> ticket)

- Inserta una venta en la tabla ventas y sus productos en detalleventa.


- Calcula el total de la venta automáticamente.


- Valida que cada producto exista antes de registrar la venta.

📊 obtenerReporteVentas()

- Realiza un LEFT JOIN entre ventas, clientes y personal.


- Retorna una lista con: ID, nombre del cliente, nombre del cajero, total y fecha.

📄 generarPDFVenta(int idVenta)

- Consulta todos los detalles de una venta (productos, cantidades, precios).


- Extrae información del cliente y cajero asociado.


- Llama a Correo_Creado para generar un PDF de la venta.
