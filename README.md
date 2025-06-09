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

# Paquete de conecciones

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

🧾 registrarVenta

(String correoCliente, String usuarioCajero, List<String[]> ticket)

- Inserta una venta en la tabla ventas y sus productos en detalleventa.


- Calcula el total de la venta automáticamente.


- Valida que cada producto exista antes de registrar la venta.

📊 obtenerReporteVentas()

- Realiza un LEFT JOIN entre ventas, clientes y personal.


- Retorna una lista con: ID, nombre del cliente, nombre del cajero, total y fecha.

📄 generarPDFVenta

(int idVenta)

- Consulta todos los detalles de una venta (productos, cantidades, precios).


- Extrae información del cliente y cajero asociado.


- Llama a Correo_Creado para generar un PDF de la venta.

---

# Clase "Correro_Creado"

Esta clase en Java permite **generar archivos PDF personalizados** y **enviarlos por correo electrónico** utilizando la librería `iText` para PDFs y `Jakarta Mail` para el envío de correos.

---

## ✨ Funcionalidades

- 📄 Generación de PDFs:
  - Comprobante de venta (`CrearPDFVenta`)
  - Código de recuperación de cuenta (`crearPDFRecuperacion`)
  - Código de verificación (`crearPDFVerificacion`)
- ✉️ Envío de correos con PDF adjunto (`EnviarCorreo`)

---

## 📦 Dependencias

- [`jakarta.mail`](https://eclipse-ee4j.github.io/mail/)
- [`itextpdf`](https://itextpdf.com)

---

## 🧱 Estructura del código

### Variables importantes

java
private final String CorreoRemitente = "mercad.ito.tap14@gmail.com";
private final String ContraseñaRemitente = "dior zlmu gcch kxrh";
private final String NombreEmpresa = "Mercad - ITO";
private final String rutaLOGO = "ruta/a/tu/logo.png";
private String rutaPDF;

## Métodos principales
- 📁 String generarRutaPDF(String tipo, String identificador)
Genera una ruta con nombre automático (tipo + fecha) para el PDF.


- 🧾 void CrearPDFVenta(List<String[]> lista, String nombreUsuario, ...)
Genera un comprobante de venta con tabla de productos y totales.


- 🔐 void crearPDFRecuperacion(String nombreCompleto, String correoUsuario, ...)
Genera un documento PDF con código de recuperación y detalles del usuario.


- ✅ void crearPDFVerificacion(String CodigoVerificacion, String nombrePersona, ...)
Genera un PDF con un código de verificación centrado y formateado.


- 📤 void EnviarCorreo(String CorreoDestinatario, String Cuerpo)
Envía por correo el PDF previamente generado como archivo adjunto.

---

# Clase validación

## ✨ Funcionalidades

### 🔤 1. `soloLetras(JTextField textField)`
✅ Permite ingresar únicamente letras (mayúsculas, minúsculas), vocales acentuadas y la letra ñ en un `JTextField`.

---

### 🔢 2. `soloNumeros(JTextField textField)`
✅ Restringe el campo para que solo se puedan ingresar números enteros.

---

### 💲 3. `Precio(JTextField textField)`
✅ Permite ingresar números decimales válidos, incluyendo el punto (`.`) como separador decimal. Solo se permite un punto por número.

---

### 🔡 4. `soloLetrasYNumeros(JTextField textField)`
✅ Permite letras (con y sin acentos), números y espacios. Es útil para nombres de usuario o campos mixtos.

---

### 📧 5. `VerificarCorreo(String Email) : boolean`
✅ Verifica si una dirección de correo electrónico es válida.  
Admite dominios:
- `.com`
- `.mx`
- `.itoaxaca`  
También valida correos comunes como:
- `@hotmail`
- `@gmail`
- `@outlook`

---

### 🧩 6. `GenerarCodigos() : String`
🔐 Genera un código aleatorio de 8 caracteres que puede incluir:
- Letras (excluye I y O para evitar confusión)
- Números
- Caracteres especiales  
Ideal para CAPTCHAs o códigos de validación.

---

# Paquete de vistas

## 🧾 Interfaz de Login - Mercad-ITO

Este proyecto forma parte del sistema de ventas para **Mercad-ITO**, una aplicación de escritorio desarrollada en Java con Swing. Proporciona una interfaz gráfica de inicio de sesión que permite acceder como **Administrador** o **Cajero**, con opciones adicionales como recuperación de contraseña y registro de usuarios.

---

## ✨ Características principales

- Interfaz amigable con FlatLaf (FlatLightLaf) ✨
- Acceso diferenciado según rol: 👨‍💼 Administrador / 👷‍♂️ Cajero
- Validación de credenciales desde la base de datos
- Iconos visuales de verificación o error ✅❌
- Recuperación de contraseña 🔐
- Registro de nuevos usuarios 📝

---

## 🧠 Funcionalidad del código

El comportamiento principal se basa en los siguientes puntos:

| Componente       | Descripción                                                                            |
|------------------|----------------------------------------------------------------------------------------|
| `btnAceptar`     | Verifica credenciales. Si son válidas, redirige al usuario según el tipo de cuenta.   |
| `btnCajeros`     | Selecciona el modo **Cajero**, activando iconos relacionados.                         |
| `btnAdministrador` | Selecciona el modo **Administrador**, activando iconos relacionados.                 |
| `btnRecuperarC`  | Abre la ventana de recuperación de contraseña.                                        |
| `btnRegistrarse` | Abre la ventana de registro de nuevos usuarios.                                       |
| `iconSegContra`  | Alterna la visibilidad de la contraseña al hacer clic. 👁️                              |
| `formWindowClosing` | Muestra una ventana de confirmación al cerrar la aplicación.                      |

---

## 🔍 Métodos importantes

### `btnAceptarActionPerformed`
Este método es clave para validar al usuario. Dependiendo de la variable `Opcion`, verifica si es cajero o administrador y redirige:

## 📦 Dependencias
- FlatLaf: Mejora visual moderna para interfaces Swing.

- Conexion_Personal: Clase que permite verificar credenciales contra la base de datos.

- Conexion_Producto: Gestión de productos (inicializada, pero no usada aquí).

- Recursos gráficos (/Img/*.png) para íconos visuales.

---

## 🛒 Sistema de Carrito de Compras - Mercad-ITO

# Img

## 📋 Descripción
Mercad-ITO es un sistema de punto de venta (POS) desarrollado en Java con interfaz gráfica Swing. Permite a los cajeros gestionar ventas de productos, administrar el inventario y generar tickets de compra con envío automático por correo electrónico.

## ✨ Características Principales

- 🛍️ Gestión de Productos: Visualización y filtrado de productos por categorías
- 🧾 Sistema de Tickets: Generación automática de tickets de venta
- 📧 Envío de Correos: Envío automático de tickets por email
- 👥 Gestión de Clientes: Registro y selección de clientes
- 📊 Control de Inventario: Actualización automática del stock
- 💰 Cálculo de Totales: Suma automática de productos y totales

## 🏗️ Arquitectura del Sistema

| Componente | Descripción | Responsabilidad |
|---------|------|-------------|
| `Carrito` | Clase principal | Interfaz gráfica y lógica de negocio|
| `Conexion_Producto` | Gestión de productos| CRUD de productos y categorías |
| `Conexion_Clientes` | Gestión de clientes| Manejo de datos de clientes |
| `Conexion_Personal` | Gestión de empleados |Datos de cajeros y personal |
| `Conexion_Ventas` |Registro de ventas| Persistencia de transacciones |
| `Correo_Creado` | Sistema de correos| Generación de PDFs y envío de emails|
| `Validacion` |Validaciones |Validación de entrada de datos. |

## 🖥️ Interfaz de Usuario
Pestañas Principales
### 🔍 Pestaña "Elegir"

- Tabla de productos disponibles
- Filtro por categorías
- Campo de cantidad
- Botón para agregar productos al carrito

## 🛒 Pestaña "Venta"

- Tabla del carrito de compras
- Selección de cliente
- Total a pagar
- Botones de acción (Pagar, Cancelar, Eliminar)

### 📦 Gestión de Productos

`// Llenar tabla de productos
public void LlenarTablaProductos(List<String[]> lista)`

`// Filtrar por categoría
public void btnCategoriaActionPerformed(ActionEvent evt)`

 Características:

- ✅ Visualización de productos con detalles completos
- ✅ Filtrado dinámico por categorías
- ✅ Validación de stock disponible
- ✅ Actualización automática del inventario

### 🛍️ Carrito de Compras

`// Agregar producto al carrito
public void btnConfirmarProductoActionPerformed(ActionEvent evt)`

`// Agrupar productos duplicados
public void LlenarTablaVenta(List<String[]> lista)`

 Características:

- ✅ Agrupación automática de productos duplicados
- ✅ Cálculo automático de totales
- ✅ Validación de cantidades
- ✅ Eliminación individual de productos

### 💳 Sistema de Pagos
`// Procesar pago
public void btnPagarActionPerformed(ActionEvent evt)`

`// Cancelar venta completa
public void CancelarVenta(List<String[]> ticket)`

Características:

- ✅ Generación automática de PDF
- ✅ Envío de ticket por correo electrónico
- ✅ Registro de venta en base de datos
- ✅ Restauración de stock en cancelaciones

  ### Tabla de Productos

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `Nombre` | String | Nombre del producto|
| `Código` | Integer|Código único del producto|
| `Categoría` | String| Categoría del producto |
| `Descripción` | String |Descripción detallada|
| `Proveedor` |String| Proveedor del producto|
| `Cantidad` |Integer|Stock disponible|
| `Precio` |Double| Precio unitario|

# 💻 Uso del Sistema
## Para Cajeros

### Iniciar Sesión 🔐

- Ingresar credenciales de cajero


### Seleccionar Productos 🛍️

- Navegar a la pestaña "Elegir"
- Filtrar por categoría (opcional)
- Seleccionar producto y cantidad
- Hacer clic en "Agregar producto"


### Gestionar Carrito 🛒

- Ir a la pestaña "Venta"
- Revisar productos agregados
- Eliminar productos si es necesario


### Procesar Pago 💳

- Seleccionar cliente
- Verificar total
- Hacer clic en "Pagar"



## 🔒 Validaciones y Seguridad
Validaciones Implementadas

- ✅ Cantidades: Solo números positivos
- ✅ Stock: Verificación de disponibilidad
- ✅ Campos obligatorios: Validación de datos requeridos
- ✅ Selección de productos: Validación de selección en tablas

---

# Sistema de venta 
Un sistema integral de gestión empresarial desarrollado en Java Swing que permite administrar clientes, proveedores, productos, ventas y personal de manera eficiente.
## 📋 Descripción
SistemaPrueba es una aplicación de escritorio que centraliza la gestión de diferentes aspectos de un negocio, proporcionando una interfaz intuitiva para el manejo de datos empresariales con funcionalidades avanzadas como generación de PDFs y verificación por correo electrónico.

## ✨ Características Principales

- 👥 Gestión de Clientes: Registro, modificación y eliminación de clientes
- 🏭 Gestión de Proveedores: Administración completa de proveedores
- 📦 Gestión de Productos: Control de inventario y categorización
- 💰 Gestión de Ventas: Registro y seguimiento de transacciones
- 👨‍💼 Gestión de Personal: Administración de empleados por cargo
- 📧 Verificación de Correo: Sistema de validación mediante códigos
- 📄 Generación de PDFs: Reportes automáticos de ventas
- 🔍 Filtros Avanzados: Búsqueda por categorías y cargos

## 🗂️ Módulos del Sistema
  | Módulo | Descripción | Funcionalidades |
|---------|------|-------------|
| 👤 Clientes| Gestión de base de clientes |➕ Agregar ✏️ Editar 🗑️ Eliminar 📋 Listaro|
| 🏭 Proveedores| Administración de proveedores|➕ Agregar ✏️ Editar 🗑️ Eliminar 📋 Listar|
| 📦 Productos | Registro de transacciones|📋 Visualizar 🗑️ Eliminar 📄 Generar PDF|
| Personal| Gestión de empleados |➕ Agregar ✏️ Editar 🗑️ Eliminar 🔍 Filtrar por cargo|

## 🛠️ Tecnologías Utilizadas

- Java Swing: Interfaz gráfica de usuario
- MySQL: Base de datos relacional
- JavaMail API: Envío de correos electrónicos
- iText/PDFBox: Generación de documentos PDF
- MVC Pattern: Arquitectura del software

## 🚀 Funcionalidades Destacadas
### 📧 Sistema de Verificación por Correo

- Generación automática de códigos de verificación
- Envío de correos electrónicos con PDFs adjuntos
- Validación en tiempo real de direcciones de correo

## 📊 Gestión de Datos

- Validación de Entrada: Solo números para teléfonos, solo letras para nombres
- Filtros Dinámicos: Búsqueda por categorías de productos y cargos de personal
- Confirmaciones: Diálogos de confirmación para operaciones críticas

## 📄 Generación de Reportes

- PDFs automáticos de ventas
- Documentos de verificación personalizados
- Apertura automática de archivos generados

## 🏗️ Arquitectura del Sistema
```
SistemaPrueba/
├── 🖼️ GUI (Swing Components)
├── 🔗 Conexiones a BD
│   ├── Conexion_Clientes
│   ├── Conexion_Proveedor
│   ├── Conexion_Producto
│   ├── Conexion_Ventas
│   └── Conexion_Personal
├── ✅ Validaciones
├── 📧 Correo_Creado
└── 📋 Modelos de Tabla
```
## 📱 Interfaz de Usuario
El sistema cuenta con una interfaz tabbed que organiza los módulos:

- Tab 0: 👤 Gestión de Clientes
- Tab 1: 🏭 Gestión de Proveedores
- Tab 2: 📦 Gestión de Productos
- Tab 3: 💰 Gestión de Ventas
- Tab 4: 👨‍💼 Gestión de Personal
- Tab 5: 🏠 Panel Principal (por defecto)

## 🔐 Características de Seguridad

- ✅ Validación de formatos de correo electrónico
- 🔒 Confirmaciones para operaciones de eliminación
- 📧 Verificación de identidad mediante códigos por correo
- 🛡️ Validación de entrada de datos

---

# 🔐 Recuperar contraseña 

## 📋 Descripción
El sistema de Recuperación de Contraseña es una aplicación Java Swing que permite a los usuarios recuperar y cambiar sus contraseñas de forma segura mediante un proceso de verificación por correo electrónico.

## ✨ Características Principales

- 🔒 Recuperación segura de contraseñas
- 📧 Verificación por correo electrónico
- 🎯 Validación de datos en tiempo real
- 🔑 Generación automática de códigos de verificación
- 👁️ Visualización opcional de contraseñas
- 📄 Generación de PDFs para documentación

## 🏗️ Arquitectura del Sistema
  | Componente | Descripción | Responsabilidad |
|---------|------|-------------|
| Recuperar_Contraseña| Clase principal de la ventana |Gestión de la interfaz y lógica principal|
| Correo_Creado| Servicio de correo|Envío de emails y generación de PDFs|
| Validacion | Validador de datos|Validación de entrada y generación de códigos|
| Conexion_Personal| Acceso a datos |Operaciones de base de datos|

## 🚀 Flujo de Funcionamiento
  | Paso | Acción | Descripción |
|---------|------|-------------|
| 1| Ingreso de Datos |Usuario ingresa correo, nombre y cargo|
| 2| Validación|Sistema valida formato de correo y existencia del usuario|
| 3 | Envío de Código|Se genera y envía código de verificación por email|
| 4| Verificación |Usuario ingresa código recibido|
| 5| Nueva Contraseña |Usuario establece nueva contraseña|
| 6| Confirmación |Sistema actualiza contraseña en base de datos|

## 🛠️ Métodos Principales
  | Método | Propósito | Parámetros |
|---------|------|-------------|
| RellenarCargos()| 📋 Llena el ComboBox con cargos disponibles |Ninguno|
|EsconderTodo()| 👁️‍🗨️ Oculta elementos de la interfaz|Ninguno|

## Métodos de Eventos
| Método       | Evento/Acción                                                                            |
|------------------|----------------------------------------------------------------------------------------|
| `btnECRCActionPerformed()`     | 📧 Enviar Código|
| `txtCodigoRCActionPerformed()`     | 🔢 Verificar Código  |
| `btnAceptarActionPerformed()` | ✅ Aceptar Cambio |
| `btnSalirActionPerformed()`  | 🚪 Salir|
| `iconSegContraMousePressed/Released()` | 👁️ Mostrar Contraseña|
| `iconSegContra1MousePressed/Released()`  | 👁️ Mostrar Confirmación|

## 🔧 Validaciones Implementadas
### 📧 Validación de Correo

- ✅ Formato válido de email
- ✅ Existencia en base de datos
- ✅ Correspondencia con nombre y cargo

## 🔐 Validación de Contraseñas

- ✅ Coincidencia entre contraseña y confirmación
- ✅ Campos no vacíos

## 🔢 Validación de Código

- ✅ Comparación exacta con código generado
- ✅ Formato numérico

## 🎨 Elementos de la Interfaz
  | Campo | Tipo | Descripción |
|---------|------|-------------|
| txtCorreoRC| TextFields |📧 Correo electrónico|
| txtNombreRC| TextField|👤 Nombre del usuario|
| cbxCargo| ComboBox|💼 Cargo del empleado|
| txtCodigoRC| TextField|🔢 Código de verificación|
| passContraRC| PasswordField |🔐 Nueva contraseña|
|passContraConfirmar| PasswordField |✅ Confirmación de contraseña|

## 🚨 Manejo de Errores
  | Error | Mensaje | Acción |
|---------|------|-------------|
| 📧 Correo inválido| "El correo no tiene el formato correcto" Mostrar iconCRC4|
| 👤 Usuario no encontrado| "Personal no encontrado"|Mostrar en txtResultado|
| 🔢 Código incorrecto| Visual (iconos de error)|Mostrar iconCRC1,2,3|
| 🔐 Contraseñas diferentes| "Las contraseñas no coinciden"|Mostrar diálogo y iconos|
| 💾 Error de actualización| "Error al modificar la contraseña" |Mostrar diálogo|

## 📄 Funcionalidades Adicionales
### 📧 Sistema de Correo

- Generación de PDF: Documento con código de recuperación
- Envío automático: Correo con código de verificación
- Manejo de excepciones: MessagingException

### 🔐 Seguridad

- Códigos únicos: Generación aleatoria para cada solicitud
- Validación múltiple: Email, nombre y cargo deben coincidir
- Confirmación de contraseña: Doble verificación

### 🎯 Casos de Uso
### Escenario Exitoso ✅

- Usuario ingresa datos válidos
- Sistema encuentra usuario en BD
- Se envía código por correo
- Usuario ingresa código correcto
- Se establecen contraseñas coincidentes
- Sistema actualiza contraseña exitosamente

### Escenarios de Error ❌

- Datos inválidos: Email mal formado o usuario inexistente
- Código incorrecto: Usuario ingresa código erróneo
- Contraseñas diferentes: No coinciden contraseña y confirmación
- Error de BD: Falla al actualizar contraseña

---

# 📋 Sistema de Registro de Personal
## 🎯 Descripción
Sistema de registro de personal desarrollado en Java Swing que permite el registro seguro de nuevos empleados con validación de correo electrónico, generación automática de contraseñas y verificación por código.

## 🛠️ Funcionalidades Principales

- ✅ Registro de personal con datos completos
- 📧 Verificación por correo electrónico
- 🔐 Generación automática de contraseñas seguras
- 🔍 Validación de campos en tiempo real
- 👁️ Visualización temporal de contraseñas
- 📄 Generación de PDF de verificación

## 📊 Tabla de Métodos Principales

  | Método | Descripción | Parámetros |
|---------|------|-------------|
| `LlenarPersonal()`|📝 Carga los cargos disponibles en el ComboBox|Ninguno|
| `ValidacionesEntradas()`| ✏️ Configura validaciones para campos de texto|Ninguno|
| `btnRegistrarUsuarioActionPerformed()`| 💾 Procesa el registro del nuevo personal|ActionEvent|
| `btnSugerirContraseñaActionPerformed()`| 🔑 Genera una contraseña segura automáticamente|ActionEvent|
| `txtCorreoRegistroActionPerformed()`| 📬 Envía código de verificación al correo |ActionEvent|
| `iconContraseñaMousePressed/Released()`|👀 Controla la visibilidad de contraseñas|MouseEvent|
| `btnSalirActionPerformed()`|🚪 Maneja el cierre seguro de la ventana |MouseEvent|

## ⚙️ Funcionamiento del Sistema
### 🔄 Flujo de Registro

- 📝 Captura de Datos: El usuario ingresa nombre, apellidos, contraseña y selecciona un cargo
- 🔍 Validación: El sistema valida que solo se ingresen letras en campos de nombre
- 📧 Verificación de Correo: Al ingresar el correo, se genera y envía un código de verificación
- 🔐 Validación de Contraseña: Se verifica que la contraseña cumpla con los requisitos de seguridad
- ✅ Confirmación: Se valida que las contraseñas coincidan
- 💾 Registro: Se almacena el personal en la base de datos tras verificar el código

## 🎨 Componentes de la Interfaz

- 🏷️ Campos de Texto: Nombre, apellidos, correo y código de verificación
- 🔒 Campos de Contraseña: Contraseña y confirmación con opción de visualización
- 📋 ComboBox: Selección de cargo del personal
- 🔘 Botones: Registro, sugerir contraseña, salir
- ⚠️ Iconos de Error: Indicadores visuales para campos inválidos

## 🔧 Características Técnicas

- 🎨 Framework: Java Swing para interfaz gráfica
- 🗄️ Base de Datos: Conexión mediante clase Conexion_Personal
- 📧 Email: Envío de correos con verificación PDF
- 🔐 Seguridad: Generación de contraseñas con biblioteca generarContrasena
- ✅ Validación: Validaciones personalizadas mediante clase Validacion

## 🚨 Validaciones Implementadas

- ✏️ Campos de Nombre: Solo acepta letras
- 📧 Correo Electrónico: Formato válido de email
- 🔐 Contraseña: Cumplimiento de requisitos de seguridad
- 🔄 Confirmación: Coincidencia entre contraseñas
- 🏷️ Cargo: Selección obligatoria de cargo
- 🔢 Código: Verificación del código enviado por correo

## 🎯 Casos de Uso

- 👤 Administrador registra nuevo empleado
- 📧 Sistema envía verificación automática
- 🔐 Generación de contraseña temporal segura
- ✅ Validación completa antes del registro

## 🔒 Seguridad

- Las contraseñas se ocultan por defecto con caracteres '*'
- Generación automática de contraseñas que cumplen requisitos de seguridad
- Verificación por correo electrónico obligatoria
- Validación de datos antes del registro en base de datos

## 📱 Interfaz de Usuario
La interfaz cuenta con un diseño intuitivo con:

- 🎨 Colores corporativos (púrpura y azul)
- ⚠️ Iconos de error que se muestran dinámicamente
- 👁️ Controles de visibilidad para contraseñas
- 📋 Formulario organizado y fácil de usar.

---
# 🔗Video
[https://youtu.be/dB0VDqqTKwc](https://youtu.be/OvW1wi_TP-g)
---
# Autores
- Méndez García Ángel de Jesús
- Pérez Jiménez Santiago Enmanuel 
