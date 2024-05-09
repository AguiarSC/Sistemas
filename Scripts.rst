=============
SCRIPTS LINUX
=============

Los scripts son una secuencia de comandos escritos en un fichero de texto. Sin embargo, los intérpretes de comandos de Linux incluyen toda una serie de estructuras que dan lugar a un auténtico lenguaje de programación, con variables, instrucciones y comandos de entrada/salida, estructuras de control, subprogramas, paso de parámetros, etc.

Lo primero que debemos introducir en el script es una línea en la que se indique para qué intérprete de comandos está programado. Hay que tener en cuenta que los distintos shells tienen funciones y estructuras de control distintas. La sintaxis será: #!ruta_shell. Por ejemplo: ``#!/bin/bash``

A continuación introduciremos líneas con comandos y estructuras permitidas en el shell que estemos programando. El carácter ``#`` nos permite introducir un comentario, ya que el shell ignorará todo lo introducido a continuación.

La extensión habitual de un fichero de script en Linux es ``.sh``, aunque también es frecuente no ponerle ninguna extensión.

Para poder ejecutar el script debemos darle permisos de ejecución, utilizando el comando ``chmod``. A continuación, se ejecuta con la orden sh y el nombre del script.


-----------------------
DEFINICIÓN DE VARIABLES
-----------------------

En Linux, las variables se definen con ``variable=valor`` y se accede a su valor con ``$variable``. Pueden insertarse en cadenas usando comillas dobles para que el shell las sustituya, comillas simples para mostrar el nombre de la variable y comillas invertidas para ejecutar un comando y devolver su resultado. 

Por ejemplo:

``var=mundo;`` 

``echo "hola, $var"`` muestra hola, mundo.

``echo 'hola, $var'`` muestra hola, $var.

``echo `ls` `` muestra el contenido del directorio actual.


-------------------------
EVALUACIÓN DE EXPRESIONES
-------------------------

Si queremos que bash evalúe el contenido de una expresión aritmética y devuelva su resultado usaremos la sintaxis ``$((expresion))`` o ``((expresión))`` (también se puede usar la sentencia ``let`` expresión, por ejemplo ``let x=2+3``).

.. code-block:: sh

  p = $((p+3)) #suma 3 a variable p

..

La sintaxis para evaluar expresiones lógicas o condicionales (que devuelven 1 o 0) es ``[[ expresión ]]``en donde la expresión puede ser:

* Comparación: ``=, !=, <, <=, >, >=``

* Negación: ``!expresión``

• ``and`` o ``or`` de varias expresiones (deben encerrarse entre paréntesis): ``expresión1 && expresión2``, ``expresión1 || expresión2``


El comando ``expr`` toma los argumentos como expresiones, los evalúa e imprime el resultado sobre la salida estándar. Cada término de la expresión debe ir separado por espacios en blanco. Puede sumar, restar, multiplicar y dividir números enteros (limitación) utilizando los operadores ``+,-,*,/ y %`` (resto de la división entera). Puesto que ``* es el comodín del shell``, debe ir precedido de la barra invertida para que el shell lo interprete.

Ejemplos:
.. code-block:: sh

  i=`expr $i \* 1`

  suma=`expr $1 + $2`

  operacion=`expr \( 2 + 3 \) \* 4`

..

Y ya si queremos hacer cosas más complicadas tendremos que recurrir al comando ``bc`` (basic calculator), que es una calculadora por línea de comandos.

Ejemplo:

.. code-block:: sh

  echo "scale=2; 10 / 3" | bc (muestra el resultado de la división con dos decimales)

.. 
