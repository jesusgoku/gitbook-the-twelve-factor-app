# X. Igualdad entre desarrollo y producción

## Mantener desarrollo, preproducción y producción tan parecidos como sea posible

Históricamente, han existido dos tipos de entorno muy diferenciados: desarrollo (donde un desarrollador puede editar en vivo en un [despliegue](https://12factor.net/es/codebase) local de la aplicación) y producción (un despliegue en el que la aplicación está en ejecución disponible para que lo usen los usuarios). Estas diferencias se pueden clasificar en tres tipos:

- **Diferencias de tiempo**: Un desarrollador puede estar trabajando en un código durante días, semanas o incluso meses antes de que llegue a producción.
- **Diferencias de personal**: Los desarrolladores escriben el código y los ingenieros de operaciones lo despliegan.
- **Diferencias de herramientas**: Los desarrolladores pueden usar una pila como Nginx, SQLite y OS X, mientras que en producción se usa Apache, MySQL y Linux.

**Las aplicaciones “twelve-factor” están diseñadas para hacer [despliegues continuos](http://avc.com/2011/02/continuous-deployment/) que reducen las diferencias entre los entornos de desarrollo y producción.** Teniendo en cuenta las tres diferencias descritas anteriormente:

- Reducir las diferencias de tiempo: Un desarrollador puede escribir código y tenerlo desplegado en tan solo unas horas, o incluso, minutos más tarde.
- Reducir las diferencias de personal: Los desarrolladores que escriben el código están muy involucrados en el despliegue y observan su comportamiento en producción.
- Reducir las diferencias de herramientas: tratar de hacer que desarrollo y producción sean tan parecidos como sea posible.

Resumiendo lo anterior en una tabla:

| | Aplicaciones tradicionales | Aplicaciones "twelve-factor" |
|-|:-:|:-:|
| Tiempo entre despliegues | Semanas | Horas |
| Desarrolladores vs Ingenieros de operaciones | Diferentes personas | Mismas personas |
| Entorno de desarrollo vs entorno de producción | Divergentes | Lo más parecidos posibles |

Los [“backing services”](https://12factor.net/es/backing-services), como la base de datos de la aplicación, el sistema de colas, o la caché, es donde la igualdad en los entornos de desarrollo y producción es importante. Muchos lenguajes ofrecen librerías en las que se simplifica el acceso a los servicios de respaldo, incluidos adaptadores para diferentes tipos de servicios. Se pueden observar algunos ejemplos en la siguiente tabla.

| Tipo | Lenguaje | Librería | Adaptador |
| - | :-: | :-: | :-: |
| Base de datos | Ruby/Rails | ActiveRecord | MySQL, PostgreSQL, SQLite |
| Colas | Python/Django | Celery | RabbitMQ, Beanstalkd, Redis |
| Caché | Ruby/Rails | ActiveSupport::Cache | Memoria, sistema de ficheros, Memcached |

Los desarrolladores, a veces, caen en la tentación de usar “backing services” ligeros en sus entornos de desarrollo, mientras que en producción se usan los más serios y robustos. Por ejemplo, se usa SQLite en desarrollo y PostgreSQL en producción; o memoria local para la caché en desarrollo y Memcached en producción.

**Un desarrollador “twelve-factor” no cae en la tentación de usar diferentes “backing services” en desarrollo y producción**, incluso cuando los adaptadores teóricamente abstractos están lejos de cualquier diferencia en “backing services”. Las diferencias entre los servicios de respaldo tienen que ver con las pequeñas incompatibilidades que surgen de la nada, causando que el código que funciona y pasa los tests en desarrollo o en preproducción, falle en producción. Este tipo de errores provocan conflictos que desincentivan la filosofía del despliegue continuo. El coste de estos conflictos y el enfriamiento subsiguiente del despliegue continuo es extremadamente alto cuando se hace balance del total de tiempo de vida de una aplicación.

Los servicios ligeros locales son menos atractivos que antes. Los “backing services” modernos como Memcached, PostgreSQL, y RabbitMQ no son difíciles de instalar y ejecutar gracias a los sistemas de gestión de paquetes modernos, como [Homebrew](http://mxcl.github.com/homebrew/) y [apt-get](https://help.ubuntu.com/community/AptGet/Howto). Al mismo tiempo, las herramientas de gestión de la configuración como [Chef](http://www.opscode.com/chef/) y [Puppet](http://docs.puppetlabs.com/) combinadas con entornos virtuales ligeros como [Docker](https://www.docker.com/) o [Vagrant](http://vagrantup.com/) permiten a los desarrolladores ejecutar entornos locales que son muy parecidos a los entornos de producción. El coste de instalar y usar estos sistemas es bajo comparado con el beneficio que se puede obtener de la paridad entre desarrollo y producción y del despliegue continuo.

Los adaptadores de los “backing services” todavía son de gran utilidad, porque hacen que cambiar de unos a otros sea un trámite relativamente poco doloroso. No obstante, todos los despliegues de una aplicación (en entornos de desarrollo, preproducción y producción) deberían usar el mismo tipo y versión de cada uno de los “backing services”.