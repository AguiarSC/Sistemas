PRESENTACIÓN ORAL
-----------------

Buenos días. Hoy os vamos a presentar las funcionalidades y mejoras implementadas durante este último sprint. En esencia, el equipo se ha centrado en la implementación de la seguridad y en la mejora de la gestión de usuarios, compras, facturación y transacciones.

Comenzaré por mostrar todo lo relacionado con la seguridad. Hemos implementado autenticación mediante credenciales y autorización mediante roles. Se han establecido tres grupos principales de usuarios: administrador, trabajador y cliente, cada uno con sus permisos asignados. [MOSTRAR LOS PREPARADOS EN LA BD]. Además, se ha añadido la encriptación de contraseñas para garantizar la privacidad y seguridad.

Ahora, vayamos al Swagger. Como podéis ver, Swagger muestra todas las opciones y métodos disponibles, aunque estos son inaccesibles hasta que se complete el proceso de autenticación del usuario. Una vez autenticado, se harán accesibles los métodos dedicados a cada rol de usuario.

Hemos implementado un registro mediante el cual podemos añadir nuevos usuarios. [DEMOSTRACIÓN]. Una vez registrado, el usuario podrá acceder al método de login, donde, añadiendo sus credenciales (email y contraseña), recibirá un token. Con este token, el usuario se dirigirá a la parte superior del Swagger, donde se encuentra el botón de Authenticate. Aquí añadirá el token recibido por el login, autenticándose en el servicio. [DEMOSTRACIÓN CON CADA ROL UN MÉTODO AL QUE PUEDE ACCEDER Y UNO AL QUE NO]. 

Finalmente, el usuario, al terminar sus gestiones, podrá hacer logout mediante nuestro método personalizado. Además, el token tiene un tiempo de caducidad para forzar el cierre de sesión automáticamente. Como podéis ver, para hacer logout no es necesario aportar ninguna credencial, ya que este método solo funciona si el usuario se ha autenticado previamente.

[¿DEBEMOS DE MENCIONAR ESTO?]
Cabe mencionar que estamos trabajando en brindar al usuario la posibilidad de cambiar su contraseña una vez establecida, pero no os lo podemos mostrar en esta demo.
   






USER:
    • Añadir método modificar datos de tu usuario. Se controlan las posibilidades de introduccion de datos correctos  (dni, currency...)
       
SHOPPINGCART:
    • Añadir posibilidad de tener 3 carritos.
    • Poder realizar varias compras.
    • Controlar los cambios de stock en las compras.
      
INVOICE:
    • Corrección datos de la factura.
    • Posibilidad de descargar la factura.
    • Añadir diferentes idiomas para los correos y las facturas.
    • Mostrar todas las facturas de un usuario.

PRODUCT SUPPLIER TRANSACTIONS
    • Incorporar facturas de un proveedor (comprar y devolver)
    • (SUPPLIER) ver historial de compras a un proveedor.

SUPPLIER:
    • Devuelve el historial de compras y devoluciones de un supplier específico.

TRANSACTIONS:
    • Añadir calculo ingresos, gastos y beneficios por fechas.

TODO EN GENERAL:
    • Controlar todas las respuestas de todos los métodos.


