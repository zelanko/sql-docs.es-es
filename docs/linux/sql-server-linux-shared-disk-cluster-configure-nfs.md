---
title: "Configurar el almacenamiento de instancia de conmutación por error clúster NFS: SQL Server en Linux | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 1b944d36e968234d5ea77a861c595e440cbbb15b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>Configurar la instancia de clúster de conmutación por error - NFS: SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este artículo se explica cómo configurar el almacenamiento NFS para una instancia de clúster de conmutación por error (FCI) en Linux. 

NFS o sistema de archivos de red es un método común para uso compartido de discos en el mundo de Linux, pero no las ventanas de uno. Similar a iSCSI, NFS puede configurarse en un servidor o algún tipo de dispositivo o unidad de almacenamiento siempre que cumple los requisitos de almacenamiento para SQL Server.

## <a name="important-nfs-server-information"></a>Información importante del servidor NFS

El origen de hospedaje NFS (un servidor Linux o algo) debe ser usar/compatible con versión 4.2 o posterior. Las versiones anteriores no funcionará con SQL Server en Linux.

Al configurar las carpetas para compartirse en el servidor NFS, asegúrese de que siguen las opciones generales de estas directrices:
- `rw`para asegurarse de que la carpeta puede leer y escribir en
- `sync`para asegurarse de garantiza que escribe en la carpeta
- No use `no_root_squash` como una opción; se considera un riesgo de seguridad
- Asegúrese de que la carpeta tiene derechos completos (777) aplicados

Asegúrese de que se apliquen los estándares de seguridad para tener acceso a. Al configurar la carpeta, asegúrese de que sólo los servidores que participan en la FCI deberían aparecer la carpeta NFS. Debajo de donde está restringida a FCIN1 y FCIN2 la carpeta se muestra un ejemplo de un /etc/exports modificado en una solución NFS basados en Linux.

![05-nfsacl][1]

## <a name="instructions"></a>Instructions

1. Elija uno de los servidores que vaya a participar en la configuración de FCI. No importa qué. 

2. Compruebe que el servidor puede ver el mount(s) en el servidor NFS.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar.

3. Para las bases de datos del sistema o cualquier elemento almacenado en la ubicación de datos de forma predeterminada, siga estos pasos. De lo contrario, vaya al paso 4.
 
   * Asegúrese de que SQL Server se detiene en el servidor que está trabajando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * Conmutador totalmente que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```

   * Cambiar a ser el usuario mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    su mssql
    ```

   * Cree un directorio temporal para almacenar los datos de SQL Server y los archivos de registro. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > es el nombre de la carpeta. En el ejemplo siguiente se crea una carpeta denominada /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * Copie los archivos de registro y datos de SQL Server en el directorio temporal. No recibirá ninguna confirmación si se realiza correctamente.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > es el nombre de la carpeta en el paso anterior.

   * Compruebe que los archivos están en el directorio.

    ```bash
    ls TempDir
    ```

    \<TempDir > es el nombre de la carpeta del paso d.

   * Elimine los archivos desde el directorio de datos de SQL Server existente. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * Compruebe que los archivos que se haya eliminado. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * Escriba exit para volver al usuario raíz.

   * Monte el recurso compartido NFS en la carpeta de datos de SQL Server. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar 

    \<FolderOnNFSServer > es el nombre del recurso compartido de NFS. La sintaxis de ejemplo siguiente coincide con la información de NFS del paso 2.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * Compruebe que el montaje fue correcto mediante la emisión de montaje sin los modificadores.

    ```bash
    mount
    ```

    ![10-mountnoswitches][2]

   * Cambie al usuario mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    su mssql
    ```

   * Copie los archivos desde el directorio temporal /var/opt/mssql/data. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * Compruebe que los archivos existen.

    ```bash
    ls /var/opt/mssql/data
    ```

   * Escriba exit para que no sea mssql 
    
   * Escriba exit para que no sea raíz

   * Inicie SQL Server. Si todos los elementos se copian correctamente y aplicada la seguridad, SQL Server debe mostrar correctamente como iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * Crear una base de datos para probar que seguridad se ha configurado correctamente. En el ejemplo siguiente mostrará que se realiza a través de Transact-SQL; se puede realizar a través de SSMS.
 
    ![CreateTestdatabase][3]

   * Detener SQL Server y compruebe que está apagar.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * Si no va a crear otros montajes NFS, desmonte el recurso compartido. Si está, no desmonte.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar

    \<FolderOnNFSServer > es el nombre del recurso compartido de NFS

    \<FolderMountedIn > es la carpeta que creó en el paso anterior. 

4. Cosas que no sea de bases de datos del sistema, como las bases de datos de usuario o las copias de seguridad, siga estos pasos. Si solo usa la ubicación predeterminada, vaya al paso 5.

   * Conmutador que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```

   * Cree una carpeta que se usará en SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nombre de carpeta > es el nombre de la carpeta. Ruta de acceso completa de la carpeta debe especificarse si no están en la ubicación correcta. En el ejemplo siguiente se crea una carpeta denominada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * Monte el recurso compartido NFS en la carpeta que creó en el paso anterior. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar

    \<FolderOnNFSServer > es el nombre del recurso compartido de NFS

    \<FolderToMountIn > es la carpeta que creó en el paso anterior. A continuación se muestra un ejemplo. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * Compruebe que el montaje fue correcto mediante la emisión de montaje sin los modificadores.
  
   * Escriba exit ya no sea el superusuario.

   * Para probar, cree una base de datos en esa carpeta. El ejemplo que se muestra a continuación utiliza sqlcmd para crear una base de datos, cambiar el contexto a él, compruebe que los archivos existen en el nivel de sistema operativo y, a continuación, elimina la ubicación temporal. Puede usar SSMS.

    ![15-createtestdatabase][4]
 
   * Desmonte el recurso compartido 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar
    
    \<FolderOnNFSServer > es el nombre del recurso compartido de NFS

    \<FolderMountedIn > es la carpeta que creó en el paso anterior. A continuación se muestra un ejemplo. 
 
5. Repita los pasos en los demás nodos.


## <a name="next-steps"></a>Pasos siguientes

[Configurar la instancia de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
