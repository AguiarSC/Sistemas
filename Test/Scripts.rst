SCRIPTS EXAMEN
==============

Bucle contador
--------------

.. code-block:: sh

  #!/bin/bash
  # Este script muestra los números del 1 al 100.
  for i in $(seq 1 100); do
      echo "Valor de i: $i" # Muestra el valor de i en cada iteración.
  done

..


Condicionales
-------------

.. code-block:: sh

  #!/bin/bash
  # Este script compara un número ingresado por el usuario con 100 y muestra un mensaje en consecuencia.
  echo "Dame un número:" # Solicita al usuario que ingrese un número.
  read n1 # Lee el número ingresado por el usuario.
  if [ "$n1" -le 100 ]; then # Comprueba si el número es menor o igual que 100.
      if [ "$n1" -lt 100 ]; then # Si es menor que 100.
          echo "El número $n1 es menor que 100."
      else
          echo "El número es igual a 100."
      fi
  else
      echo "El número $n1 es mayor que 100."
  fi

..


Bucle while. Se mantiene el bucle mientras la condición sea verdadera.
----------------------------------------------------------------------

.. code-block:: sh

  #!/bin/bash
  # Este script muestra los números del 1 al 100 utilizando un bucle while.
  i=1
  while [ "$i" -le 100 ]; do
      echo "Valor de i: $i"
      i=$((i + 1))
  done

..


Bucle until. Se mantiene el bucle mientras la condición sea falsa.
------------------------------------------------------------------

.. code-block:: sh

  #!/bin/bash
  # Este script muestra los números del 1 al 100 utilizando un bucle until.
  i=1
  until [ "$i" -ge 101 ]; do
      echo "Valor de i: $i"
      i=$((i + 1))
  done

..


Funciones
---------

.. code-block:: sh

  #!/bin/bash
  # Este script define y llama a una función para sumar dos números.
  suma() {
      echo "Dame un número:"
      read n1
      echo "Dame otro número:"
      read n2
      echo "La suma de $n1 y $n2 es: $(($n1 + $n2))"
  }
  suma

..


Estructura case
---------------

.. code-block:: sh

  #!/bin/bash
  # Este script muestra un menú de opciones y ejecuta la opción seleccionada por el usuario.
  echo "Opción 1. Ver directorio actual"
  echo "Opción 2. Leer /tmp"
  echo "Opción 3. Salir"
  echo "Elige opción: 1, 2 o 3?"
  read opcion
  case $opcion in
      1) pwd ;; # Muestra el directorio actual.
      2) ls /tmp ;; # Muestra el contenido de /tmp.
      3) exit ;; # Sale del script.
      *) echo "No elegiste una opción válida." ;;
  esac

..


Copia de seguridad
------------------

.. code-block:: sh

  #!/bin/bash
  # Este script comprueba si un directorio de usuario existe y, de ser así, lo comprime.
  inicio() {
      echo "Dame usuario:"
      read user
      testear
  }
  testear() {
      if [ -d "/home/$user" ]; then
          echo "El directorio /home/$user existe."
          tar -czvf "$user.tar.gz" "/home/$user"
      else
          echo "El directorio /home/$user no existe."
          echo "El contenido de /home es el siguiente: $(ls /home)"
          inicio
      fi
  }
  inicio

  # En este script, si se utilizan alternativas como: 
  # echo "El contenido de /home es el siguiente:
  # echo `ls /home` o exec ls /home
  # El script se detiene con la ejecución. 

..


Copia de seguridad del usuario
------------------------------

.. code-block:: sh

  #!/bin/bash
  
  backup_directorio() {
      echo "Introduce la ruta del directorio que deseas respaldar:"
      read directorio
  
      if [ -d "$directorio" ]; then
          echo "El directorio $directorio existe."
          echo "Creando copia de seguridad en $HOME/backups/$directorio.tar.gz..."
          tar -czvf "$HOME/backups/$directorio.tar.gz" "$directorio"
          echo "Copia de seguridad creada con éxito."
      else
          echo "El directorio $directorio no existe."
          echo "Por favor, asegúrate de que la ruta sea correcta."
      fi
  }
  
  backup_directorio

..












