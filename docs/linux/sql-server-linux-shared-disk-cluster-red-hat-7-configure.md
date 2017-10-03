---
title: "Configuración de clúster compartido de Red Hat Enterprise Linux para SQL Server | Documentos de Microsoft"
description: "Implementar la alta disponibilidad mediante la configuración de clúster de disco compartido de Red Hat Enterprise Linux para SQL Server."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 1708138f5eeb082f022f78dfb685f333f3f0a17b
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Configuración de clúster de disco compartido de Red Hat Enterprise Linux para SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Esta guía proporciona instrucciones para crear un clúster de disco compartido de dos nodos para SQL Server en Red Hat Enterprise Linux. El nivel de agrupación en clústeres se basa en los servicios de Red Hat Enterprise Linux (RHEL) [complemento HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) construidos sobre [marcapasos](http://clusterlabs.org/). La instancia de SQL Server está activa en un nodo o la otra.

> [!NOTE] 
> Acceso a documentación y HA de Red Hat complemento requiere una suscripción. 

Como muestra el diagrama siguiente se presenta el almacenamiento a dos servidores. Componentes de agrupación en clústeres - Corosync y marcapasos - coordinan las comunicaciones y administración de recursos. Uno de los servidores tiene la conexión activa a los recursos de almacenamiento y el servidor SQL Server. Cuando marcapasos detecta un error de los componentes de agrupación en clústeres administran mover los recursos a otro nodo.  

![Red Hat Enterprise Linux 7 compartido de clúster de disco de SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Para obtener más detalles sobre la configuración del clúster y opciones de agentes de recursos, administración, visite [documentación de referencia RHEL](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).


> [!NOTE] 
> En este momento, la integración de SQL Server con marcapasos no es como acoplamiento como con WSFC en Windows. Desde dentro de SQL, no hay ningún conocimiento sobre la presencia del clúster, todas las orquestaciones está fuera de y marcapasos controla el servicio como una instancia independiente. También, por ejemplo, sys.dm_os_cluster_properties y clúster DMV sys.dm_os_cluster_nodes no van a ningún registro.
Para usar una cadena de conexión que apunta a un nombre de servidor de cadena y no usar la dirección IP, tendrá que registrar en su servidor DNS la dirección IP utilizada para crear el recurso IP virtual (tal y como se explica más adelante) con el nombre del servidor seleccionado.

En las siguientes secciones abordan los pasos necesarios para configurar una solución de clúster de conmutación por error. 

## <a name="prerequisites"></a>Requisitos previos

Para completar el siguiente escenario de extremo a extremo debe tener dos máquinas para implementar el clúster de dos nodos y otro servidor para configurar el servidor NFS. Pasos siguientes describen cómo se configurarán estos servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar y configurar el sistema operativo en cada nodo del clúster

El primer paso es configurar el sistema operativo en los nodos del clúster. Para este tutorial, utilice RHEL con una suscripción válida para el complemento de alta disponibilidad. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Instalar y configurar SQL Server en cada nodo del clúster

1. Instalar y configurar SQL Server en ambos nodos.  Para obtener instrucciones detalladas, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).

1. Designar un nodo como principal y el otro como secundario para fines de configuración. Utilizando estos términos para los siguientes elementos en esta guía.  

1. En el nodo secundario, detenga y deshabilite a SQL Server.

   En el ejemplo siguiente se detiene y deshabilita a SQL Server: 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> Durante la instalación, una clave maestra del servidor se genera para la instancia de SQL Server y se coloca en var/opt/mssql/secretos /-clave del equipo. En Linux, SQL Server siempre se ejecuta como una cuenta local denominada mssql. Dado que es una cuenta local, su identidad no se comparte en todos los nodos. Por lo tanto, debe copiar la clave de cifrado de nodo principal a cada nodo secundario para cada cuenta mssql local pueda acceder a él para descifrar la clave maestra de servidor. 

1. En el nodo principal, cree un inicio de sesión SQL server para marcapasos y conceder el permiso de inicio de sesión para ejecutar `sp_server_diagnostics`. Marcapasos usará esta cuenta para comprobar qué nodo está ejecutando SQL Server. 

   ```bash
   sudo systemctl start mssql-server
   ```

   Conectarse a SQL Server `master` base de datos con la cuenta sa y ejecute lo siguiente:

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   Como alternativa, puede establecer los permisos con más detalle. Requiere que el inicio de sesión marcapasos `VIEW SERVER STATE` para consultar el estado de mantenimiento con sp_server_diagnostics, `setupadmin` y `ALTER ANY LINKED SERVER` para actualizar el nombre de instancia FCI con el nombre del recurso ejecutando sp_dropserver y sp_addserver. 

1. En el nodo principal, detenga y deshabilite a SQL Server. 

1. Configurar el archivo de hosts para cada nodo del clúster. El archivo de host debe incluir la dirección IP y el nombre de cada nodo del clúster. 

    Compruebe la dirección IP para cada nodo. El siguiente script muestra la dirección IP del nodo actual. 

   ```bash
   sudo ip addr show
   ```

   Establecer el nombre del equipo en cada nodo. Asigne a cada nodo un nombre único que es de 15 caracteres o menos. Establece el nombre del equipo mediante la adición a `/etc/hosts`. El siguiente script le permite editar `/etc/hosts` con `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```
   El ejemplo siguiente muestra `/etc/hosts` con las adiciones de dos nodos con el nombre `sqlfcivm1` y `sqlfcivm2`.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

En la siguiente sección configurará el almacenamiento compartido y mover los archivos de base de datos al que el almacenamiento. 

## <a name="configure-shared-storage-and-move-database-files"></a>Configurar el almacenamiento compartido y mover archivos de base de datos 

Hay una variedad de soluciones para proporcionar almacenamiento compartido. Este tutorial muestra cómo configurar almacenamiento compartido con NFS. Se recomienda seguir las prácticas recomendadas y usar Kerberos para proteger NFS (encontrará un ejemplo aquí: https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/). Si no lo hace, a continuación, cualquier persona que tenga acceso a la red y suplantar la identidad de la dirección IP de un nodo SQL podrá acceder a los archivos de datos. Como siempre, asegúrese de que el sistema de modelo de amenaza antes de usarlo en producción. Otra opción de almacenamiento es usar el recurso compartido de archivos SMB.

### <a name="configure-shared-storage-with-nfs"></a>Configurar el almacenamiento compartido con NFS

> [!IMPORTANT] 
> Hospedar los archivos de base de datos en un servidor NFS con la versión < 4 no se admite en esta versión. Esto incluye el uso de NFS para agrupación en clústeres, así como las bases de datos en instancias no clúster de conmutación por error de disco compartido. Estamos trabajando en habilitar otras versiones de servidor NFS en las próximas versiones. 

En el servidor NFS realice lo siguiente:

1. Instale `nfs-utils`.

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Habilitar e iniciar`rpcbind`

   ```bash
   sudo systemctl enable rpcbind && systemctl start rpcbind
   ```

1. Habilitar e iniciar`nfs-server`
 
   ```bash
   systemctl enable nfs-server && systemctl start nfs-server
   ```
 
1.  Editar `/etc/exports` para exportar el directorio que desea compartir. Necesitará 1 línea para cada recurso compartido que desee. Por ejemplo: 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. Exportar los recursos compartidos

   ```bash
   sudo exportfs -rav
   ```

1. Compruebe que las rutas de acceso son compartidos/exportado, ejecutar desde el servidor NFS

   ```bash
   sudo showmount -e
   ```

1. Agregar excepción en SELinux

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. Abra el firewall del servidor.

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurar todos los nodos del clúster para conectarse al almacenamiento compartido NFS

Siga estos pasos en todos los nodos del clúster.

1.  Desde el servidor NFS, instalar`nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Abra el firewall en los clientes y servidor NFS

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. Compruebe que puede ver los recursos compartidos de NFS en equipos cliente

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. Repita estos pasos en todos los nodos del clúster.

Para obtener información adicional sobre el uso de NFS, consulte los siguientes recursos:

* [NFS servidores y firewalld | Intercambio de pila](http://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [Montar un volumen NFS | Guía del Administrador de red de Linux](http://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [Configuración del servidor NFS](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/3/html/Reference_Guide/s1-nfs-server-export.html)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>Montar el directorio de archivos de base de datos para que apunte al almacenamiento compartido

1.  **En el nodo principal solo**, guardar los archivos de base de datos en una ubicación temporal. El siguiente script, crea un nuevo directorio temporal, copia los archivos de base de datos en el nuevo directorio y elimina los archivos antiguos de la base de datos. Cuando SQL Server se ejecuta como usuario local mssql, debe asegurarse de que, después de transferencia de datos para el recurso compartido montado, usuario local tiene acceso de lectura y escritura al recurso compartido. 

   ``` 
   $ su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  En todos los nodos del clúster editar `/etc/fstab` archivo para incluir el comando de montaje.  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   El siguiente script muestra un ejemplo de la edición.  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>Si usa un recurso de sistema de archivos (FS) tal como se recomienda a continuación, no hay ninguna necesidad de conservar el comando de montaje en/etc/fstab. Marcapasos se encargará de la carpeta de montaje cuando se inicia el recurso de clúster de FS. Con la Ayuda de la barrera, hará lo siguiente ensurethe FS nunca se monta dos veces. 

1.  Ejecutar `mount -a` comando para el sistema actualizar las rutas de acceso montados.  

1.  Copie los archivos de base de datos y registro que guardó en `/var/opt/mssql/tmp` al recurso compartido montado recién `/var/opt/mssql/data`. Esto solo debe hacerse **en el nodo principal**. Asegúrese de conceder permisos de lectura y escritura al usuario local 'mssql'.

   ``` 
   $ chown mssql /var/opt/mssql/data
   $ chgrp mssql /var/opt/mssql/data
   $ su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  Validar que SQL Server se inicia correctamente con la nueva ruta de acceso. Hacer esto en cada nodo. En este momento sólo un nodo debe ejecutar SQL Server a la vez. No pueden ambos ejecutar al mismo tiempo ya que ambos intentará tener acceso a los archivos de datos al mismo tiempo (para evitar accidentalmente a partir de SQL Server en ambos nodos, use un recurso de clúster del sistema de archivos para asegurarse de que el recurso compartido no está montado dos veces por los distintos nodos). Los siguientes comandos iniciar SQL Server, comprueban el estado y, a continuación, detener SQL Server.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
En este momento, ambas instancias de SQL Server se configuran para ejecutarse con los archivos de base de datos en el almacenamiento compartido. El siguiente paso es configurar SQL Server para marcapasos. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar y configurar a marcapasos en cada nodo del clúster


2. En ambos nodos del clúster, cree un archivo para almacenar el nombre de usuario de SQL Server y la contraseña para el inicio de sesión de Pacemaker. El comando siguiente crea y rellena este archivo:

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
   sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. En ambos nodos del clúster, abra los puertos de firewall de Pacemaker. Para abrir estos puertos con `firewalld`, ejecute el comando siguiente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Si usa otro firewall que no tiene una configuración de alta disponibilidad integrada, deberán abrirse los puertos siguientes para que Pacemaker pueda comunicarse con otros nodos del clúster.
   >
   > * TCP: puertos 2224, 3121, 21064
   > * UDP: puerto 5405

1. Instale paquetes de Pacemaker en cada nodo.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. Establezca la contraseña para el usuario predeterminado que se crea al instalar paquetes de Pacemaker y Corosync. Use la misma contraseña en ambos nodos. 

   ```bash
   sudo passwd hacluster
   ```

   

3. Habilite e inicie el servicio `pcsd` y Pacemaker. Esto permitirá que los nodos se unan al clúster después del reinicio. Ejecute el comando siguiente en ambos nodos.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Instale el agente de recursos de FCI para SQL Server. Ejecute los comandos siguientes en ambos nodos. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="create-the-cluster"></a>Crear el clúster 

1. En uno de los nodos, cree el clúster.

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 …> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 …>
   sudo pcs cluster start --all
   ```

   > Alta disponibilidad de RHEL complemento tiene agentes de barrera para KVM y VMWare. Barrera debe deshabilitarse en todos los demás hipervisores. No se recomienda deshabilitar agentes de barrera en entornos de producción. A partir de período de tiempo, no hay ningún agente de barrera para entornos de Hyper-v o en la nube. Si está ejecutando una de estas configuraciones, debe deshabilitar la barrera. \**NO se recomienda en un sistema de producción.**

   El siguiente comando deshabilita a los agentes de barrera.

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. Configurar los recursos de clúster de SQL Server, sistema de archivos y recursos IP virtuales e insertar la configuración en el clúster. Necesitará la siguiente información:

   - **Nombre del recurso de SQL Server**: un nombre para el recurso de SQL Server en clúster. 
   - **Valor de tiempo de espera**: el valor de tiempo de espera es la cantidad de tiempo que espera a que el clúster aunque una se conecta un recurso. Para SQL Server, este es el tiempo que espera SQL Server para llevar a cabo para poner el `master` en línea de base de datos.  
   - **Nombre de recurso de IP de flotante**: un nombre para el recurso de dirección IP virtual.
   - **Dirección IP**: la dirección IP que los clientes usarán para conectarse a la instancia en clúster de SQL Server. 
   - **Nombre de recurso del sistema de archivos**: un nombre para el recurso de sistema de archivos.
   - **dispositivo**: ruta de acceso de recursos compartidos de NFS el
   - **dispositivo**: la ruta de acceso local que está montado en el recurso compartido
   - **fsType**: tipo de recurso compartido de archivo (es decir, nfs)

   Actualice los valores de la secuencia de comandos a continuación para su entorno. Ejecutar en un nodo para configurar e iniciar el servicio en clúster.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci op defaults timeout=<timeout_in_seconds>
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   Por ejemplo, el script siguiente crea un recurso de clúster de SQL Server denominado `mssqlha`y un recurso IP flotante con la dirección IP `10.0.0.99`. También crea un recurso de sistema de archivos y agrega restricciones para que todos los recursos están colocados en el mismo nodo que el recurso de SQL. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci op defaults timeout=60s
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   Después de la configuración se inserta, se iniciará SQL Server en un nodo. 

3. Compruebe que SQL Server se ha iniciado. 

   ```bash
   sudo pcs status 
   ```

   Lo ejemplos siguientes se muestra los resultados cuando marcapasos tiene correctamente, inicia una instancia en clúster de SQL Server. 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>Recursos adicionales

* [Clúster desde el principio](http://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Guía de marcapasos

## <a name="next-steps"></a>Pasos siguientes

[Usar SQL Server en clúster de disco compartido de Red Hat Enterprise Linux](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)

