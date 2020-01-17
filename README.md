# TCC
En este repositorio se encunetra la practica del tema 2 de la asignatura Técnicas de computación científica de la ETSI Informaticos. Hemos desarrollado un script para la instalación de la herramienta MPI en un clúster de máquinas virtuales con el sistema operativo Linux Debian. Decidimos realizar este script, ya que el profesor Juan Pedro ha comentado que es un proceso complejo y por tanto nos gustaría conocer como funciona y por ende automatizarlo, para simplificar la tarea.
2	Configuración previa de máquinas
Como decíamos en la propuesta la idea principal es la de creación de un clúster de máquinas virtuales basadas en Debian, esta red se interconectará por SSH. La idea del script es que el administrador de sistema se identifique como tal en cualquiera de los equipos de la red ssh y ejecute el script. Además, comprobaríamos el funcionamiento de la configuración ejecutando algunos programas con la herramienta MPI, así como OpenMPI.
Para la instalación de MPI en este clúster debemos generar una red interconectada por SSH e instalar directorio compartido mediante NFS.  
2.1	Creación de red virtual
Para crear la red de máquinas virtuales en la aplicación VirtualBox hemos: 
1.	Generado una “Red solo-anfitrión” (Herramienta > Red > Crear) dejando la configuración por defecto con DHCP. 
2.	Hemos generado en cada maquina virtual un nuevo adaptador para la conexión a la red solo-anfitrión (Configuración > Red > Adaptador sólo-anfitrión > Nombre_Adaptador_Generado_Paso_Anterio)
2.2	Configuración de red SSH
Para generar las conexiones SSH, hemos usado OpenSSH y hemos generado una conexión sin contraseñas:
1.	Configuración de conexiones SSH, lo hemos hecho con OpenSSH, configuración basica. En en el fichero /etc/sshd_conf lo hemos configurado para permitir el acceso como root desde maquinas de la red y autenticación PAM.
2.	Clonación de 5 maquinas virtuales, generando nuevas direcciones mac en las tarjetas, para evitar conflictos.
2.3	Configuración directoria compartido mediante NFS
Tras configurar la conexión mediante SSH de los equipos hemos ejecutado un script auxiliar que se usa de dos scripts que nos genera un directorio compartido mediante NFS, este script usará un fichero de configuración que se le indicará el fichero de donde se va a obtener el fichero de configuración para configurar la maquina servidora y las maquinas clientes. Será en este fichero de configuración donde especificaremos el scrip que usaremos para la instalación de OpenMPI. Los scripts que hemos utilizados son propios, realizados para practica y modificados para adaptarlos.

root@m1:/#./configuracion_cluster.sh configuracion_cluster.conf

Este script utiliza los scripts auxiliares:
-	nfs_server.sh
-	nfs_client.sh
Cada script dispone de un fichero propio de configuración nfs_server.conf y nfs_client.conf respectivamente.
