# Simulacro del examen RHCSA 
![version](https://img.shields.io/badge/Version-1.7-green)
![revision](https://img.shields.io/badge/Revision%20progress-85%25-yellow)
![examen-version](https://img.shields.io/badge/RHCSA-8-red)

Realiza la tarea expuesta en cada apartado y haz clic en "Mostrar comando" para ver un ejemplo de como realizar la tarea solicitada correctamente.

![RHCSALogo](https://www.tcc-consulting.com.hk/wp-content/uploads/2021/05/RED-HAT-LOGO-RHCSA-EX200.png)

## Índice

1. [IPv6](#id1)
2. [Gestion y administración de interfaces de red](#id2)
3. [Redhat Subscription manager](#id3)
4. [Gestor de paquetes yum](#id4)
5. [Control de servicios con systemctl](#id5)
6. [Reestablecer la password del usuario root](#id6)
7. [Gestion de discos](#id7)
8. [Almacenamiento en capas con Stratis](#id8)
9. [Compresion de almacenamiento con VDO](#id9)
10. [NFS](#id10)
11. [Comando timedatectl](#id11)
12. [chronyd](#id12)
13. [Journal del sistema ](#id13)
14. [Gestionando la seguridad del sistema con SELinux](#id14)
15. [Administración y gestión del Firewall, con firewall-cmd](#id15)
16. [Uso de SUDO](#id16)
17. [Gestion de Usuarios y grupos](#id17)
18. [Permisos especiales](#id18)
19. [Gestion y administracion de procesos](#id19)
20. [Perfiles de sintonización (tune profile)](#id20)
21. [Ficheros y directorios temporales](#id21)
22. [Containers con Podman](#id22)

<div id='id1' />

## 1. IPv6

1. Hacer ping a IPv6 
    <details>
      <summary>Mostrar comando</summary>

      <pre>ping6 -c5 fe80::5054:ff:fe57:b57d%enp1s0</pre>
    </details>

## 2. Gestion y administración de interfaces de red

1. Agregar una conexion secundaria con ip 192.168.100.191/24 y gateway 192.168.100.1
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      nmcli connection add con-name second type ethernet ifname enp1s0 ip4 192.168.100.191/24 gw4 192.168.100.1
      </pre>
    </details>

2. Modificar una conexion agregandole el dns 8.8.8.8
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      nmcli conn mod second +ipv4.dns 8.8.8.8
      </pre>
    </details>

3.  Establecer una interfaz en modo autoconnect
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      nmcli con mod second connection.autoconnect yes
      </pre>
    </details>

4.  Editar una conexion en modo interactivo
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      nmcli connection edit enp1s0
      </pre>
    </details>

5. Mostrar los permisos del usuario
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      nmcli general permissions
      </pre>
    </details>

<div id='id3' />

## 3. Redhat Subscription manager

1. Registrar el host en el servicio de administración de suscripciones
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      subscription-manager register
      </pre>
    </details>

2. Listar información de productos y suscripciones disponibles
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      subscription-manager list --available
      </pre>
    </details>

3. Adjuntar una subscripción especifica usando un pool ID
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      subscription-manager attach --pool=$POOLID
      </pre>
    </details>

4. Desregistrar el sistema
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      subscription-manager unregister
      </pre>
    </details>

5. Mostrar repositorios que el sistema tiene derecho a usar
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      subscription-manager repos --list-enabled
      </pre>
    </details>

<div id='id4' />

## 4. Gestor de paquetes yum

1. Listar el paquete httpd
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum list 'httpd'
      </pre>
    </details>

2. Buscar el paquete 'nginx'
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum search 'nginx'
      yum search all 'nginx'
      </pre>
    </details>

3. Ver informacion de un paquete de 'nginx'
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum info 'nginx-all-modules'
      </pre>
    </details>

4. Listar los grupos de paquetes
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum group list
      yum group list hidden
      </pre>
    </details>

5. Ver historial de yum
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum history
      </pre>
    </details>

6. Ver información de una instalacion/actualizacion usando el ID obtenido en el historial
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum history info 10
      </pre>
    </details>

7. Deshacer una instalacion usando el ID obtenido en el historial
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum history undo 10
      </pre>
    </details>

8. Indicar el fichero de configuración de yum
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      /etc/yum.conf
      </pre>
    </details>

9. Realizar la configuracion basica de un repositorio
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      # Se crea un fichero en /etc/yum.repos.d/
      vi /etc/yum.repos.d/basic.repo
      # Se agrega el siguiente contenido
      [nombre-repo]  
      name = nombre repo  
      baseurl = https://fakewebsite.com/repositories/nombre-repo  
      enabled = 1  
      gpgcheck = 0  
      gpgkey = file://etc/pki/rpm-gpg/el-nombre-de-la-key  
      </pre>
    </details>

10. Limpiar cache de repositorios de yum y visualizar los repositorios existentes
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum clean all
      yum repolist
      </pre>
    </details>

11. Importar llave GPG de un repositorio
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      rpm --import https://fakewebsite.com/repositories/gpg-key
      # Se importa la key a /etc/pki/rpm-gpg
      </pre>
    </details>

### 4.1 Modulos yum

1. Listar modulos
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum module list
      </pre>
    </details>

2. Instalar un modulo especifico
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum module install module_name:version
      </pre>
    </details>

<div id='id5' />

## 5. Control de servicios con systemctl

1. Ver el contenido de un unit-file
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl cat sshd.service
      </pre>
    </details>

2. Ver todas las unidades tipo service en fallo
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl --failed -t service --all
      </pre>
    </details>

3. Enmascarar un servicio (desactivarlo completamente)
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl mask --now firewalld
      </pre>
    </details>

4. Desenmascarar un servicio
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl unmask firewalld
      </pre>
    </details>

5. Cambiar el target del sistema a modo consola
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl isolate multi-user.target  
      </pre>
    </details>

6. Cambiar el target del sistema a modo grafico
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl isolate graphical.target
      </pre>
    </details>

7. Ver el target del sistema por defecto
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl get-default
      </pre>
    </details>

8. Establecer un target por defecto
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl set-default multi-user
      </pre>
    </details>

<div id='id6' />

## 6. Reestablecer la password del usuario root

1. Reestablece la contraseña del usuario root a 'rhcsa' empezando el proceso desde el arranque
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      Tras enceder el host, editar el grub presionando: 'e'  
      Añadir el parametro: rd.break al final de la linea que empieza con: linux
      Montar el sistema de archivos / en rw mode: mount -o rw,remount /sysroot  
      Enjaular /sysroot: chroot /sysroot  
      Cambiar la password de root a rhcsa: passwd root  
      Crear un archivo para indicar a selinux que haga un retiquetado: touch /.autorelabel  
      Reiniciar: reboot 
      </pre>
    </details>

<div id='id7' />

## 7. Gestion de discos

1. Ver los puntos de montaje con sus filesystems y paths
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      lsblk -fp
      </pre>
    </details>

2. Listar los comandos de creacion de particiones y formateo de discos
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      fdisk
      gdisk
      parted
      </pre>
    </details>

3. Indicar el fichero del sistema donde se configuran los puntos de montaje y los tipos de formatos admitidos
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      /etc/fstab  

      Ejemplos de formatos en fstab:  
      1. UUID=${UID} /mnt1 xfs defautls 0 0
      2. LABEL=${LABEL}  /mnt2 xfs defautls 0 0
      3. /dev/mapper/${VG}${LV} /mnt3 xfs defautls 0 0
      4. /dev/sda  /mnt4 xfs defautls 0 0

      </pre>
    </details>

4. Crear una nueva swap de 500MB y activarla
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      #Crear particion para swap
      fdisk /dev/vdb
      Nueva particion: n
      Tipo de particion primaria: p
      Numero de particion: 1
      Primer sector: predeterminado
      Ultimo sector: +500M
      Indicar tipo de sistema de archivos: t
      Tipo Linux Swap: 82
      Guardar cambios: w
      
      #Formatear como swap  
      mkswap /dev/vdb1
      
      #Montar swap  
      swapon /dev/vdb1

      #Crear entrada en fstab
      echo "/dev/vdb1 none swap defaults 0 0" >> /etc/fstab
      </pre>
    </details>


5. Establecer prioridad 10 a la nueva swap y 5 a la antigua
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      vi/etc/fstab  
      #Entre mayor sea el numero, mayor prioridad  
      /dev/mapper/rhel_rhcsa--master-swap none    swap    pri=5        0 0
      /dev/vdb1                           none    swap    pri=10       0 0
      </pre>
    </details>

6. Visualizar los discos SWAP y comprobar que la prioridad establecidad en el punto anterior esta aplicada
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      swapon --show
      </pre>
    </details>

### 7.1. Logical volume management: LV y VG 

1. Crear disco para usar como lvm con parted
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      parted /dev/vdb mklabel msdos  
      parted /dev/vdb mkpart primary 1M 500M  
      parted /dev/vdb print  
      parted /dev/vdb set 1 lvm on  
      </pre>
    </details>

2. Crear disco para usar como lvm con fdisk
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      fdisk /dev/vdb  
      Nueva particion: n  
      Particion primaria: p  
      Inicio: predeterminado  
      Fin: +500M  
      Indicar tipo de particion: t  
      Indicar tipo lvm: 8e  
      Guardar y salir: w
      </pre>
    </details>

3. ¿Que son los Physical Extend (PE)?
    <details>
      <summary>Mostrar respuesta</summary>

      <pre>
      Es la cantidad de veces en la que se divide un Volume Group. Esta información se puede ver al ejecutar el comando vgdisplay  
      PE Size               4,00 MiB  
      Total PE              242  
      Alloc PE / Size       0 / 0   
      Free  PE / Size       242 / 968,00 MiB  
      </pre>
    </details>

4. Crear un lvm indicando MB o PE (Extents)
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      lvcreate --name logicalvolumename volumegroupname -L 250M  
      lvcreate --name logicalvolumename volumegroupname --extents 10  

      Si cada physical extent es de 4mb, entonces 10*4, el lvm será de 40M  
      </pre>
    </details>

5. Extender un volumen group
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      vgextend vg01 /dev/sdc  
      </pre>
    </details>

6. Extender un logical volume indicando megabytes
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      lvextend /dev/vg01/lv02 -L +100M --resizefs --test  
      lvextend /dev/vg01/lv02 -L +100M --resizefs 
      </pre>
    </details>

7. Extender un logical volume indicando extends
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      lvextend /dev/vg01/lv02 --extents +25 --resizefs --test   
      lvextend /dev/vg01/lv02 --extents +25 --resizefs
      </pre>
    </details>

8. Extender un logical volume indicando espacio libre
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      lvextend /dev/vg01/lv02 -l +10%FREE --resizefs --test  
      lvextend /dev/vg01/lv02 -l +10%FREE --resizefs
      </pre>
    </details>
 
9. Eliminar un physical volume de un volume group
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      pvmove /dev/vbd1  
      vgreduce vg01 /dev/vbd1  
      pvremove /dev/vbd1  
      </pre>
    </details>

10. Reducir un logical volume
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      lvreduce /dev/vg01/lv01 -L 150M --resizefs --test  
      lvreduce /dev/vg01/lv01 -L 150M --resizefs
      </pre>
    </details>

11. Comando a ejecutar tras hacer cambios en las particiones
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      partprobe --summary
      </pre>
    </details>


<div id='id8' />

## 8. Almacenamiento en capas con Stratis

1. Instalar stratis
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum install stratis-cli stratisd
      </pre>
    </details>

2. Crear un pool y listar los pools
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      stratis pool create labpool1 /dev/vdb /dev/vdc  
      stratis pool list  
      </pre>
    </details>

3. Añadir un disco a un pool existente
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      stratis pool add-data labpool1 /dev/vdd
      </pre>
    </details>

4. Destruir un pool
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      stratis pool destroy labpool1  
      </pre>
    </details>

5. Crear filesystem y listar los filesystems
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      stratis filesystem create labpool1 fs1  
      stratis filesystem list  
      </pre>
    </details>

6. Indicar directorio donde estan los filesystems
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      /dev/stratis/${pool-name}/${filesystem-name}
      
      </pre>
    </details>

7. Crear un snapshot de un filesystem
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      stratis filesystem snapshot labpool1 fs1 fs1-snapshot
      </pre>
    </details>

8. Establecer unidad stratis para que se monte en el arranque 
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      #Obtenemos el UUID del device
      lsblk --output=UUID /dev/stratis/${pool-name}/${filesystem-name}

      echo "UUID=105e8e96-2f87-4418-b8d6-0616b69b4410 /dirStratis xfs defaults,x-systemd.requires=stratisd.service" >> /etc/fstab
      </pre>
    </details>

9. Recuperar un filesystem de un snapshot
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      #Obtenemos el UUID del device
      lsblk --output=UUID /dev/stratis/${pool-name}/${filesystem-name}

      echo "UUID=105e8e96-2f87-4418-b8d6-0616b69b4410 /dirStratis xfs defaults,x-systemd.requires=stratisd.service" >> /etc/fstab
      </pre>
    </details>


<div id='id9' />

## 9. Compresion de almacenamiento con VDO

1. Instalar VDO
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum install vdo kmod-kvdo
      </pre>
    </details>


2. Crear un volumen VDO
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      vdo create --name volume-vdo1 --device /dev/sda --vdoLogicalSize 20G 
      </pre>
    </details>

3. Ver volumenes y su estado
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      vdo list  
      vdo status  
      </pre>
    </details>

4. Formatear y montar volumen vdo
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      mkfs.xfs /dev/mapper/volumen-vdo1  
      lsblk --output=UUID /dev/mapper/volume-vdo1  
      echo "UUID=bde4ea16-8f5c-42da-b45d-c1964cae89b2 /devxfs defaults,x-systemd.requires=vdo.service 0 0" >> /etc/fstab
      </pre>
    </details>

5. Ver estado de un vdo
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      vdostats --human-readable
      </pre>
    </details>

<div id='id10' />

## 10. NFS

1. Establecer configuraciones de NFS con nfsconf
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      nfsconf --set nfsd vers2 y  
      nfsconf --set nfsd vers3 n  
      nfsconf --unset nfsd vers2  
      nfsconf --set nfsd vers2 n  
      </pre>
    </details>

2. Ver recursos NFS compartidos en un servidor
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      showmount -e rhcsa-master.labrhel.com  
      </pre>
    </details>

3. Automatizar montaje NFS - indirecto
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      yum install autofs  
      systemctl --now enable autofs  
      
      vi /etc/auto.master.d/public.autofs   
      /public /etc/directpublic.test  
      
      /etc/directpublic.test  
      nfs -rw,sync rhcsa-master.labrhel.com:/srv/nfs  
      systemctl restart autofs
      # A continuacion si se accede a /public/nfs autofs lee el fichero
      # /etc/auto.master.d/public.autofs  y aplica las reglas que se 
      # definan en /etc/directpublic.test, es decir, se monta:  
      # rhcsa-master.labrhel.com:/srv/nfs en modo rw
      </pre>
    </details>

4. Automatizar montaje NFS - directo
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      vi /etc/auto.master.d/public.autofs  
      /- /etc/indirectpublic.test  
      
      vi /etc/indirectpublic.test  
      /mnt/nfs -rw,sync rhcsa-master.labrhel.com:/srv
      systemctl restart autofs
      # A continuación el recurso /srv se monta automaticamente en
      # /mnt/nfs
      </pre>
    </details>


<div id='id11' />

## 11. Comando timedatectl

1. Listar y establecer timezone
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      timedatectl list-timezones
      timedatectl set-timezone Africa/Ouagadougou
      </pre>
    </details>

2. Establecer la hora a: 09:30:10
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      timedatectl set-time 09:30:10
      </pre>
    </details>

3. Activar NTP service y verificar si esta sincronizado
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      timedatectl set-ntp true
      timedatectl show | grep NTPSynchronized=yes
      </pre>
    </details>

<div id='id12' />

## 12. chronyd

1. Ver el estado de sincronizacion de chronyc
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      chronyc tracking  
      chronyc sources -v  
      </pre>
    </details>

2. Lanzar el wizard de seleccion timezone
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      tzselect
      </pre>
    </details>

<div id='id13' />

## 13. Journal del sistema 

1. Indicar el fichero de configuración del Journal
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      /etc/systemd/journal.conf
      </pre>
    </details>

2. Ver todos los criticals,warnings,errores,etc... del Journal
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      journalctl -p [emerg|alert|crit|err|warning|notice|info|debug]  
      Ejemplo para chronyd: journalctl -u chronyd -p err  
      </pre>
    </details>

3. Ver errores del Journal especificando una fecha de inicio y final
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      journalctl -p err --since "2022-01-31 09:00:00" --until "2022-01-31 09:30:00"
      </pre>
    </details>

4. Indicar los filtros posibles al visualizar el journal
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      Tenemos distintos tipos de filtros:
      journalctl _PID=1000  
      journalctl _UID=0  
      journalctl _COMM=command  
      journalctl _EXE=ejecutablepath  
      journalctl _SYSTEMD_UNIT=sshd.service  

      </pre>
    </details>

5. Guardar un mensaje en el log indicando la prioridad 
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      logger -p local7.error "Esto es un error"
      </pre>
    </details>

<div id='id14' />

## 14. Gestionando la seguridad del sistema con SELinux

1. Ver contextos de seguridad de SELiunx
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      semanage fcontext -l
      </pre>
    </details>

2. Ver el contexto de seguridad de los ficheros:  
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      ls -lZ  
      
      Se muestra:  
      
      drwxr-xr-x.  6 root     root     system_u:object_r:etc_t:s0                     70 jul 12 11:05 X11
      -rw-r--r--.  1 root     root     system_u:object_r:etc_t:s0                    642 dic  9  2016 xattr.conf
      drwxr-xr-x.  4 root     root     system_u:object_r:etc_t:s0                     38 jul 12 11:05 xdg

      Sintaxis del contexto: user:role:tipo:label  

      </pre>
    </details>

3. Cambiar modo de funcionamiento de SELinux
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      setenforce [0|1]  
      vi /etc/selinux/config  
      # 0 desactiva temporalmente
      # 1 activa temporalmente
      # editar el fichero y modificar el parametro SELINUX=[enforcing|permissive|disabled]
      </pre>
    </details>

4. Aplicar un contexto de seguridad especifico a un directorio (temporal)
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      chcon -t httpd_sys_content_t /directorio
      # Si se hace un touch /.autorelabel se pierde el contexto asignado
      # Si se hace un restorecon -v /directorio tambien se pierde el contexto asignado
      </pre>
    </details>

5. Restaura contexto de seguridad SELinux en un directorio
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      restorecon -v /directorio
      </pre>
    </details>

6. Visualizar el estado de los Booleans de SELinux
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      getsebool -a 
      </pre>
    </details>

7. Ver informacion detallada de los boolean de SELinux
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      semanage boolean -l
      </pre>
    </details>

8. Activar o desactivar un boolean
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      setsebool -P abrt_anon_write on .
      </pre>
    </details>

9. Aplicar un contexto de seguridad a un directorio y que este se mantenga tras hacer el autorelabel de SELinux
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      semanage fcontext -a -t httpd_sys_content_t /directorio
      </pre>
    </details>

10. Ver errores de SELinux
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      sealert -a /var/log/audit/audit.log  
      ausearch -m AVC -ts recent
      </pre>
    </details>

11. Ver los registros de los objetos de tipo puerto (port) en SELinux
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      semanage port --list
      </pre>
    </details>

12. Agregar el puerto 1009 en SELinux para Apache
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      semanage port --add --type http_port_t --proto tcp 1009
      </pre>
    </details>

<div id='id15' />

## 15. Administración y gestión del Firewall

1. Agregar el servicio https permanentemente
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      firewall-cmd --permanent --add-service=https
      </pre>
    </details>

2. Eliminar un servicio permanentemente
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      firewall-cmd --permanent --remove-service=https  
      </pre>
    </details>

3. Agregar un puerto permanentemente
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      firewall-cmd --permanent --add-port=1009/tcp  
      </pre>
    </details>

4. Recargar la configuracion
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      firewall-cmd --reload  
      </pre>
    </details>

5. Listar la configuración de la zona activa
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      firewall-cmd --list-all
      </pre>
    </details>

6. Listar información de todas las zonas
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      firewall-cmd --list-all-zones
      </pre>
    </details>

<div id='id16' />

## 16. Uso de SUDO

1. Configurar un usuario para que no se le pida contraseña al usar sudo
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      cd /etc/sudoers.d/  
      echo "david ALL=(ALL) NOPASSWD: ALL" >> david_user  

      </pre>
    </details>

2. Configurar un grupo para que sus usuarios tengan permisos sudo
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      cd /etc/sudoers.d/  
      echo "%admins ALL=(ALL) ALL" >> admins_group  

      </pre>
    </details>

<div id='id17' />

## 17. Gestion de Usuarios y grupos

1. Listar los comandos para gestionar usuarios y grupos
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      # Estos son algunos de los comandos con los que se gestionan los grupos y usuarios
      usermod  
      useradd  
      gpasswd  
      groupadd  
      groupdel  
      </pre>
    </details>

2. Observando la explicación del comando chage configura que la contraseña de un usuario tenga: minimo 2 dias antes de cambiarla, maximo, 1 mes para cambiarla, le avise 2 dias antes de la expiracion, y quede inactiva despues de 1 dia.
    ![image](images/chagecommand-explanation.png)
    <details>
      <summary>Mostrar comando</summary>
      
      <pre>
      chage -m 2 -M 31 -W 2 -I 1 user
      </pre>
    </details>

3. Configura la cuenta de un usuario para que su contraseña caduque el 31 de diciembre de 2022
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      chage -E 2022-12-31 user
      </pre>
    </details>

4. Configura una cuenta par aque esta quede bloqueada el 30 de Julio de 2023
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      usermod --lock --expiredate 2023-07-30 david  
      </pre>
    </details>

<div id='id18' />

## 18. Permisos especiales

Puedes obtener más información de esta apartado [en esta entrada](https://deividsdocs.wordpress.com/2015/06/21/setuid-setgid-y-sticky-bit/)

1. Agrega y quita permisos de setuid a un fichero usando notación numerica (octal) y simbolica.
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      # El permiso SetUID en un archivo provoca que cualquier usuario que ejecute el fichero obtenga los  permisos del propietario del fichero

      chmod u+s file.sh  
      chmod 4700 file.sh  

      chmod u-s file.sh  
      </pre>
    </details>

2. Agrega y quita permisos de setgid en un fichero y un directorio, usando notación numerica (octal) y simbolica
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      # En un fichero es similar a SetUID, trabaja dando los permisos del grupo al usuario que ejecuta el archivo  
      # En un directorio actúa estableciendo siempre el grupo del propietario como grupo para todos los ficheros/directorios que se creen dentro del mismo  

      chmod g+s file.sh  
      chmod 2700 file.sh  

      chmod g+s dir  
      chmod 2700 dir  

      chmod g-s [ dir | file.sh ]  

      </pre>
    </details>

3. Agrega y quita permisos de stickybit a un fichero usando notación numerica (octal) y simbolica.
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      # El sticky bit se utiliza en directorios compartidos, es decir, directorios en los que muchos usuarios pueden escribir, y como bien sabemos si un usuario puede escribir en un directorio también puede borrar aunque no sea propietario del archivo que borra.

      chmod o+t directorio  
      chmod 1700 directorio

      chmod o-t directorio  

      </pre>
    </details>

<div id='id19' />

## 19. Gestion y administracion de procesos

1. Mata la sesion de usuario 
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      pkill -t tty\3  
      pkill -SIGKILL -t pts/2

      </pre>
    </details>

2. Arrancar un proceso con el valor nice 15
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      nice -n 15 process.sh
      </pre>
    </details>

3. Modificar el valor nice actual de un proceso a -10 indicando el PID
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      renice -n -10 -p 132
      </pre>
    </details>

<div id='id20' />

## 20. Perfiles de sintonización (tune profile)

4. Instalar tuned
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      Instalar tuned  
      </pre>
    </details>

5. Comando de gestion de perfiles
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      tune-adm
      </pre>
    </details>

<div id='id21' />

## 21. Ficheros y directorios temporales

1. Cuales son los directorios gestionados por systemd para ficheros temporales 
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      /etc/tmpfiles.d   
      /usr/lib/tmpfiles.d  
      /run/tmpfiles.d  
      </pre>
    </details>

2. Ver servicio el servicio de limpieza de ficheros temporales
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemctl status systemd-tmpfiles-clean
      </pre>
    </details>

3. Limpiar ficheros temporales con systemd-tmpfiles
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemd-tmpfiles --clean
      </pre>
    </details>

4. Crear directorios temporales
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemd-tmpfiles --create
      </pre>
    </details>

5. Ver configuracion actual de directorios temporales
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      systemd-tmpfiles --cat-config
      </pre>
    </details>

<div id='id22' />

## 22. Containers con Podman

1. Instalar el grupo de paquetes para podman
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      dnf install -y @container-tools
      </pre>
    </details>

2. Buscar una imagen en el registry de redhat
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      podman search registry.redhat.io/mariadb
      </pre>
    </details>

3. Pullear un contenedor desde el registry de redhat
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      podman login  registry.redhat.io
      podman pull registry.redhat.io/rhel8/mariadb-103

      </pre>
    </details>

4. Ver imagenes locales
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      podman images --all
      </pre>
    </details>

5. Inspeccionar una imagen especifica
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      podman inspect 364f5d5eb513
      </pre>
    </details>

6. Lanzar un container como demonio, exponiendo un puerto concreto
    <details>
      <summary>Mostrar comando</summary>

      <pre>
      podman run -d -p 8081:80 --name http fc7e49a0cf98
      </pre>
    </details>

##### Esta pagina no tiene relación alguna con Red Hat ©.
