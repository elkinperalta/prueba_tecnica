4. Buenas prácticas de liderazgo técnico

Demuestre cómo lideraría el desarrollo de este sistema con un equipo pequeño (2-3
desarrolladores). Debe abordar:
• ¿Cómo organizaría los sprints y la asignación de tareas?
RTA: 
Sprint 1 – Configuración y arquitectura básica:


Configuración del entorno de desarrollo (servidor, base de datos, control de versiones).
Diseño de la arquitectura de software y base de datos.
Creación de los módulos de autenticación y autorización de usuarios.


Sprint 2 – Módulo de Solicitudes de Productos:
Desarrollo de tablas, procedimientos almacenados y controladores PHP.
endpoints para creación y consulta de solicitudes.
Pruebas unitarias e integración.


Sprint 3 – Módulo de Ofertas de Proveedores:
Desarrollo de tablas, procedimientos almacenados y controladores.
Endpoints para crear y consultar ofertas.
Validaciones de acceso por roles.


Sprint 4 – Módulo de Decisiones del Cliente:
Desarrollo de tablas, procedimientos almacenados y controladores.
Endpoints para aceptar, rechazar o contraofertar ofertas.
Pruebas funcionales completas del flujo.

Sprint 5 – Optimización y Seguridad:
Implementación de JWT, roles de usuario y middleware.
Optimización de consultas, validaciones y manejo de errores.
Pruebas de carga y rendimiento.

Sprint 6 – Documentación y entrega:
Documentación técnica y de usuario.
Creación de manuales de API y diagramas de arquitectura.
Ajustes finales y despliegue en entorno productivo.
Backlog priorizado: Todas las tareas se documentan en un backlog, con prioridad según impacto y dependencia entre módulos.
Asignación por roles y competencias:
Desarrolladores PHP y MySQL se enfocan en backend y procedimientos almacenados.
Frontend (si aplica) se asigna a desarrolladores con experiencia en interfaces y consumo de API.
Revisión y pruebas: Cada tarea se valida mediante pruebas unitarias y de integración antes de cerrar.
Daily: Se realizan reuniones cortas diarias para seguimiento de avances y resolución de bloqueos.
Los beneficios para este modelo de trabajo Agile es que permite entregas parciales funcionales en cada sprint, asegurando retroalimentación temprana.
Facilita la adaptación a cambios en requerimientos.
Garantiza que todos los miembros del equipo (2,3 o n) tengan claridad sobre prioridades y responsabilidades.

• ¿Qué metodologías y herramientas de revisión de código recomendaría?
RTA:
Pull Requests (PR) con revisión por pares:
Configurar pipelines en GitHub Actions, GitLab CI/CD o Jenkins para ejecutar tests unitarios y de integración en cada PR.
Integración continua (CI) y pruebas automáticas

• ¿Qué procesos de CI/CD implementaría para garantizar la calidad y el despliegue
continuo?
RTA:

Para asegurar la calidad del software y un despliegue confiable y continuo, se recomienda implementar un flujo de CI/CD basado en las siguientes prácticas:

Integración Continua (CI)
Control de versiones: Todo el código se gestiona mediante Git, utilizando ramas de desarrollo (develop) y producción (main/master).

Automatización de pruebas: Cada commit o PR dispara un pipeline que ejecuta pruebas unitarias, de integración y validación de endpoints API.

Se asegura que ningún cambio rompa funcionalidades existentes.

Análisis estático y linters: Se ejecutan herramientas como SonarQube para verificar calidad del código, vulnerabilidades y cumplimiento de estándares.

Build automatizado:
Se genera un build listo para despliegue que incluye dependencias, configuraciones y scripts necesarios.

2. Despliegue Continuo (CD)

Los cambios aprobados en CI se despliegan automáticamente en un entorno de pruebas, replicando lo más fielmente posible el entorno de producción.
Validación previa a producción: Se realizan pruebas funcionales, de rendimiento y de seguridad en staging antes de promover los cambios a producción.

Despliegue automatizado a producción: Una vez aprobado, el pipeline despliega los cambios al servidor de producción usando scripts o contenedores Docker.

Esto garantiza consistencia entre entornos y minimiza errores manuales.

Monitoreo: Se integran logs y alertas para detectar fallas durante o después del despliegue.

Rollback automático: En caso de errores críticos, el sistema puede revertir a la versión anterior estable, asegurando disponibilidad del servicio.
