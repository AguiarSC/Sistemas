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
