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

    awk -F ',' '{print $1}' archivo.csv  # Imprime el primer campo de cada línea de un archivo CSV

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

Supongamos:

``Juan,25,Madrid

Ana,30,Barcelona

Luis,22,Valencia``

.. code-block::

  awk -F ',' '{print $1, $2}' datos.txt

..

``Juan 25

Ana 30

Luis 22``

























