---
title: Configurar el almacenamiento de instancia failover cluster SMB - SQL Server en Linux | Microsoft Docs
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
ms.openlocfilehash: 184e513ba974a7fba6127e3cf79ea74effe0a661
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084547"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>Configurar la instancia de clúster de conmutación por error: SMB: SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar el almacenamiento SMB para una instancia de clúster de conmutación por error (FCI) en Linux. 
 
En el mundo que no sean Windows, SMB a menudo se conoce para compartir como un sistema de archivos de Internet común (CIFS) y se implementa a través de Samba. En el mundo de Windows, el acceso a un recurso compartido SMB se realiza de este modo: \\nombreservidor\nombrerecursocompartido. Para las instalaciones de SQL Server basada en Linux, se debe montar el recurso compartido SMB como una carpeta.

## <a name="important-source-and-server-information"></a>Información importante de origen y el servidor

Estas son algunas sugerencias y notas para utilizar correctamente SMB:
- Puede ser el recurso compartido SMB en Windows, Linux, o incluso desde un dispositivo como siempre y cuando usa SMB 3.0 o superior. Para obtener más información sobre Samba y SMB 3.0, consulte [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) para ver si su implementación de Samba es compatible con SMB 3.0.
- El recurso compartido SMB debe tener alta disponibilidad.
- Se debe establecer la seguridad correctamente en el recurso compartido SMB. A continuación es un ejemplo de /etc/samba/smb.conf, donde SQLData1 es el nombre del recurso compartido.

![05-smbsource][1]

## <a name="instructions"></a>Instructions

1.  Elija uno de los servidores que participarán en la configuración de FCI. No importa cuál de ellos.

2.  Obtenga información sobre el usuario de mssql.

    ```bash
    sudo id mssql
    ```
    
    Tenga en cuenta el uid, gid y grupos. 

3. Ejecutar `sudo smbclient -L //NameOrIP/ShareName -U User`.

    \<NameOrIP > es el nombre DNS o dirección IP del servidor que hospeda el recurso compartido SMB.

    \<Nombre de recurso compartido > es el nombre del recurso compartido SMB. 

4. Para el sistema de bases de datos o cualquier elemento almacenado en la ubicación de datos predeterminada siga estos pasos. En caso contrario, vaya al paso 5. 

   *    Asegúrese de que SQL Server se ha detenido en el servidor que está trabajando.
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Conmutador totalmente que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```

   *    Cambiar a ser el usuario de mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    su mssql
    ```

   *    Cree un directorio temporal para almacenar los datos de SQL Server y los archivos de registro. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    mkdir <TempDir>
    ```

    <TempDir> es el nombre de la carpeta. El ejemplo siguiente crea una carpeta denominada /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   *    Copie los archivos de registro y datos de SQL Server en el directorio temporal. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > es el nombre de la carpeta en el paso anterior.
    
   *    Compruebe que los archivos están en el directorio.

    ```bash
    ls <TempDir>
    ```

    \<TempDir > es el nombre de la carpeta del paso d.
    
   *    Elimine los archivos del directorio de datos de SQL Server existente. No recibirá ninguna confirmación si se realiza correctamente.
 
    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    Compruebe que se han eliminado los archivos. 

    ```bash
    ls /var/opt/mssql/data
    ```
 
   *    Escriba exit para volver al usuario raíz.

   *    Monte el recurso compartido SMB en la carpeta de datos de SQL Server. No recibirá ninguna confirmación si se realiza correctamente. En este ejemplo se muestra la sintaxis para conectarse a un recurso compartido de SMB 3.0 de basado en Windows Server.

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<ServerName > es el nombre del servidor con el recurso compartido SMB
    
    \<Nombre de recurso compartido > es el nombre del recurso compartido

    \<Nombre de usuario > es el nombre del usuario para acceder al recurso compartido

    \<Contraseña > es la contraseña del usuario

    \<dominio > es el nombre de Active Directory

    \<mssqlUID > es el identificador exclusivo del usuario de mssql 
 
    \<mssqlGID > es el GID del usuario de mssql
 
   *    Compruebe que el montaje fue correcto mediante la emisión de montaje sin los modificadores.

    ```bash
    mount
    ```
 
   *    Cambie al usuario mssql. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    su mssql
    ```

   *    Copie los archivos desde el directorio temporal de /var/opt/mssql/data. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssql/data
    ```

   *    Compruebe que existen los archivos.

    ```bash
    ls /var/opt/mssql/data
    ```

   *    Escriba la salida para que no sea mssql 

   *    Escriba la salida para que no sea raíz

   *    Inicie SQL Server. Si todo lo que se copió correctamente y seguridad aplicada correctamente, SQL Server debe aparecer como iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
 
   *    Para realizar más pruebas, cree una base de datos para asegurarse de que los permisos están bien. En el ejemplo siguiente se utiliza Transact-SQL; Puede usar SSMS.

    ![10_testcreatedb][2] 
  
   *    Detener SQL Server y comprobar que es apagar. Si va a agregar o probar otros discos, no apague SQL Server hasta que los que se agregan y probados.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Solo si terminado, desmonte el recurso compartido. Si no es así, desmontar después de finalizar las pruebas y agregar discos adicionales.

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
    ```

    \<IPAddressOrServerName > es la dirección IP o nombre del host SMB

    \<Nombre de recurso compartido > es el nombre del recurso compartido
    
    \<FolderMountedIn > es el nombre de la carpeta donde se monta SMB

5.  Para elementos distintos de las bases de datos del sistema, como las bases de datos de usuario o las copias de seguridad, siga estos pasos. Si solo usa la ubicación predeterminada, vaya al paso 14.
    
   *    Conmutador que será el superusuario. No recibirá ninguna confirmación si se realiza correctamente.

    ```bash
    sudo -i
    ```
    
   *    Cree una carpeta que se usará en SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nombre de carpeta > es el nombre de la carpeta. Ruta de acceso completa de la carpeta debe especificarse si no están en la ubicación correcta. El ejemplo siguiente crea una carpeta denominada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Monte el recurso compartido SMB en la carpeta de datos de SQL Server. No recibirá ninguna confirmación si se realiza correctamente. En este ejemplo se muestra la sintaxis para conectarse a un recurso compartido basado en Samba SMB 3.0.

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<ServerName > es el nombre del servidor con el recurso compartido SMB

    \<Nombre de recurso compartido > es el nombre del recurso compartido

    \<Nombre de carpeta > es el nombre de la carpeta creada en el último paso  

    \<Nombre de usuario > es el nombre del usuario para acceder al recurso compartido

    \<Contraseña > es la contraseña del usuario

    \<mssqlUID > es el identificador exclusivo del usuario de mssql

    \<mssqlGID > es el GID del usuario de mssql.
 
   * Compruebe que el montaje fue correcto mediante la emisión de montaje sin los modificadores.
 
   * Tipo de salida ya no sea el superusuario.

   * Para probar, cree una base de datos en esa carpeta. El ejemplo siguiente usa sqlcmd para crear una base de datos, cambiar el contexto a ella, compruebe los archivos existen en el nivel de sistema operativo y, a continuación, elimina la ubicación temporal. Puede usar SSMS.
 
   * Desmontar el recurso compartido 

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
    ```
    
    \<IPAddressOrServerName > es la dirección IP o nombre del host SMB
 
    \<Nombre de recurso compartido > es el nombre del recurso compartido
 
    \<FolderMountedIn > es el nombre de la carpeta donde se monta SMB.
 
6.  Repita los pasos en los demás nodos.

Ahora está listo para configurar la FCI.

## <a name="next-steps"></a>Pasos siguientes

[Configurar la instancia de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
