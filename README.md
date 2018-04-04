# The Twelve-Factor App

## Introducción

En estos tiempos, el software se está distribuyendo como un servicio: se le denomina web apps, o software as a service (SaaS). “The twelve-factor app” es una metodología para construir aplicaciones SaaS que:

- Usan formatos **declarativos** para la automatización de la configuración, para minimizar el tiempo y el coste que supone que nuevos desarrolladores se unan al proyecto;
- Tienen un **contrato claro** con el sistema operativo sobre el que trabajan, ofreciendo la **máxima portabilidad** entre los diferentes entornos de ejecución;
- Son apropiadas para **desplegarse** en modernas **plataformas en la nube**, obviando la necesidad de servidores y administración de sistemas;
- **Minimizan las diferencias** entre los entornos de desarrollo y producción, posibilitando un **despliegue continuo** para conseguir la máxima agilidad;
- Y pueden **escalar** sin cambios significativos para las herramientas, la arquitectura o las prácticas de desarrollo.

La metodología “twelve-factor” puede ser aplicada a aplicaciones escritas en cualquier lenguaje de programación, y cualquier combinación de ‘backing services’ (bases de datos, colas, memoria cache, etc).

## Contexto

Los colaboradores de este documento han estado involucrados directamente en el desarrollo y despliegue de cientos de aplicaciones, y han sido testigos indirectos del desarrollo, las operaciones y el escalado de cientos de miles de aplicaciones mediante nuestro trabajo en la plataforma [Heroku](http://www.heroku.com/).

Este documento sintetiza toda nuestra experiencia y observaciones en una amplia variedad de aplicaciones SaaS. Es la triangulación entre practicas ideales para el desarrollo de aplicaciones, prestando especial atención a las dinámicas del crecimiento natural de una aplicación a lo largo del tiempo, las dinámicas de colaboración entre desarrolladores que trabajan en el código base de las aplicaciones y [evitando el coste de la entropía del software](http://blog.heroku.com/archives/2011/6/28/the_new_heroku_4_erosion_resistance_explicit_contracts/).

Nuestra motivación es mejorar la concienciación sobre algunos problemas sistémicos que hemos observado en el desarrollo de las aplicaciones modernas, aportar un vocabulario común que sirva para discutir sobre estos problemas, y ofrecer un conjunto de soluciones conceptualmente robustas para esos problemas acompañados de su correspondiente terminología. El formato está inspirado en los libros de Martin Fowler [Patterns of Enterprise Application Architecture](http://books.google.com/books/about/Patterns_of_enterprise_application_archi.html?id=FyWZt5DdvFkC) y [Refactoring](http://books.google.com/books/about/Refactoring.html?id=1MsETFPD3I0C).

¿Quién debería leer este documento?
Cualquier desarrollador que construya aplicaciones y las ejecute como un servicio. Ingenieros de operaciones que desplieguen y gestionen dichas aplicaciones.

## Twelve Factors

### [I. Código base (Codebase)](01-codigo-base.md)

Un código base sobre el que hacer el control de versiones y multiples despliegues

### [II. Dependencias](02-dependencias.md)

Declarar y aislar explícitamente las dependencias

### [III. Configuración](03-configuracion.md)

Guardar la configuración en el entorno

### [IV. Backing services](04-backing-services.md)

Tratar a los “backing services” como recursos conectables

### [V. Construir, distribuir, ejecutar](05-construir-distribuir-ejecutar.md)

Separar completamente la etapa de construcción de la etapa de ejecución

### [VI. Procesos](06-procesos.md)

Ejecutar la aplicación como uno o más procesos sin estado

### [VII. Asignación de puertos](07-asignacion-puertos.md)

Publicar servicios mediante asignación de puertos

### [VIII. Concurrencia](08-concurrencia.md)

Escalar mediante el modelo de procesos

### [IX. Desechabilidad](09-desechabilidad.md)

Hacer el sistema más robusto intentando conseguir inicios rápidos y finalizaciones seguras

### [X. Igualdad entre desarrollo y producción](10-igualdad-desarrollo-produccion.md)

Mantener desarrollo, preproducción y producción tan parecidos como sea posible

### [XI. Historiales](11-historiales.md)

Tratar los historiales como una transmisión de eventos

### [XII. Administración de procesos](12-administracion-procesos.md)

Ejecutar las tareas de gestión/administración como procesos que solo se ejecutan una vez
