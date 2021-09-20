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

1. Arranca la máquina virtual desde la ISO de instalación y en el cargador de arranque selecciona la opción *Arch Linux install medium (x86_64, BIOS)*
2. El sistema arrancará los procesos mínimos del sistema y presentará un prompt de root en el que introducir comandos y un pequeño texto de ayuda en la parte superior. Si empiezas a teclear verás que por defecto utiliza el teclado inglés. Para pasar al castellano utiliza:
`loadkeys es`
3. Es importante verificar que se tiene conexión a Internet ya que será necesaria para descargar e instalar paquetes. Al estar configurada la VM en modo NAT ya debe tener conectividad pero se debe comprobar con los siguientes comandos:
```bash
# Dirección IP
ip address show

# Tabla de enrutamiento o gateway por defecto
ip route show

# Comprobación de echo con ICMP
ping 8.8.8.8
ping www.google.es
```
4. La hora del sistema es un parámetro que debe estar correcto para evitar problemas en la navegación ya que los sistemas remotos la utilizan como parámetro para el correcto funcionamiento del protocolo HTTPS y otras aplicaciones. El comando `date` devuelve la hora actual del sistema.
Lo habitual es confiar en un servidor de hora en Internet bajo el protocolo NTP *Network Time Protocol* que sincronice la hora automáticamente con el comando:
```
timedatectl set-ntp true
```
5. Este es uno de los momentos críticos de la instalación, el particionado de los discos duros

