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


--------------------
VARIABLES DE ENTORNO
--------------------

Las variables utilizadas en un script son solo accesibles en él. Mediante ``export`` podemos exportarla al entorno del sistema, siendo almacenada en la sesión y accesible en cualquier proceso.

.. code-block:: sh

  export var2 = mundo2 #

..

El sistema tiene predefinidas una serie de variables de entorno manipulables mediante scripts:

* ``PS1``: mensaje del prompt.

* ``HOME``: ruta del directorio home del user.

* ``PATH``: lista de rutas en las que se buscan los comandos, separadas por ``:``.

* ``SHELL``: ruta del shell utilizado.

* ``DISPLAY``: consola por la que se rdirige la salida.

* ``LONGNAME`` o ``USER``: nombre del user.

* ``IFS``: separador de campos internos.


--------------------
PASO DE PARÁMETROS
--------------------

Interesa que el script pueda recibir parámetros en la consola y acceder a ellos en el script, para lo que se utilizará:

* ``$#`` devuelve el número de parámetros.

* ``$@`` o ``$*`` devuelve todos los parámetros.

* ``$0`` devuelve el nombre del script.

* ``$n`` devuelve el valor del parámetro ``n``.

* ``$!`` devuelve el número de proceso del último proceso ejecutado.

* ``$?`` devuelve el código de retorno del último comando ejecutado. Puede devolver ``0`` si se ejecutó correctamente o ``1`` en caso contrario.

* ``Shift (n)`` desplaza a la izquierda y renombra todos los parámetros. Se puede indicar el número de posiciones que nos queremos desplazar. Siempre se pierde el valor ``$1``.

* ``READ`` inserta la entrada del user (teclado) en el script, asignándole una o más variables. Si no se porporciona un nombre a la variable del shell se utiliza ``REPLY`` por defecto.

* ``ECHO`` escribe sus argumentos sobre la salida estándar (pantalla). Entiende las siguientes secuencias:

  * ``\b`` BACKSPACE.

  * ``\C`` print sin salto de línea.

  * ``\f`` siguiente página.

  * ``\n`` NEWLINE.

  * ``\r`` RETURN.

  * ``\t`` TAB.

  * ``\v`` TAB vertical.

  * ``\\`` barra invertida ``\``.

  * ``\On`` ASCII en octal de cualquier carácter.


----------------
CONTROL DE FLUJO
----------------

Pueden incluirse en los scripts sentencias de control de flujo (condicionales o iterativas). También puede utilizarse, en lugar de ``else if``, ``elif`` para eliminar el ``fi``

* ``if ... then .. fi`` para bifurcar la ejecución de un script.

  .. code-block:: sh
  
    if [condición1]; then acción1
    else if[condición2]; then acción2
      else acción
      fi
    fi
  
  .. 

  .. code-block:: sh
  
    if [condición1]; then acción1
    elif [condición2]; then acción2
      else acción
    fi
  
  .. 

* ``TEST`` que permite evaluar una expresión y ver si es verdadera (= 0) o falsa (!= 0). Su expresión es ``test expresión`` o ``[expresión]``. Son utilizados con frecuencia en las condiciones del ``if``. Esta expresión puede tener cualquiera de los formatos siguientes:

  * ``-e fichero`` si el fichero existe.
  
  * ``-r fichero`` si el fichero existe y se puede leer.
  
  * ``-w fichero`` si el fichero existe y se puede escribir.
  
  * ``-x fichero`` si el fichero existe y se puede ejecutar.
  
  * ``-f fichero`` si el fichero existe y es un fichero regular.
  
  * ``-d fichero`` si el fichero es un directorio.
  
  * ``-c fichero`` si el fichero es especial de tipo caracter.
  
  * ``-b fichero`` si el fichero es especial de tipo bloque.
  
  * ``-h fichero`` si el fichero existe y es un enlace simbólico.
  
  * ``-s fichero`` si el fichero tiene un tamaño mayor que 0.
  
  * ``z s1`` La longitud de la cadena s1 es cero.
  
  * ``-n s1`` La longitud de la cadena s1 no es cero (no es vacía).
  
  * ``s1 = s2`` Las dos cadenas son iguales.
  
  * ``s1 != s2`` Las dos cadenas son distintas.
  
  * ``s1`` La cadena s1 existe.
  
  * ``n1 –eq n2`` n1 e n2 tienen el mismo valor numérico.
  
  * ``n1 –ne n2`` n1 e n2 tienen distinto valor numérico.
  
  * ``n1 –gt n2`` n1 tiene un valor mayor que n2 (mayor estricto).
  
  * ``n1 –lt n2`` n1 tiene un valor menor que n2 (menor estricto).
  
  * ``n1 –ge n2`` n1 tiene un valor mayor o igual que n2.
  
  * ``n1 –le n2`` n1 tiene un valor menor o igual que n2.
  
  * ``! e`` Negación de la expresión (es cierta si la expresión es falsa).
  
  * ``e1 -a e2`` AND lógico de las expresiones.
  
  * ``e1 -o e2`` OR lógico de las expresiones.
  
  * ``\( e \)`` Los paréntesis se usan para agrupar expresiones y cambiar el orden de evaluación.


.. code-block:: sh

    ...

..


* ``case ... in ... esac`` es una estructura de control en el scripting de shell que permite ejecutar diferentes bloques de código según el valor de una variable. Cada patrón posible del ``case`` puede ser:
  * Un valor constante, numérico o de cadena.
  * Un conjunto de valores constantes, separados por ``|``.
  * Un rango de valores, separando el mínimo y el máximo por ``-``.

  Se puede definir un patrón por defecto utilizando ``*)``, el cual se ejecutará si ningún otro patrón coincide con la variable. Cada cláusula debe terminarse con ``;;`` o ``;&``:
  
    * Si termina en ``;;``, el shell no intentará coincidencias posteriores después de la primera coincidencia.
  
    * Si termina en ``;&``, el shell probará los patrones de las siguientes cláusulas.
  
  
  La estructura general es la siguiente:
  
   .. code-block:: sh
  
    case variable in
      patrón1] "comandos a ejecutar si la variable coincide con patrón1";;
      patrón2] "comandos a ejecutar si variable coincide con patrón2";;
      ...
      *) "comandos a ejecutar si variable coincide con patrón2"";
    esac  
  
   .. code-block:: sh
  
    case $variable in
      1) echo "La variable es igual a 1" ;;
      2|3|4) echo "La variable es 2, 3 o 4" ;;
      5-10) echo "La variable está en el rango de 5 a 10" ;;
      *) echo "La variable no coincide con ningún patrón conocido" ;;
    esac

* El bucle ``for`` en su forma básica tiene la siguiente sintaxis:

  .. code-block:: shell
  
      for variable in lista-de-valores
      do
          Instrucciones a ejecutar
      done

  Por ejemplo, podemos utilizar un bucle ``for`` para iterar sobre una lista de nombres:
  
  .. code-block:: shell
  
      for nombre in Juan Pedro María Ana
      do
          echo "Hola, $nombre"
      done
  
  Este bucle imprimirá "Hola, Juan", "Hola, Pedro", "Hola, María" y "Hola, Ana" en la salida estándar. Donde la lista de valores puede ser un conjunto de valores separados por espacio, el resultado de un comando entre comillas inversas (\``), o el conjunto de parámetros del script (\``$@\``).
  
  También se admite una forma alternativa del bucle ``for`` utilizando la sintaxis:
  
  .. code-block:: shell
  
      for (( expr1; expr2; expr3 )) ; do
          comandos
      done
  
  Por ejemplo, podemos utilizar un bucle ``for`` para imprimir los números del 1 al 5:
  
  .. code-block:: shell
  
      for ((contador=1; contador<=5; contador++)); do
          echo -n "$contador "
      done
  
  Este bucle imprimirá los números del 1 al 5 en la salida estándar, separados por un espacio.

* Los bucles ``while`` y ``until`` tienen una sintaxis similar. En el bucle ``while``, las instrucciones dentro de ``do`` se ejecutan mientras la condición sea verdadera (es decir, su código de salida sea 0). En el bucle ``until``, las instrucciones dentro de ``do`` se ejecutan hasta que la condición sea verdadera (es decir, su código de salida no sea 0).

  .. code-block:: shell
  
      # Inicializamos una variable contador
      contador=1
      
      # Mientras el contador sea menor o igual a 5, imprimimos el valor del contador y lo incrementamos en 1
      while [ $contador -le 5 ]
      do
          echo $contador
          contador=$((contador+1))
      done
  
  Este bucle imprimirá los números del 1 al 5 en la salida estándar.

* El operador ``&&`` se utiliza para ejecutar el segundo comando solo si el primer comando tiene éxito; es decir, si su código de salida es 0. Por otro lado, ``||`` ejecuta el segundo comando solo si el primero no tiene éxito; es decir, si su código de salida es distinto de 0.

* Las sentencias ``break`` y ``continue`` se utilizan en bucles para controlar la ejecución. ``break`` termina el bucle actual y ``continue`` salta a la siguiente iteración del bucle.

* La sentencia ``exit`` se utiliza para salir del script de shell.

* El comando ``sleep`` hace una pausa del número de segundos indicado.


-----------------------
Definición de Funciones
-----------------------

Una función nos permite englobar un conjunto de comandos bajo un nombre que podemos invocar desde el script. El cuerpo de la función suele ser una lista de comandos encerrados entre llaves y separados por espacios del mismo (las llaves son palabras reservadas). La lista de comandos a ejecutar debe terminar en punto y coma. Su sintaxis es la siguiente:

.. code-block:: shell

    function nombre ()
    {
        comandos a ejecutar;
    }

Por ejemplo, supongamos que queremos definir una función llamada "saludar" que imprima un saludo personalizado:

.. code-block:: shell

    function saludar ()
    {
        echo "Hola, $1"
    }

La sentencia ``return`` (opcional) permite salir de la función devolviendo un valor. Podemos indicar opcionalmente el valor de retorno de la función. Las funciones pueden ser recursivas.

Para invocar una función, simplemente introduciremos su nombre seguido de los posibles parámetros, que se recogerán en la función de la misma forma que se recogen en el script, como ``$1``, ``$2``, etc.

Por ejemplo, después de definir la función ``saludar``, podemos invocarla de la siguiente manera:

.. code-block:: shell

    saludar "Juan"

Este comando imprimirá "Hola, Juan" en la salida estándar.


--------------------
EJEMPLOS DE SCRIPTS
--------------------

1. **Script para entender el tipo de comillas existentes:**

.. code-block:: shell

    #!/bin/bash
    a=ls
    echo '$a'   # Comillas simples, no interpreta caracteres especiales como el carácter $
    echo "$a"   # Comillas dobles, interpreta caracteres especiales como el carácter $ y todo lo
                # que se encuentre entre ellas, considerando todo como un solo parámetro
    echo `$a`   # Comillas inclinadas, ejecuta el contenido dentro de las comillas

2. **Script para entender el tipo de parámetros `$` existentes:**

.. code-block:: shell

    #!/bin/bash
    echo "El parámetro cero, $0, es el propio nombre del script"
    echo "Primer parámetro que recibo: $1, segundo: $2…"
    echo "El número total de parámetros pasados en la ejecución del script (excluido $0) es: $#"
    echo "La lista completa de parámetros (excluido $0), separados por un espacio, es $*"
    echo "El Identificador del proceso (PID) es $$"
    echo "La salida de la ejecución del último comando puede ser correcta (valor cero) o
    errónea (valor distinto de cero), siendo en este caso $?"

3. **Script para hacer operaciones matemáticas con números enteros:**

.. code-block:: shell

    #!/bin/bash
    expr 2 \* 2   # Hace la operación 2*2
    echo "(2 * 2) + 0.5" | bc   # bc es una calculadora para línea de comandos
    echo $((2*2))   # Hace la operación 2*2

4. **Script para pedir variables por teclado:**

.. code-block:: shell

    #!/bin/bash
    echo Dame tu nombre
    read nombre
    echo Hola $nombre

5. **Script para hacer un bucle contador:**

.. code-block:: shell

    #!/bin/bash
    for i in $(seq 1 100)
    do
        echo Valor de i: $i
    done

6. **Script para hacer una condición:**

.. code-block:: shell

    #!/bin/bash
    echo Dame un número
    read n1
    if test $n1 -lt 100
    then
        echo El número $n1 es menor que 100
    else
        echo El número $n1 es mayor que 100
    fi

7. **Script para hacer una condición mejorada:**

.. code-block:: shell

    #!/bin/bash
    echo Dame un número
    read n1
    if test $n1 -le 100
    then
        if test $n1 -lt 100 ; then
            echo El número $n1 es menor que 100
        else
            echo El número es igual a 100
        fi
    else
        echo El número $n1 es mayor que 100
    fi

8. **Script funcionamiento de while:**

.. code-block:: shell

    #!/bin/bash
    i=1
    while [ $i -le 100 ]
    do
        echo Valor de i: $i
        i=$(($i+1))
    done

9. **Script funcionamiento de until:**

.. code-block:: shell

    #!/bin/bash
    i=1
    until [ $i -ge 101 ]
    do
        echo Valor de i: $i
        i=$(($i+1))
    done

10. **Script funcionamiento funciones:**

.. code-block:: shell

    #!/bin/bash
    suma() {
        echo Dame numero
        read n1
        echo Dame otro numero
        read n2
        echo La suma de $n1 y $n2 es: $(($n1+$n2))
    }
    suma

11. **Script funcionamiento case para crear un menú:**

.. code-block:: shell

    #!/bin/bash
    echo Opcion1. Ver directorio actual
    echo Opcion2. Leer /tmp
    echo Opcion3. Salir
    echo Elige opcion: 1, 2, 3?
    read opcion
    case $opcion in
        1) pwd ;;
        2) ls /tmp ;;
        3) exit ;;
        *) echo no elegiste ni 1, 2, 3 ;;
    esac

12. **Script copia de seguridad (backup) home usuario:**

.. code-block:: shell

    #!/bin/bash
    inicio() {
        echo Dame usuario
        read user
        testear
    }
    testear() {
        if test -d /home/$user
        then
            echo El directorio /home/$user existe
            tar -czvf user.tar.gz /home/$user
        else
            echo El directorio /home/$user no existe
            echo El contenido de /home es el siguiente `ls /home`
            inicio
        fi
    }
    inicio









