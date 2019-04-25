---
title: 'Configurar el almacenamiento de instancia de conmutación por error clúster NFS: SQL Server en Linux | Microsoft Docs'
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 672e6142ee7196115ba10309e6ac5ef7aa7d151f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62634758"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>Configurar la instancia de clúster de conmutación por error: NFS: SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar el almacenamiento NFS para una instancia de clúster de conmutación por error (FCI) en Linux. 

NFS o sistema de archivos de red, es un método común para el uso compartido de discos en el mundo de Linux, pero no el Windows uno. Similar a iSCSI, NFS se puede configurar en un servidor o de algún tipo de dispositivo o unidad de almacenamiento, siempre cumpla los requisitos de almacenamiento para SQL Server.

## <a name="important-nfs-server-information"></a>Información importante del servidor NFS

El origen de hospedaje NFS (un servidor Linux o cosa) debe ser utilizando/compatible con la versión 4.2 o posterior. Las versiones anteriores no funcionarán con SQL Server en Linux.

Al configurar las carpetas que se pueden compartir en el servidor NFS, asegúrese de que siguen las opciones generales de estas directrices:
- `rw` para asegurarse de que la carpeta se puede leer y escribir en
- `sync` para asegurarse de garantiza que las escrituras a la carpeta
- No use `no_root_squash` como una opción; se considera un riesgo de seguridad
- Asegúrese de que la carpeta tiene derechos completos (777) aplicados

Asegúrese de que se apliquen los estándares de seguridad para tener acceso a. Al configurar la carpeta, asegúrese de que sólo los servidores que participan en la FCI deberían ver la carpeta NFS. A continuación que está restringida a FCIN1 y FCIN2 la carpeta se muestra un ejemplo de un /etc/exports modificado en una solución NFS basados en Linux.

![05-nfsacl][1]

## <a name="instructions"></a>Instructions

1. Elija uno de los servidores que participarán en la configuración de FCI. No importa cuál de ellos. 

2. Compruebe que el servidor puede ver el mount(s) en el servidor NFS.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar.

3. Para las bases de datos del sistema o cualquier elemento almacenado en la ubicación de datos de forma predeterminada, siga estos pasos. De lo contrario, vaya al paso 4.
 
   * Asegúrese de que SQL Server se ha detenido en el servidor que está trabajando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * Conmutador totalmente que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```

   * Cambiar a ser el usuario de mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    su mssql
    ```

   * Cree un directorio temporal para almacenar los datos de SQL Server y los archivos de registro. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > es el nombre de la carpeta. El ejemplo siguiente crea una carpeta denominada /var/opt/mssql/tmp.

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

   * Elimine los archivos del directorio de datos de SQL Server existente. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   * Compruebe que se han eliminado los archivos. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * Escriba exit para volver al usuario raíz.

   * Monte el recurso compartido de NFS en la carpeta de datos de SQL Server. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar 

    \<FolderOnNFSServer > es el nombre del recurso compartido NFS. La sintaxis de ejemplo siguiente coincide con la información de NFS en el paso 2.

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

   * Copie los archivos desde el directorio temporal de /var/opt/mssql/data. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * Compruebe que existen los archivos.

    ```bash
    ls /var/opt/mssql/data
    ```

   * Escriba la salida para que no sea mssql 
    
   * Escriba la salida para que no sea raíz

   * Inicie SQL Server. Si todo lo que se copió correctamente y seguridad aplicada correctamente, SQL Server debe aparecer como iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * Crear una base de datos para probar que seguridad se ha configurado correctamente. El ejemplo siguiente muestra se realiza a través de Transact-SQL; puede realizarse a través de SSMS.
 
    ![CreateTestdatabase][3]

   * Detener SQL Server y comprobar que es apagar.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * Si no va a crear cualquier otros montajes NFS, desmonte el recurso compartido. Si es así, no desmonte.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar

    \<FolderOnNFSServer > es el nombre del recurso compartido NFS

    \<FolderMountedIn > es la carpeta que creó en el paso anterior. 

4. Para elementos distintos de las bases de datos del sistema, como las bases de datos de usuario o las copias de seguridad, siga estos pasos. Si solo usa la ubicación predeterminada, vaya al paso 5.

   * Conmutador que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```

   * Cree una carpeta que se usará en SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nombre de carpeta > es el nombre de la carpeta. Ruta de acceso completa de la carpeta debe especificarse si no están en la ubicación correcta. El ejemplo siguiente crea una carpeta denominada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * Monte el recurso compartido de NFS en la carpeta que creó en el paso anterior. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar

    \<FolderOnNFSServer > es el nombre del recurso compartido NFS

    \<FolderToMountIn > es la carpeta que creó en el paso anterior. A continuación es un ejemplo. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * Compruebe que el montaje fue correcto mediante la emisión de montaje sin los modificadores.
  
   * Tipo de salida ya no sea el superusuario.

   * Para probar, cree una base de datos en esa carpeta. El ejemplo siguiente usa sqlcmd para crear una base de datos, cambiar el contexto a ella, compruebe los archivos existen en el nivel de sistema operativo y, a continuación, elimina la ubicación temporal. Puede usar SSMS.

    ![15-createtestdatabase][4]
 
   * Desmontar el recurso compartido 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > es la dirección IP del servidor NFS que va a usar
    
    \<FolderOnNFSServer > es el nombre del recurso compartido NFS

    \<FolderMountedIn > es la carpeta que creó en el paso anterior. A continuación es un ejemplo. 
 
5. Repita los pasos en los demás nodos.


## <a name="next-steps"></a>Pasos siguientes

[Configurar la instancia de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
