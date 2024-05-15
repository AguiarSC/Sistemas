Usuarios 
=============

Los sistemas operativos actuales pueden ser utilizados por uno o varios usuarios, en algunos sistemas pueden hacerlo simultáneamente y en otros no ademas estos puedes ser creados de manera local o en red. 

En Linux hay tres tipos de cuentas de usuario: 

- ROOT

  Tiene acceso total al sistema, a todos los archivos del sistema. Es la primera cuenta que se crea al instalar el sistema operativo. Es aconsejable utilizarla únicamente para la administración del sistema. 

- Estándar o locales

  Tienen limitaciones en cuanto a las acciones que pueden realizar, salvo en su directorio personal. Son los recomendados para el uso diario del sistema. 

- Del sistema o asociados a servicios

  Son incorporados por el propio sistema, y se encargan de administrar los demonios del mismo. No pueden iniciar sesiones en el sistema, ni tener un shell donde trabajar.

- Usuario administrador

  Es aquel que tiene capacidad de gestión en el sistema, sin ser necesariamente el superusuario. Esta capacidad puede ser desarrollada si dispone de privilegios gracias al comando sudo.


Los sistemas GNU/Linux gestionan los usuarios mediante archivos de configuración. Sobre estos archivos, los usuarios comunes no gozan de privilegios, por lo que son los administradores o el usuario root los únicos que pueden editarlos.

Como ya sabemos, /etc/passwd almacena las cuentas de todos los usuarios del sistema. Cada fila se corresponde con un usuario y consta de siete campos delimitados por dos puntos.

.. code-block:: sh

root:x:0:0:root:/root:/bin/bash

daemon:x:1:1:daemon:/usr/sbin:/bin/sh

..

nombre de usuario

  contraseña

    id de usuario

      id de grupo

        info usuario

          carpeta personal

            Shell



El id del usuario sigue un patron en el cual el 0 es el root o superusuario, de la 1-99 usuarios predefinidos del sistema y de la 100-999 para cuentas administrativas del sistema, por tanto, los nuevos usuarios serán asociados a partir del 1000.

El prompt, o línea de petición de órdenes en el intérprete de comandos, varía según el usuario activo en él. En Ubuntu, cuando el superusuario se encuentra activo en el intérprete de comandos a la espera de introducir órdenes, su indicativo de petición en el prompt es el símbolo "#", mientras que para el resto de usuarios es "$".

El comando su permite abrir una sesión del intérprete de comandos con el ID de otro usuario o iniciar una nueva shell con ese
identificador. si se pone su sin seguir de un usuario se interpretara que se esta llamando al usuario root.

+-------------------+----------------------+---------------------------------------------------------------------+
| Tipo              | Archivos             | Descripción                                                         |
+===================+======================+=====================================================================+
| globales          | ``etc/skel``         | Directorio que contiene la pantalla de creación de perfiles de usuario|
+-------------------+----------------------+---------------------------------------------------------------------+
| globales          | ``etc/profile``      | Configuración genérica de perfiles cuando se inicia sesion en el sistema      como login shell|
+-------------------+----------------------+---------------------------------------------------------------------+
| globales          | ``etc/bash.bashrc``  | Configuración genérica de perfiles cuando se inicia sesion con shell bash| 
|                   |                      | interactivo                                                         |
+-------------------+----------------------+---------------------------------------------------------------------+

Seguridad de cuentas y contraseñas 
---------------------------------------

Las contraseñas se gestionan gracias al fichero de configuración /etc/shadow, que contiene las cuentas de los usuarios
del sistema. Este fichero sólo puede ser leído por el root y la contraseña está encriptada.

.. code-block:: xml
slice: ajhdkash453ad74s3:14324:0:99999:7::
..

valores 
---------

 - slice = nombre

 - ajhdkash453ad74s3: =contraseña

!: indica que la cuenta está bloqueada
*: indica que esta cuenta no se puede utilizar para iniciar sesión
!!: indica que la contraseña caducó. 
El procesador puede ejecutar instrucciones de dos modos: 

  - Modo usuario: normalmente es el empleado por los programas de usuario y las actividades no críticas del sistema operativo. Puede aver varios modos de usuario, diferenciados por privilegios.Si este desea realizar una operación critica debera llamar al kernel y que este la realice.
  
  - Modo kernel, núcleo o privilegiado: es el empleado principalmente por el sistema operativo para ejecutar las instrucciones contenidas en él. En este modo se puede obtener el control total del sistema.

Por otro lado, la ejecución de los procesos puede realizarse de varios modos: 

  -Por lotes, de trabajos o batch: se lanza un conjunto de tareas para realizar por el sistema y este ejecuta todas ellas, una detrás de otra, sin intervención del usuario.
  
  - Interactivo: a diferencia de los anteriores, estos solicitan constantemente las acciones del usuario para su continuidad. El usuario realiza una acción mediante la ejecución de un comando o acción dentro de un programa y espera a que finalice para realizar otra acción o proceso interactivo.

 - Los procesos llamados servicios (Windows) o demonios (Linux), realizan una función específica y se caracterizan generalmente por comenzar automáticamente cuando se inicia el sistema y ejecutarse en segundo plano. El usuario no espera que finalicen para interactuar con el sistema. 

Identificación y administración
----------------------------------

Los procesos disponen de un identificador único llamado PID (IDentificador de Procesos). El PCB (bloque de control de proceso) de cada proceso almacena información esencial para la gestión del mismo.Informacion como el usuario propietario,el estado,los buffers o la identificación de procesos y proceso padre.

 El superusuario son aquellos usuarios con postestad para administrar los procesos del sistema.No obstante, cada usuario puede gestionar sus propios procesos. 

El primer proceso que se crea en el sistema es el proceso denominado init y él no tiene un
proceso padre.

Cuando ejecutamos un programa desde la línea de comandos, es el shell quien maneja su ejecución: 

Si la orden es un comando interno (pwd...), se ejecuta internamente sin generar nuevos procesos; pero si la orden no es interna, entonces el shell crea un proceso hijo que ejecuta esa orden mientras el proceso padre (el shell) espera hasta que el hijo termina su ejecución, momento en que el shell “se despierta” para interpretar la siguiente orden. 


Estados de procesos(STAT o S):

+-------------------+-------------------------------------------------------------------------------------------+
| Tipo              | Descripción                                                                               |
+===================+===========================================================================================+
| ``R``             | Ejecutandose o listo para ser ejecutado                                                   |
+-------------------+-------------------------------------------------------------------------------------------+
| ``S``             | Bloqueado o durmiendo                                                                     |
+-------------------+-------------------------------------------------------------------------------------------+
| ``T``             | Parado                                                                                    | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``Z``             | Zombi(proceso muerto pero que su proceso padre no ha reconocido su muerte)                | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``I``             | Inactivo en creación                                                                      |
+-------------------+-------------------------------------------------------------------------------------------+
| ``N``             | Con prioridad menor de lo normal                                                          | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``<``             | Con prioridad mayor de lo normal                                                          |
+-------------------+-------------------------------------------------------------------------------------------+
| ``+``             | Se encuentra en el grupo deprocesos del primer plano                                      |
+-------------------+-------------------------------------------------------------------------------------------+
| ``s``             | Proceso lider en sesión                                                                   | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``l``             | Es un proceso multihilo (mismo proceso con multiples tareas que se pueden realizar en paralelo|
|                   | evitando así el cambio de contexto)                                                       |
+-------------------+-------------------------------------------------------------------------------------------+

Gestión por interfaz gráfica de Windows
=========================================

Por defecto, Windows crea varias cuentas administrativas que no se encuentran habilitadas por seguridad, aunque a través de esta ventana podemos activarlas. Como son:

-Administrador: cuenta con los privilegios más altos del sistema, que permite realizar cualquier acción, similar a root en Linux.

-Invitado: cuenta destinada a aquellos usuarios que acceden al sistema esporádicamente, sin apenas privilegios. 

Consola de comandos Windows :
--------------------------------

A través de la consola de comandos podemos añadir un usuario con el siguiente comando:

.. code-block:: xml

net user [nombredeusuario] [contraseña | * ] opciones /add 


+-------------------------------+-------------------------------------------------------------------------------+
| Tipo                          | Descripción                                                                   |
+===============================+===============================================================================+
| ``"*"``                       | Genera un mensaje que pide la contraseña. La contraseña no se muestra al escribirla.|
+-------------------------------+-------------------------------------------------------------------------------+
| ``/domain``                   | Permite añadir el usuario al dominio.                                         |
+-------------------------------+-------------------------------------------------------------------------------+
| ``/active:{yes|no}``          | Activa o desactiva la cuenta de usuario                                       | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``/comment:"texto"``          | Añade un comentario a la cuenta del usuario                                   | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``/passwordchg:{yes|no}``     | Si los usuarios pueden cambiar su contraseña.                                 |
+-------------------------------+-------------------------------------------------------------------------------+
| ``/logonpasswordchg:{yes|no}``| Si el usuario debe cambiar la contraseña en el siguiente inicio.              | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``/expires:{fecha| NEVER}``   | Hace que la cuenta expire si se establece una fecha                           |
+-------------------------------+-------------------------------------------------------------------------------+
| ``/fullname:"nombre"``        | Especifica el nombre completo de usuario.                                     |
+-------------------------------+-------------------------------------------------------------------------------+
| ``/homedir:nombrederuta``     | Ruta del directorio principal del usuario.                                    | 
+-------------------+-------------------------------------------------------------------------------------------+
| ``/profilepath[:ruta]``       | Establece una ruta para el perfil de inicio de sesión del usuario.            |
+-------------------------------+-------------------------------------------------------------------------------+
| ``net user [nombredeusuario]``| Eliminar un usuario                                                           |
| ``[opciones] /delete``        |                                                                               |
+-------------------------------+-------------------------------------------------------------------------------+
| ``net localgroup``            | Ver los grupos predeterminados                                                |
+-------------------------------+-------------------------------------------------------------------------------+
|``net localgroup [nomdegrupo]``| Crear un grupo                                                                |
| ``opciones /add``             |                                                                               |
+-------------------+-------------------------------------------------------------------------------------------+
| ``net localgroup nombregrupo``| Añadir un usuario al grupo                                                    | 
| ``/add nombreusuario``        |                                                                               |
+-------------------+-------------------------------------------------------------------------------------------+
| ``net localgroup nombregrupo``| Comprobar que el usuario se ha agregado                                       |
+-------------------------------+-------------------------------------------------------------------------------+
|``net localgroup [nomdegrupo]``| Eliminar un grupo                                                             |
| ``/delete``                   |                                                                               |
+-------------------+-------------------------------------------------------------------------------------------+
| `` net localgroup nomgrupo``  | Eliminar un usuario de un grupo                                              |
| ``/delete nombreusuario``     |                                                                               |
+-------------------------------+-------------------------------------------------------------------------------+

Procesos y servicios:
=======================

Los sistemas operativos como Windows, macOS y Linux, son multitarea y multiusuario, el sistema operativo asigna
pequeños espacios de tiempo a cada tarea y usuario.

Las instancias de los programas en ejecución, también llamados tareas o procesos, son administrados por el sistema operativo como un recurso más. Dependiendo de los privilegios de los usuarios sobre el sistema, estos podrán modificar la planificación de procesos

El sistema operativo gestiona todos los procesos mediante operaciones de creación, comunicación, compartición y finalización de procesos. El módulo del sistema operativo encargado de realizar estas tareas es el planificador de procesos. Los procesos pueden pasar por distintos estados desde que se crea hasta que muere. El
planificador de procesos se encarga de establecer el estado de cada proceso y de modificarlo, atendiendo a un algoritmo de planificación. 

El procesador puede ejecutar instrucciones de dos modos: 

  - Modo usuario: normalmente es el empleado por los programas de usuario y las actividades no críticas del sistema operativo. Puede aver varios modos de usuario, diferenciados por privilegios.Si este desea realizar una operación critica debera llamar al kernel y que este la realice.
  
  - Modo kernel, núcleo o privilegiado: es el empleado principalmente por el sistema operativo para ejecutar las instrucciones contenidas en él. En este modo se puede obtener el control total del sistema.

Por otro lado, la ejecución de los procesos puede realizarse de varios modos: 

  -Por lotes, de trabajos o batch: se lanza un conjunto de tareas para realizar por el sistema y este ejecuta todas ellas, una detrás de otra, sin intervención del usuario.
  
  - Interactivo: a diferencia de los anteriores, estos solicitan constantemente las acciones del usuario para su continuidad. El usuario realiza una acción mediante la ejecución de un comando o acción dentro de un programa y espera a que finalice para realizar otra acción o proceso interactivo.

 - Los procesos llamados servicios (Windows) o demonios (Linux), realizan una función específica y se caracterizan generalmente por comenzar automáticamente cuando se inicia el sistema y ejecutarse en segundo plano. El usuario no espera que finalicen para interactuar con el sistema. 


 Primer y segundo plano 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La forma de ejecutar en 1º plano es la que utilizamos de meter codigo en el terminal y esperar a q acabe y salga de nuevo el prompt, pero existe una alternativa para evitar que el propio usuario tenga que esperar la terminación de una tarea para poder continuar con la ejecución de otras nuevas, denominada ejecución en segundo plano o background. Consiste en añadir al final de la línea de mandatos que ejecutar en el shell, el símbolo "&". De esta manera, el prompt se devolverá inmediatamente, sin esperar la terminación de la tarea recién lanzada. 

  - Con el comando jobs podemos identificar las tareas o trabajos que se hallan ejecutándose en segundo plano
Cuando un proceso es detenido, el sistema nos muestra un mensaje similar al siguiente:

.. code-block:: sh
[nº_tarea]+ Stopped nombre_proceso


.. code-block:: sh
fg [%][tarea] 

  pasa una tarea a primer plano.

.. code-block:: sh
bg[%][tarea] 

  pasa una tarea a segundo plano


Prioridad de las órdenes 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

El valor nice de un proceso oscila entre -20 (máxima prioridad) y 19 (menor prioridad),por defecto, un usuario solo puede disminuir la prioridad de sus procesos cuando los lanza.

Podemos lanzar procesos, modificando su prioridad relativa con nice, siendo su sintaxis:

.. code-block:: sh
nice -[n] {+|-} numero_nice orden 

.. code-block:: sh
renice prioridad [[-p] PID´s] [[-u] usuarios]

sirve para disminuir su prioridad

Envío de señales 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Los procesos reciben señales para ser controlados desde el propio sistema operativo y desde el exterior. Un usuario también puede enviar señales a los procesos

.. code-block:: sh
kill -señal PID 


  -2 o SIGINT: interrumpe un proceso. Esta señal puede ser manejada por el propio proceso, aunque no es lo habitual, terminando su ejecución.

  - 9 o SIGKILL: mata inmediatamente un proceso.

  - 15 o SIGTERM: termina o mata un proceso, aunque esta señal puede ser ignorada en determinados casos.

  - 18 o SIGCONT: continúa la ejecución de un proceso.

  - 19 o SIGSTOP: pausa la ejecución de un proceso. 


En Linux se pueden planificar tareas de manera periódica o recurrente gracias a cron, que permite lanzar órdenes o scripts definidosen un archivo crontab

Los ficheros crontab han de especificar las órdenes y su periodicidad mediante los siguientes valores separados por espacios:

  MINUTOS [0..59] HORA [0..23] DIA [1..31] MES [1..12] DIA DE LA SEMANA [0..6] ORDEN

Si un campo se ignora, se especifica mediante "*", indicando cualquier valor válido. Se pueden especificar listas mediante comas y sin espacios, mediante sus valores mínimos y máximos separados por "-", y también mediante un valor de inicio y un valor incremental, separados por "/". 
