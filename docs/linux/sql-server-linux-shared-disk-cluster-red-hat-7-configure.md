---
title: Configuración de clúster compartido de Red Hat Enterprise Linux para SQL Server | Microsoft Docs
description: Implementar la alta disponibilidad mediante la configuración de clúster de disco compartido de Red Hat Enterprise Linux para SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: 1801551b179cf7040f1eb5cbaa05d8eb3bebc564
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62634023"
---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Configuración de clúster de disco compartido de Red Hat Enterprise Linux para SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Esta guía proporciona instrucciones para crear un clúster de disco compartido de dos nodos para SQL Server en Red Hat Enterprise Linux. El nivel de agrupación en clústeres se basa en Red Hat Enterprise Linux (RHEL) [complemento de alta disponibilidad](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) construidos sobre [Pacemaker](https://clusterlabs.org/). La instancia de SQL Server está activa en un nodo o la otra.

> [!NOTE] 
> Acceso a Red Hat alta disponibilidad de complementos y documentación requiere una suscripción. 

Como se muestra en el siguiente diagrama, almacenamiento se presenta en dos servidores. Componentes de agrupación en clústeres, Corosync y Pacemaker, coordinan las comunicaciones y administración de recursos. Uno de los servidores tiene la conexión activa a los recursos de almacenamiento y el servidor SQL Server. Cuando Pacemaker detecta un error de los componentes de agrupación en clústeres administran mover los recursos a otro nodo.  

![Red Hat Enterprise Linux 7 compartidos de clúster de disco de SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Para obtener más información sobre la configuración del clúster, las opciones de los agentes de recursos y administración, visite [documentación de referencia RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).


> [!NOTE] 
> En este momento, integración de SQL Server con Pacemaker no es tan acoplamiento como con WSFC en Windows. Desde dentro de SQL, no hay ningún conocimiento sobre la presencia del clúster, todas las orquestaciones está fuera de y Pacemaker controla el servicio como una instancia independiente. También, por ejemplo, sys.dm_os_cluster_properties y clúster DMV sys.dm_os_cluster_nodes no realizará ningún registro.
Para usar una cadena de conexión que apunta a un nombre de servidor de la cadena y no usar la dirección IP, tendrá que registrar la dirección IP usada para crear el recurso IP virtual (como se explica en las secciones siguientes) en su servidor DNS con el nombre de servidor elegido.

Las siguientes secciones se guiarán por los pasos para configurar una solución de clúster de conmutación por error. 

## <a name="prerequisites"></a>Requisitos previos

Para completar el siguiente escenario de extremo a otro, debe tener dos máquinas para implementar el clúster de dos nodos y otro servidor para configurar el servidor NFS. Los pasos siguientes describen cómo se configurará estos servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar y configurar el sistema operativo en cada nodo del clúster

El primer paso es configurar el sistema operativo en los nodos del clúster. Para este tutorial, use RHEL con una suscripción válida para el complemento de alta disponibilidad. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Instalar y configurar SQL Server en cada nodo del clúster

1. Instalar y configurar SQL Server en ambos nodos.  Para obtener instrucciones detalladas, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).

1. Designar un nodo como principal y el otro como secundario para fines de configuración. Usar estos términos para los siguientes elementos en esta guía.  

1. En el nodo secundario, detenga y deshabilite a SQL Server.

   El ejemplo siguiente se detiene y deshabilita el SQL Server: 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> Durante la instalación, se genera para la instancia de SQL Server y se coloca en una clave maestra del servidor `/var/opt/mssql/secrets/machine-key`. En Linux, SQL Server siempre se ejecuta como una cuenta local denominada mssql. Dado que es una cuenta local, su identidad no se comparte entre los nodos. Por lo tanto, deberá copiar la clave de cifrado del nodo principal en cada nodo secundario para cada cuenta local mssql pueda acceder a él para descifrar la clave maestra del servidor. 

1. En el nodo principal, cree un inicio de sesión SQL server para Pacemaker y conceda el permiso de inicio de sesión para ejecutar `sp_server_diagnostics`. Pacemaker usa esta cuenta para comprobar qué nodo se está ejecutando SQL Server. 

   ```bash
   sudo systemctl start mssql-server
   ```

   Conectarse a SQL Server `master` de base de datos con la cuenta de administrador y ejecute lo siguiente:

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   Como alternativa, puede establecer los permisos con más detalle. El inicio de sesión de Pacemaker requiere `VIEW SERVER STATE` para consultar el estado de mantenimiento con sp_server_diagnostics, `setupadmin` y `ALTER ANY LINKED SERVER` para actualizar el nombre de instancia FCI con el nombre del recurso mediante la ejecución sp_dropserver y sp_addserver. 

1. En el nodo principal, detenga y deshabilite a SQL Server. 

1. Configurar el archivo de hosts para cada nodo del clúster. El archivo de host debe incluir la dirección IP y el nombre de cada nodo del clúster. 

    Compruebe la dirección IP para cada nodo. El siguiente script muestra la dirección IP del nodo actual. 

   ```bash
   sudo ip addr show
   ```

   Establezca el nombre del equipo en cada nodo. Asigne a cada nodo un nombre único que es de 15 caracteres o menos. Establece el nombre del equipo mediante la adición a `/etc/hosts`. El siguiente script le permite editar `/etc/hosts` con `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```
   El ejemplo siguiente muestra `/etc/hosts` con adiciones de dos nodos denominados `sqlfcivm1` y `sqlfcivm2`.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

En la siguiente sección configurará el almacenamiento compartido y mover los archivos de base de datos a la que el almacenamiento. 

## <a name="configure-shared-storage-and-move-database-files"></a>Configurar el almacenamiento compartido y mover archivos de base de datos 

Hay una variedad de soluciones para proporcionar almacenamiento compartido. Este tutorial muestra cómo configurar el almacenamiento compartido NFS. Se recomienda seguir los procedimientos recomendados y utilizar Kerberos para proteger NFS (puede encontrar un ejemplo aquí: https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/). 

>[!Warning]
>Si no lo protegen NFS, a continuación, cualquier persona que puede tener acceso a la red y suplantar la identidad de la dirección IP de un nodo de SQL podrán acceder a los archivos de datos. Como siempre, asegúrese de modelamos amenazas de su sistema antes de usarlo en producción. Otra opción de almacenamiento es usar el recurso compartido de archivos SMB.

### <a name="configure-shared-storage-with-nfs"></a>Configurar el almacenamiento compartido NFS

> [!IMPORTANT] 
> Hospedaje de archivos de base de datos en un servidor NFS con la versión < 4 no se admite en esta versión. Esto incluye el uso de NFS para agrupación en clústeres, así como las bases de datos en instancias no clúster de conmutación por error de disco compartido. Estamos trabajando para habilitar otras versiones de servidor NFS en las próximas versiones. 

En el servidor NFS, realice lo siguiente:

1. Instalar `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Habilitar e iniciar `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. Habilitar e iniciar `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  Editar `/etc/exports` para exportar el directorio que desea compartir. Necesita 1 línea para cada recurso compartido que desee. Por ejemplo: 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. Exportar los recursos compartidos

   ```bash
   sudo exportfs -rav
   ```

1. Compruebe que las rutas de acceso compartido o exportar, ejecutar desde el servidor NFS

   ```bash
   sudo showmount -e
   ```

1. Agregar excepción de SELinux

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

1.  Instalar `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Abra el firewall de los clientes y el servidor NFS

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. Compruebe que puede ver los recursos compartidos de NFS en los equipos cliente

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. Repita estos pasos en todos los nodos del clúster.

Para obtener más información sobre el uso de NFS, consulte los siguientes recursos:

* [NFS servidores y firewalld | Stack Exchange](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [Montaje de un volumen NFS | Guía de administradores de red de Linux](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [Configuración del servidor NFS | Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/nfs-serverconfig)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>Montar el directorio de archivos de base de datos para que apunte al almacenamiento compartido

1.  **En el nodo principal solo**, guardar los archivos de base de datos en una ubicación temporal. El siguiente script, crea un nuevo directorio temporal, copia los archivos de base de datos en el nuevo directorio y quita los archivos de base de datos antiguos. Como SQL Server se ejecuta como usuario local mssql, deberá asegurarse de que después de transferencia de datos para el recurso compartido montado, usuario local tiene acceso de lectura y escritura al recurso compartido. 

   ``` 
   $ sudo su mssql
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
>Si usa un recurso de sistema de archivos (FS) como se recomienda aquí, no hay ninguna necesidad de conservar el comando de montaje en/etc/fstab. Pacemaker se encargará de la carpeta de montaje cuando se inicia el recurso de clúster de FS. Con la Ayuda de la barrera, se asegurará que la FS nunca se monta dos veces. 

1.  Ejecute `mount -a` comando del sistema actualizar las rutas de acceso montados.  

1.  Copie los archivos de base de datos y registro que guardó en `/var/opt/mssql/tmp` para el recurso compartido montado recién `/var/opt/mssql/data`. Esto solo debe hacerse **en el nodo principal**. Asegúrese de conceder permisos de lectura y escritura al usuario local 'mssql'.

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  Compruebe que SQL Server se inicia correctamente con la nueva ruta de acceso. Hacer esto en cada nodo. En este momento sólo un nodo debe ejecutar SQL Server a la vez. No pueden ambos ejecutar al mismo tiempo ya que ambos intentará tener acceso a los archivos de datos al mismo tiempo (para evitar accidentalmente iniciar SQL Server en ambos nodos, use un recurso de clúster del sistema de archivos para asegurarse de que no se monta el recurso compartido de dos veces por los diferentes nodos). Los siguientes comandos iniciar SQL Server, comprueban el estado y, a continuación, detener SQL Server.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
En este punto, ambas instancias de SQL Server configuradas para ejecutarse con los archivos de base de datos en el almacenamiento compartido. El siguiente paso es configurar SQL Server para Pacemaker. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalación y configuración de Pacemaker en cada nodo del clúster


2. En ambos nodos del clúster, cree un archivo para almacenar el nombre de usuario de SQL Server y la contraseña para el inicio de sesión de Pacemaker. El comando siguiente crea y rellena este archivo:

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. En ambos nodos del clúster, abra los puertos de firewall de Pacemaker. Para abrir estos puertos con `firewalld`, ejecute el comando siguiente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Si usa otro firewall que no tiene una configuración de alta disponibilidad integrada, los puertos siguientes es necesario abrir para que Pacemaker pueda comunicarse con otros nodos del clúster
   >
   > * TCP: Puertos 2224, 3121, 21064
   > * UDP: Puerto 5405

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
   sudo pcs cluster auth <nodeName1 nodeName2 ...> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>
   sudo pcs cluster start --all
   ```

   > Complemento de alta disponibilidad de RHEL tiene agentes de vallado de KVM y VMWare. Vallado debe deshabilitarse en todos los demás hipervisores. No se recomienda deshabilitar agentes de barrera en entornos de producción. A partir de período de tiempo, no hay ningún agente de barrera para entornos Hyper-v o en la nube. Si está ejecutando una de estas configuraciones, deberá deshabilitar la barrera. \**NO se recomienda en un sistema de producción.**

   El siguiente comando deshabilita a los agentes de barrera.

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. Configurar los recursos de clúster de SQL Server, el sistema de archivos y recursos IP virtuales e inserte la configuración en el clúster. Necesita la siguiente información:

   - **Nombre del recurso SQL Server**: Un nombre para el recurso de SQL Server en clúster. 
   - **Nombre del recurso IP de flotante**: Un nombre para el recurso de dirección IP virtual.
   - **Dirección IP**: La dirección IP que los clientes usarán para conectarse a la instancia en clúster de SQL Server. 
   - **Nombre del recurso del sistema de archivos**: Un nombre para el recurso de sistema de archivos.
   - **device**: El recurso compartido NFS ruta de acceso
   - **device**: La ruta de acceso local que está montado en el recurso compartido
   - **fstype**: Tipo de recurso compartido de archivo (es decir, nfs)

   Actualice los valores de la siguiente secuencia de comandos para su entorno. Ejecutar en un nodo para configurar e iniciar el servicio en clúster.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   Por ejemplo, el script siguiente crea un recurso de SQL Server en clúster denominado `mssqlha`y un recurso IP flotante con dirección IP `10.0.0.99`. También crea un recurso del sistema de archivos y agrega restricciones, por lo que todos los recursos se colocarán en el mismo nodo que el recurso de SQL. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   Una vez que se inserta la configuración, se iniciará SQL Server en un nodo. 

3. Compruebe que se inició SQL Server. 

   ```bash
   sudo pcs status 
   ```

   Los ejemplos siguientes muestran los resultados cuando Pacemaker se ha iniciado correctamente una instancia agrupada de SQL Server. 

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

* [Desde el principio del clúster](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Guía de Pacemaker

## <a name="next-steps"></a>Pasos siguientes

[Usar SQL Server en clúster de disco compartido de Red Hat Enterprise Linux](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
