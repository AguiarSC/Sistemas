COMANDOS DE LAS PRÁCTICAS
=========================

``awk``
-------

Es una herramienta de procesamiento de textos. Se utiliza principalmente para la manipulación y análisis de datos en formato de texto. Permite realizar operaciones de filtrado, formateo, y transformación de datos de manera eficiente. Presenta la siguiente estructura base:

.. code-block::

  awk 'patrón {acción}' archivo

..

El ``patrón`` especifica cuándo debe ejecutarse la acción y puede ser una expresión regular o una condición lógica; ``la acción`` define qué operación se realizará en las líneas que coincidan con el patrón y están delimitadas por llaves {}.

Entre sus opciones más comunes, destacan:

* ``-F`` (field-separator): para definir el delimitador de campos. Por defecto, considera que están separados por espacios en blanco.

  .. code-block::

    awk -F ',' '{print $1}' archivo.csv 

  ..

* ``-v``: para definir variables.

  .. code-block::

    awk -v var=valor 'patrón {acción}' archivo

  ..

* ``-f``: para especificar un archivo que contiene el script awk a ejecutar.

  .. code-block::

    awk -f script.awk archiv

  ..

Entre sus patrones más comunes y acciones comunes, destacan:

* ``%n``: hace referencia al n-ésimo campo de la línea actual.

  .. code-block::

    awk '{print $1, $3}' archivo

  ..

* ``NR``: hace referencia al número de línea.

  .. code-block::

    awk 'NR == 5' archivo

  ..

* ``$0``: hace referencia a la línea actual. Equivalente a ``cat archivo``

  .. code-block::

    awk 'NR == 5' archivo

  ..

* Ejemplos de las prácticas

  .. code-block::
  
    awk '/Linux/{count++} END{print count}' datos.txt

    Recorre cada línea del archivo datos.txt. Cada vez que encuentra una línea que contiene la palabra "Linux", incrementa un contador (count). Al final del procesamiento de todas las líneas, imprime el valor del contador, que representa el número total de líneas que contienen la palabra "Linux".
  
  ..


``cat``
-------

Se utiliza principalmente para concatenar y mostrar el contenido de archivos. Es una de las herramientas básicas y más usadas en la línea de comandos. Es muy útil y versátil, no solo para mostrar archivos sino también para combinarlos, crear nuevos archivos y más, mediante su uso combinado con redirección y pipes ``|``.

Entre sus opciones más comunes, destacan:

* ``cat archivo``: muestra el contenido de uno o más archivos en la salida estándar.

  .. code-block::

    cat archivo.txt

  ..

* ``cat archivo1 archivo2 ...``: concatenar y muestra el contenido de varios archivos en la salida estándar.

  .. code-block::

    cat archivo1.txt archivo2.txt

  ..

* ``cat > archivo``: crea un nuevo archivo o sobrescribe uno existente con la entrada que se proporcione desde el teclado hasta que se use ``Ctrl+D`` para indicar el fin de la entrada.

  .. code-block::

    cat > nuevo_archivo.tx

  ..


* ``cat >> archivo``: añade la entrada proporcionada al final de un archivo existente.

  .. code-block::

    cat >> existente.txt

  ..

* ``cat -n archivo``: numera todas las líneas de los archivos proporcionados.

  .. code-block::

    cat -n archivo.tx

  ..

* ``cat -b archivo``: numera solo las líneas no vacías.

  .. code-block::

    cat -b archivo.txt

  ..

* ``cat -s archivo``: numera solo las líneas no vacías.

  .. code-block::

    cat -s archivo.txt

  ..

* ``cat -v archivo``: muestra los caracteres no imprimibles, excepto las tabulaciones y saltos de línea, en un formato visible.

  .. code-block::

    cat -v archivo.txt

  ..

* ``cat -e archivo``: equivalente a usar ``-vE``. Muestra los caracteres no imprimibles y marca el final de cada línea con un ``$``.

  .. code-block::

    cat -e archivo.txt

  ..

* ``cat -t archivo``: equivalente a usar ``-vT``. Muestra los caracteres no imprimibles y reemplaza las tabulaciones con ``^I``.

  .. code-block::

    cat -t archivo.txt

  ..


``awk``
-------

Es una herramienta de procesamiento de textos. Se utiliza principalmente para la manipulación y análisis de datos en formato de texto. Permite realizar operaciones de filtrado, formateo, y transformación de datos de manera eficiente. Presenta la siguiente estructura base:

.. code-block::

  awk 'patrón {acción}' archivo

..

El ``patrón`` especifica cuándo debe ejecutarse la acción y puede ser una expresión regular o una condición lógica; ``la acción`` define qué operación se realizará en las líneas que coincidan con el patrón y están delimitadas por llaves {}.

Entre sus opciones más comunes, destacan:

* ``-F`` (field-separator): para definir el delimitador de campos. Por defecto, considera que están separados por espacios en blanco.

  .. code-block::

    awk -F ',' '{print $1}' archivo.csv 

  ..

* ``-v``: para definir variables.

  .. code-block::

    awk -v var=valor 'patrón {acción}' archivo

  ..

* ``-f``: para especificar un archivo que contiene el script awk a ejecutar.

  .. code-block::

    awk -f script.awk archiv

  ..

Entre sus patrones más comunes y acciones comunes, destacan:

* ``%n``: hace referencia al n-ésimo campo de la línea actual.

  .. code-block::

    awk '{print $1, $3}' archivo

  ..

* ``NR``: hace referencia al número de línea.

  .. code-block::

    awk 'NR == 5' archivo

  ..

* ``$0``: hace referencia a la línea actual. Equivalente a ``cat archivo``

  .. code-block::

    awk 'NR == 5' archivo

  ..



















