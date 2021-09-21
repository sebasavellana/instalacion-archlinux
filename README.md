# Instalación de ArchLinux

La distribución ArchLinux está dirigida para usuarios avanzados y su proceso de instalación permite conocer en mayor profundidad como funciona el sistema operativo y las diferentes opciones de configuración.

Esta guía pretendo que sirva de referencia para los alumnos de Sistemas Operativos en Red y Administración de Sistemas Operativos. La wiki de ArchLinux contiene toda la documentación necesaria para realizar la instalación y configuración de ArchLinux. Solo pretendo documentar el proceso de instalación de manera que el alumnado tenga presente lo que va haciendo en cada paso y enlazarlo con los contenidos de los módulos de Sistemas Operativos de los ciclos formativos de Informática.

Al ser un material de uso en clase, se documentará la instalación en una **máquina virtual**

## Creación de la máquina virtual

El primer paso es descargar los médios de instalación (es decir, la ISO) de ArchLinux y se deberá hacer desde un página web www.archlinux.org

Como ArchLinux tiene una política *Rolling Release* cada mes se genera una nueva ISO con los paquetes actualizados hasta el 31 del mes anterior. No suele haber grandes cambios en el proceso pero conviene repasar la wiki para estar al tanto de las novedades.

Siendo alumno de segundo curso no se debe explicar como hacer una máquina virtual. La intención en este tutorial es instalar el sistema operativo con entorno de escritorio por lo que una configuración adecuada serían:
- 15 GiB de disco duro
- 2 núcleos
- Tarjeta de red en modo NAT
- 4 GB de RAM

Toda la información está obtenida de https://wiki.archlinux.org/title/installation_guide

## Proceso de instalación

1 - Arranca la máquina virtual desde la ISO de instalación y en el cargador de arranque selecciona la opción *Arch Linux install medium (x86_64, BIOS)*

2 - El sistema arrancará los procesos mínimos del sistema y presentará un prompt de root en el que introducir comandos y un pequeño texto de ayuda en la parte superior. Si empiezas a teclear verás que por defecto utiliza el teclado inglés. Para pasar al castellano utiliza:
```
loadkeys es
```

3 - Es importante verificar que se tiene conexión a Internet ya que será necesaria para descargar e instalar paquetes. Al estar configurada la VM en modo NAT ya debe tener conectividad pero se debe comprobar con los siguientes comandos:
```bash
# Dirección IP
ip address show

# Tabla de enrutamiento o gateway por defecto
ip route show

# Comprobación de echo con ICMP
ping 8.8.8.8
ping www.google.es
```
4 - La hora del sistema es un parámetro que debe estar correcto para evitar problemas en la navegación ya que los sistemas remotos la utilizan como parámetro para el correcto funcionamiento del protocolo HTTPS y otras aplicaciones. 
El comando `date` devuelve la hora actual del sistema.
Lo habitual es confiar en un servidor de hora en Internet bajo el protocolo NTP *Network Time Protocol* que sincronice la hora automáticamente con el comando:
```
timedatectl set-ntp true
```
5 - Llega uno de los momentos importantes de la instalación del sistema operativo, el momento de particionar el disco duro. En este momento del curso se va a realizar con particionado de manera tradicional (más adelante se utilizarán técnicas avanzadas como LVM) con la siguiente distribución:
- 10 GiB para el sistema de ficheros raíz
- 4 GiB para los directorios personales de los usuarios `/home`
- 1 GiB de partición dedicada a swap
El particionado se puede realizar con dos herramientas `fdisk` y `cfdisk` sobre el dispositivo ubicado en `/dev/sda`
La tabla de particiones puede estar en modo *mbr* (identificado como *dos*) o *gpt*. En este ejemplo, realizaremos la instalación en modo *dos*

Recuerda que con tabla de particiones MBR tienes las siguientes restricciones:
- 4 particiones primarias
- 3 primarias y una extendida, que en su interior tendrá particiones lógicas

Por su parte, el particionado GPT supera estas limitaciones permitiendo hasta 128 particiones primarias.

6 - Una partición requiere un sistema de archivos para poder ser utilizada. Se le pueden dar formatos como el habitual *ext4* o su posible sustituto a futuro  *brtfs* con el comando `mkfs`
```bash
# Formato ext4 a la partición raíz
mkfs.ext4 /dev/sda1

# Formato ext4 a la partición /home
mkfs.ext4 /dev/sda2
```
Hay que dar formato a la partición dedicada a la memoria swap (la cual se puede generar también con un fichero dedicado) con la orden:
```
mkswap /dev/sda3
```

7 - En este momento de la instalación se están lanzando comandos desde el Live CD de instalación pero el objetivo es que el sistema operativo quede instalado en el disco duro.
```
mount /dev/sda1 /mnt
```
Observa lo que hace este comando. Antes de su ejecución, el directorio `/mnt` estaba vacío ya que no había nada en su interior. Una vez ejecutado, tampoco hay nada (realmente un directorio de *journaling* llamado `lost+found`) pero todo archivo y directorio que se cree allí estará en el disco duro donde se va a instalar el sistema.

8 - Este el primer paso tangible de la instalación en que se descarga el sistema base de los repositorios de Arch y los instala en el disco duro, el cual se localiza en el directorio `/mnt` a los ojos del LiveCD.
```
pacstrap /mnt base linux linux-firmware
```
Los paquetes _linux_ y _linux-firmware_ son el kernel del sistema operativo.

9 - Los puntos de montaje persistentes en el sistema se almacenan en el fichero `/etc/fstab`. Una parte de la instalación se puede automatizar con la siguiente orden:
```
genfstab -U /mnt >> /mnt/etc/fstab
```
Observa todo lo que hace el comando:
- Genera el contenido de `/etc/fstab` para la partición ubicada en `/dev/sda1`, la cual está montada en `/mnt`
- Con el operador de redirección `>>` añade en la última línea del fichero `/mnt/etc/fstab` el contenido generado. Observa que el fichero está en `/mnt` ya que es del disco duro _sda_ ya que no es el mismo _fstab_ que encontrarás en el LiveCD.

En este supuesto de instalación hay que añadir una línea para el automontaje del `/home` y de la particion _swap_.

10 - Un **chroot** es una operación que modifica el directorio raíz de manera *aparente* para el proceso en ejecución y los que se ejecuten a posteriori hasta que se salga de la *jaula chroot*.

El _chroot_ se puede realizar en cualquier ubicación de la estructura de ficheros de Linux y desde el directorio que se realice el usuario no podrá subir por encima de ese nivel (con la orden `cd ..` por ejemplo) aunque a nivel físico existan directorios a nivel superior.

Esta técnica se utiliza mucho en servidores FTP (que veréis en el módulo de Servicios en Red).

ArchLinux utiliza un comando propio `arch-chroot` que realiza todos los procesos necesarios para trabajar directamente como si estuviesemos en el disco duro y partiendo desde la raíz en la estructura de ficheros.
```
arch-chroot /mnt
```



11. f
12. f
13. f
14. f
15. f
16. f
17. f
18. f
19. f
20. f
21. f
22. f
23. f
24. f
25. f
26. f
27. f

