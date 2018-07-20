---
title: 'Configurar la instancia de clúster de conmutación por error: SQL Server en Linux (RHEL) | Microsoft Docs'
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 90235a612617fef28a02f980b349fc15490cba3f
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086157"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>Configurar la instancia de clúster de conmutación por error: SQL Server en Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Una instancia de clúster de conmutación por error de disco compartido de dos nodos de SQL Server proporciona redundancia de nivel de servidor para lograr alta disponibilidad. En este tutorial, obtendrá información sobre cómo crear una instancia de clúster de conmutación por error de dos nodos de SQL Server en Linux. Los pasos específicos que completará incluyen:

> [!div class="checklist"]
> * Instalación y configuración de Linux
> * Instalar y configurar SQL Server
> * Configurar el archivo de hosts
> * Configurar el almacenamiento compartido y mover los archivos de base de datos
> * Instalación y configuración de Pacemaker en cada nodo del clúster
> * Configurar la instancia de clúster de conmutación por error

En este artículo se explica cómo crear una instancia de clúster de conmutación por error (FCI) de disco compartido de dos nodos para SQL Server. El artículo incluye instrucciones y ejemplos de script para Red Hat Enterprise Linux (RHEL). Distribuciones de Ubuntu son similares a RHEL de manera que los ejemplos de script hará normalmente también funcionan en Ubuntu. 

Para obtener información conceptual, consulte [conmutación por error de clúster de instancia (FCI de SQL Server) en Linux](sql-server-linux-shared-disk-cluster-concepts.md).

## <a name="prerequisites"></a>Requisitos previos

Para completar el siguiente escenario de extremo a otro, debe tener dos máquinas para implementar el clúster de dos nodos y otro servidor para el almacenamiento. Los pasos siguientes describen cómo se configurará estos servidores.

## <a name="set-up-and-configure-linux"></a>Instalación y configuración de Linux

El primer paso es configurar el sistema operativo en los nodos del clúster. En cada nodo del clúster, configure una distribución de linux. Utilice la misma distribución y versión en ambos nodos. Usar una u otra de las distribuciones siguientes:
    
* RHEL con una suscripción válida para el complemento de alta disponibilidad

## <a name="install-and-configure-sql-server"></a>Instalar y configurar SQL Server

1. Instalar y configurar SQL Server en ambos nodos.  Para obtener instrucciones detalladas, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).
1. Designar un nodo como principal y el otro como secundario para fines de configuración. Usar estos términos para los siguientes elementos en esta guía.  
1. En el nodo secundario, detenga y deshabilite a SQL Server.
    El ejemplo siguiente se detiene y deshabilita el SQL Server: 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > En el conjunto de tiempo de actividad, se genera para la instancia de SQL Server y se coloca en una clave maestra del servidor `var/opt/mssql/secrets/machine-key`. En Linux, SQL Server siempre se ejecuta como una cuenta local denominada mssql. Dado que es una cuenta local, su identidad no se comparte entre los nodos. Por lo tanto, deberá copiar la clave de cifrado del nodo principal en cada nodo secundario para cada cuenta local mssql pueda acceder a él para descifrar la clave maestra del servidor. 

1.  En el nodo principal, cree un inicio de sesión SQL server para Pacemaker y conceda el permiso de inicio de sesión para ejecutar `sp_server_diagnostics`. Pacemaker usa esta cuenta para comprobar qué nodo se está ejecutando SQL Server. 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   Conectarse a SQL Server `master` de base de datos con la cuenta de administrador y ejecute lo siguiente:

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   Como alternativa, puede establecer los permisos con más detalle. El inicio de sesión de Pacemaker requiere `VIEW SERVER STATE` para consultar el estado de mantenimiento con sp_server_diagnostics, `setupadmin` y `ALTER ANY LINKED SERVER` para actualizar el nombre de instancia FCI con el nombre del recurso mediante la ejecución sp_dropserver y sp_addserver. 

1. En el nodo principal, detenga y deshabilite a SQL Server. 

## <a name="configure-the-hosts-file"></a>Configurar el archivo de hosts

En cada nodo del clúster, configure el archivo de hosts. El archivo de hosts debe incluir la dirección IP y el nombre de cada nodo del clúster.

1. Compruebe la dirección IP para cada nodo. El siguiente script muestra la dirección IP del nodo actual. 

    ```bash
    sudo ip addr show
    ```

1. Establezca el nombre del equipo en cada nodo. Asigne a cada nodo un nombre único que es de 15 caracteres o menos. Establece el nombre del equipo mediante la adición a `/etc/hosts`. El siguiente script le permite editar `/etc/hosts` con `vi`. 

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

## <a name="configure-storage--move-database-files"></a>Configurar el almacenamiento y movimiento de archivos de base de datos  

Deberá proporcionar el almacenamiento que pueden tener acceso ambos nodos. Puede usar SMB, NFS o iSCSI. Configurar el almacenamiento, presentar el almacenamiento a los nodos del clúster y, a continuación, mueva los archivos de base de datos al nuevo almacenamiento. Los siguientes artículos explican los pasos para cada tipo de almacenamiento:

- [Configurar la instancia de clúster de conmutación por error - iSCSI: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar la instancia de clúster de conmutación por error: NFS: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar la instancia de clúster de conmutación por error: SMB: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalación y configuración de Pacemaker en cada nodo del clúster

1. En ambos nodos del clúster, cree un archivo para almacenar el nombre de usuario de SQL Server y la contraseña para el inicio de sesión de Pacemaker. 

    El comando siguiente crea y rellena este archivo:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. En ambos nodos del clúster, abra los puertos de firewall de Pacemaker. Para abrir estos puertos con `firewalld`, ejecute el comando siguiente:

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
1. Establezca la contraseña para el usuario predeterminado que se crea al instalar paquetes de Pacemaker y Corosync. Use la misma contraseña en ambos nodos. 

   ```bash
   sudo passwd hacluster
   ```
1. Habilite e inicie el servicio `pcsd` y Pacemaker. Esto permitirá que los nodos se unan al clúster después del reinicio. Ejecute el comando siguiente en ambos nodos.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. Instale el agente de recursos de FCI para SQL Server. Ejecute los comandos siguientes en ambos nodos. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>Configurar la instancia de clúster de conmutación por error

Se creará la FCI en un grupo de recursos. Esto es un poco más fácil porque el grupo de recursos alivia la necesidad de restricciones. Sin embargo, puede agregar los recursos en el grupo de recursos en el orden en que deben iniciarse. El orden en que deben iniciarse es: 

1. Recurso de almacenamiento
2. Recursos de red
3. Recurso de aplicación

Este ejemplo creará una FCI en el grupo NewLinFCIGrp. El nombre del grupo de recursos debe ser único de cualquier recurso que creó en Pacemaker.

1.  Crear el recurso de disco. Si no hay un problema, obtendrá ninguna respuesta. La forma de crear el recurso de disco depende del tipo de almacenamiento. El siguiente es un ejemplo para cada tipo de almacenamiento. Use el ejemplo que se aplica al tipo de almacenamiento para su almacenamiento en clúster.

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > es el nombre del recurso asociado con el disco iSCSI

    \<VolumeGroupName > es el nombre del grupo de volúmenes  

    \<LogicalVolumeName > es el nombre del volumen lógico que se creó  

    \<FolderToMountiSCSIDIsk > es la carpeta para montar el disco (para las bases de datos del sistema y la ubicación predeterminada, estaría /var/opt/mssql/data)

    \<FileSystemType > sería EXT4 o XFS dependiendo de cómo se da formato a las cosas y es compatible con lo que la distribución. 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > es el nombre del recurso asociado con el recurso compartido NFS

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar

    \<FolderOnNFSServer > es el nombre del recurso compartido NFS

    \<FolderToMountNFSShare > es la carpeta para montar el disco (para las bases de datos del sistema y la ubicación predeterminada, estaría /var/opt/mssql/data)

    A continuación, se muestra un ejemplo:

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName > es el nombre del servidor con el recurso compartido SMB

    \<Nombre de recurso compartido > es el nombre del recurso compartido

    \<Nombre de carpeta > es el nombre de la carpeta creada en el último paso
    
    \<Nombre de usuario > es el nombre del usuario para acceder al recurso compartido

    \<Contraseña > es la contraseña del usuario

    \<ADDomain > es el dominio de AD DS (si es aplicable cuando se usa un recurso compartido SMB basado en Windows Server)

    \<mssqlUID > es el identificador exclusivo del usuario de mssql

    \<mssqlGID > es el GID del usuario de mssql

    \<RGName > es el nombre del grupo de recursos
 
2.  Cree la dirección IP que se usará en la FCI. Si no hay un problema, obtendrá ninguna respuesta.

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName > es el nombre del recurso asociado con la dirección IP

    \<Dirección IP > es la dirección IP para la FCI

    \<NetworkCard > es la tarjeta de red asociada con la subred (es decir, eth0)

    \<Máscara de red > es la máscara de red de la subred (es decir, 24)

    \<RGName > es el nombre del grupo de recursos
 
3.  Cree el recurso FCI. Si no hay un problema, obtendrá ninguna respuesta.

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName > es el nombre del recurso, pero no solo el nombre descriptivo que está asociado a la FCI. Esto es lo que los usuarios y aplicaciones a usar para conectarse. 

    \<RGName > es el nombre del grupo de recursos.
 
4.  Ejecute el comando `sudo pcs resource`. La FCI debe estar en línea.
 
5.  Conéctese a la FCI con SSMS o con el nombre DNS o recursos de la FCI de sqlcmd.

6.  Emita la instrucción `SELECT @@SERVERNAME`. Debe devolver el nombre de la FCI.

7.  Emita la instrucción `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`. Debe devolver el nombre del nodo que se está ejecutando la FCI.

8.  Se producirá un error manualmente en la FCI para los demás nodos. Consulte las instrucciones en [instancia de clúster de conmutación por error Operate: SQL Server en Linux](sql-server-linux-shared-disk-cluster-operate.md).

9.  Por último, producirá un error en la FCI en el nodo original y quite la restricción de colocación.

<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
-->
## <a name="summary"></a>Resumen

En este tutorial se completó las tareas siguientes.

> [!div class="checklist"]
> * Instalación y configuración de Linux
> * Instalar y configurar SQL Server
> * Configurar el archivo de hosts
> * Configurar el almacenamiento compartido y mover los archivos de base de datos
> * Instalación y configuración de Pacemaker en cada nodo del clúster
> * Configurar la instancia de clúster de conmutación por error

## <a name="next-steps"></a>Pasos siguientes

- [Operar la instancia de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
