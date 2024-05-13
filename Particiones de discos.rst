# Herramientas de administración de discos

Las particiones son divisiones lógicas del disco duro que se pueden crear para compartir varios sistemas operativos en un mismo disco duro. Cada partición tendría la estructura lógica correspondiente a su sistema operativo instalado. Podemos optar por crear una o varias particiones, pero el espacio asignado a una partición en un disco debe ser contiguo. El espacio del disco que no pertenezca a ninguna partición será espacio sin asignar.

Desde el punto de vista del usuario, cada partición aparece como un disco distinto con el que trabaja de forma independiente, aunque sean particiones de un mismo disco.

La respuesta sobre cuántas particiones puede tener el disco duro dependerá de la estructura de esa unidad. Para eso necesitarás de un sistema para gestionar particiones. Hay múltiples tipos de particionado, los dos más comunes son:

- MBR (Master Boot Record) o MSDOS: un disco duro puede tener hasta 4 particiones primarias. También puede tener tres primarias y una extendida. La extendida estará compuesta por tantas unidades lógicas como alcance la capacidad del disco (máximo de 32). De las 4 particiones, solo una puede estar definida como activa. Será la que cargue el S.O. cuando se inicie el ordenador. En el primer sector del disco duro se sitúa una tabla de particiones, en una zona llamada MBR (Master Boot Record), ésta incluye toda la configuración de particiones del disco duro; las particiones que hay y su tamaño y un pequeño programa que permite localizar la partición activa, leer su sector de arranque y usarlo para arrancar el sistema informático. Además, el MBR reserva espacio para almacenar las instrucciones del gestor de arranque (boot manager).

El gestor de arranque es el primer programa que se ejecuta justo después de las instrucciones de arranque de la BIOS, y este básicamente se encarga de indicar qué partición tiene las instrucciones para arrancar un sistema operativo, redireccionando el arranque a ésta. En el caso de que tengamos múltiples sistemas operativos instalados en un mismo ordenador, un gestor de arranque puede configurarse para mostrar un menú en el que podremos seleccionar el que queremos arrancar. No siempre tendremos un gestor de arranque en el MBR.

- GPT (GUID Partition Table): En el sistema GPT, las particiones son casi ilimitadas sin importar su relevancia. No hay distinción entre particiones, todas se consideran primarias. En Windows se limita a 128 mientras que GNU/Linux llega a 256. Además, también pueden tener mayor tamaño. Vino a solucionar el problema de las limitaciones de 2 TiB por partición y de 4 TiB por disco del MBR, y tiene mayor seguridad en los datos y arranque más rápido que MBR. Reserva también un espacio al principio del disco donde almacena la tabla de particiones y el gestor de arranque. Este espacio es mayor que en MBR ya que al poder particionar en más trozos necesita más espacio para guarda los datos de todas las particiones. Dentro de este espacio reserva el primer sector (LBA 0) para el también llamado MBR por compatibilidad con equipos con BIOS antiguas.

**NOTA**: En Linux, el gestor de arranque predeterminado es GRUB (Grand Unifier Bootloader) y en Windows, el gestor de arranque es Windows Boot Manager.

Las operaciones básicas que se pueden realizar sobre particiones son:

- Crear partición
- Formatear partición
- Eliminar partición
- Reducir o extender partición

El gran problema que tiene que afrontar el S.O. para gestionar los distintos dispositivos de E/S es la gran cantidad de dispositivos y fabricantes que existen. Linux resuelve este problema tratando todos los dispositivos siguiendo una interface común: la de un fichero, que se puede abrir, escribir, leer y cerrar.

Por lo tanto, para Linux un dispositivo es un fichero especial (localizado en el directorio `/dev` que cuelga del directorio raíz) que en realidad enlaza con el controlador del dispositivo. Así, el fichero `mem` representa la memoria, `hdxx` los dispositivos IDE, `lp` las impresoras por el puerto paralelo, etc. La única diferencia posible entre los dispositivos es que pueden ser de dos tipos: de bloque (ej.: disco duro) o de carácter (ej.: ratón, teclado).

Cada unidad de almacenamiento del ordenador y cada posible partición de esta unidad es considerada como un dispositivo:

- `/dev/hda`, `/dev/hdb`: Unidades IDE maestro y esclavo del primer canal (controladora principal).
- `/dev/hdc`, `/dev/hdd`: Unidades IDE maestro y esclavo del segundo canal (controladora secundaria).
- `/dev/sda`, `/dev/sdb`, …, `/dev/sdh`: Interfaz para discos SCSI, SATA y unidades de conexión USB (unidades FLASH o discos duros externos).
- `/dev/hda1`, `/dev/hda2`, … `/dev/sda1`, `/dev/sda2`: Particiones dentro de la unidad correspondiente.
- `/dev/fd*`: Disqueteras.
- `/dev/scd*` (también conocida como `/dev/sr*`): CD-ROM SCSI o DVD
- `/dev/tty*`: consolas o terminales físicos.

**Nota**: Con la llegada de SATA, en la actualidad se utiliza mayormente `sda` en lugar de `hda` para referirse a discos duros. Donde `sd` quiere decir serial drive.

Por lo menos una partición será asignada al directorio raíz, y el resto de las particiones y unidades se montarán sobre este sistema de ficheros.



