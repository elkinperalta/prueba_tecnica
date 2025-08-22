

3. Justificación de decisiones técnicas
Debe justificar las principales decisiones técnicas que tomó en el diseño e implementación.
Debe abordar aspectos como:
• ¿Por qué eligió la estructura arquitectónica propuesta?
RTA:

En el diseño e implementación del sistema que indicaron como prueba,  se tomaron las siguientes decisiones técnicas clave:
1. Elección de la arquitectura modular en capas
Se optó por una arquitectura en capas (Presentación, Lógica de Negocio, Persistencia) por las siguientes razones:
Claridad y separación de responsabilidades: Cada capa maneja funciones específicas:


La capa de Presentación / API REST gestiona la interacción con los usuarios y la exposición de los endpoints.


La capa de Lógica de Negocio centraliza reglas de negocio, validaciones y procesos, asegurando que las decisiones se ejecuten de manera consistente.


La capa de Persistencia / Base de Datos asegura el almacenamiento estructurado y eficiente de clientes, proveedores, solicitudes, ofertas y decisiones.


Escalabilidad: Esta arquitectura permite ampliar los módulos o agregar nuevas funcionalidades sin afectar otras partes del sistema. Por ejemplo, se pueden integrar futuras notificaciones, reportes o servicios externos.


Mantenibilidad: Separar las responsabilidades facilita el mantenimiento, depuración y actualización del sistema, permitiendo que los desarrolladores trabajen en módulos específicos sin interferir en otros.


2. Uso de JWT para autenticación y autorización
Seguridad: Se eligió JWT para autenticar usuarios y controlar roles (CLIENTE y PROVEEDOR) de forma confiable.


Escalabilidad y eficiencia: Los tokens permiten que los endpoints validen usuarios sin necesidad de consultar la base de datos en cada petición, reduciendo carga y mejorando la performance.


Flexibilidad: JWT permite implementar fácilmente expiración de tokens, renovación mediante refresh tokens y control de acceso granular según los roles de usuario.


3. Uso de procedimientos almacenados (SP) en MySQL
Seguridad y consistencia: Los SP encapsulan la lógica de creación, consulta y actualización de solicitudes, ofertas y decisiones, minimizando el riesgo de inyecciones SQL y errores de integridad.


Eficiencia: Permite ejecutar operaciones complejas de manera optimizada directamente en la base de datos.


Mantenibilidad: La lógica de negocio crítica se centraliza en la base de datos, facilitando cambios sin afectar el código PHP de los controladores.


4. Organización de controladores y middleware en PHP
Modularidad: Cada módulo (Auth, Usuarios, Solicitudes, Ofertas, Decisiones) tiene su propio controlador, lo que facilita la extensión y mantenimiento.


Middleware: Implementa CORS, manejo de errores y validación de JWT, centralizando la seguridad y la estandarización de respuestas JSON.


Reusabilidad: Funciones como require_auth() y json_response() son reutilizables en todos los módulos, reduciendo duplicación de código.


5. Diseño de base de datos normalizada
Integridad y trazabilidad: Tablas separadas para solicitudes, detalles, ofertas y decisiones permiten mantener relaciones claras y consistentes.


Escalabilidad: La normalización permite almacenar grandes volúmenes de solicitudes y ofertas sin comprometer el rendimiento.


Auditoría: Cada acción (crear solicitud, enviar oferta, tomar decisión) queda registrada, facilitando la revisión histórica de operaciones.


En resumen, cada decisión técnica se orientó a construir un sistema seguro, escalable y mantenible, capaz de crecer con futuras funcionalidades y soportar múltiples usuarios y flujos de interacción entre clientes y proveedores.

• ¿Cómo maneja el sistema la seguridad de las transacciones (autenticación, roles de
usuario)?
RTA:

El sistema garantiza la seguridad de las transacciones mediante autenticación robusta y control de roles, asegurando que solo usuarios autorizados puedan realizar determinadas acciones.
1. Autenticación
Se utiliza JWT (JSON Web Tokens) para autenticar usuarios en cada petición.


Durante el login, se emite un access token de corta duración y un refresh token para renovación segura.


Los tokens incluyen información del usuario como ID, email y rol, permitiendo validar la identidad sin consultar la base de datos en cada solicitud.


Todas las rutas que requieren autenticación verifican el token mediante el middleware require_auth(), asegurando que solo usuarios válidos puedan acceder a los endpoints.



2. Autorización por Roles
El sistema distingue entre roles CLIENTE y PROVEEDOR.


Cada módulo valida el rol antes de ejecutar acciones específicas:


Clientes: Pueden crear solicitudes y tomar decisiones sobre ofertas recibidas.


Proveedores: Pueden enviar ofertas únicamente a solicitudes abiertas.


La función require_role() asegura que el usuario tenga el permiso correcto para cada operación, evitando accesos no autorizados.


3. Protección de Datos y Operaciones
Las contraseñas se almacenan encriptadas con hash seguro (password_hash), garantizando confidencialidad.


Los procedimientos almacenados (SP) gestionan la creación, actualización y consulta de solicitudes, ofertas y decisiones, reduciendo el riesgo de inyecciones SQL.


Las acciones críticas (aceptar, rechazar o contraofertar) requieren token válido y rol autorizado, asegurando la integridad de las transacciones.
• ¿Cómo manejaría el crecimiento del sistema si tuviera que escalar?
RTA: 

En cuanto al software 
Servidores API: Se pueden desplegar múltiples instancias del backend PHP detrás de un balanceador de carga, distribuyendo las solicitudes de los clientes y proveedores de manera equitativa.
Base de datos: Aunque inicialmente se utiliza MySQL, la arquitectura permite implementar replicación maestro-esclavo, separando lectura y escritura para mejorar rendimiento y disponibilidad.
Almacenamiento estático y CDN: Archivos o recursos que no cambian se pueden distribuir mediante CDN, aliviando la carga del servidor principal.

En cuanto al hardware 
Aumentar la capacidad del servidor (CPU, RAM, disco) en caso de crecimiento repentino de usuarios o solicitudes.


Optimización de consultas SQL y procedimientos almacenados para mejorar la velocidad de respuesta sin necesidad de reestructurar la base de datos.
