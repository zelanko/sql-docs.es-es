---
title: Configurar recursos compartidos de instantáneas carpeta replicación de SQL Server en Linux
description: En este artículo se describe cómo configurar la replicación de SQL Server de los recursos compartidos de carpeta de instantáneas en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4091bd6f1a3afcf32431af78ad47089ffc9a1620
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834779"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>Configurar la carpeta de instantáneas de replicación con recursos compartidos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

La carpeta de instantáneas es un directorio que ha designado como un recurso compartido; los agentes que leen y escriben en esta carpeta deben tener los permisos suficientes para tener acceso a él.

![diagrama de replicación][1]

### <a name="replication-snapshot-folder-share-explained"></a>Se explica recurso compartido de carpeta de instantáneas de replicación

Antes de los ejemplos, veamos cómo SQL Server usa los recursos compartidos de samba en la replicación. A continuación es un ejemplo básico de cómo funciona esto.

1. Recursos compartidos de Samba se configuran que los archivos escritos en `/local/path1` la replicación, agentes en el publicador pueden verse el suscriptor
2. SQL Server está configurado para usar las rutas de acceso del recurso compartido al configurar el publicador en el servidor de distribución de modo que todas las instancias se parecería a la `//share/path`
3. SQL Server busca la ruta de acceso local desde el `//share/path` saber dónde buscar los archivos
4. Lecturas y escrituras de SQL Server en rutas de acceso locales, respaldado por un recurso compartido de archivos


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>Configurar un recurso compartido de archivos para la carpeta de instantáneas 

Los agentes de replicación será necesario un directorio compartido entre los hosts de replicación para tener acceso a las carpetas de instantáneas en otros equipos. Por ejemplo, en la replicación transaccional de extracción, el agente de distribución se encuentra en el suscriptor, lo que requiere acceso al distribuidor y los artículos. En esta sección, analizaremos un ejemplo de cómo configurar un recurso compartido de archivos en dos hosts de replicación.


## <a name="steps"></a>Pasos

Por ejemplo, configuraremos una carpeta de instantáneas en el Host 1 (el distribuidor) se comparta con el Host 2 (el suscriptor) mediante Samba. 

### <a name="install-and-start-samba-on-both-machines"></a>Instale e inicie Samba en ambas máquinas 

En Ubuntu:

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

En RHEL:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>En el recurso compartido de archivos de configuración de Host 1 (distribuidor) 

1. Usuario de instalación y la contraseña de samba:

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. Editar el `/etc/samba/smb.conf` para incluir la siguiente entrada y rellene el *nombre_recurso_compartido* y *ruta* campos
 ```bash
  <[share_name]>
  path = </local/path/on/host/1>
  writable = yes
  create mask = 770
  directory mask 
  valid users = mssql 
  ```

  **Ejemplo**

  ```bash
  [mssql_data]    <- Name of the shared directory
  path = /var/opt/mssql/repldata <- location of directory we wish to share
  writable = yes  <- determines if the share is writable from other hosts
  create mask = 770  <- Linux permissions for files created 
  directory mask = 770 <- Linux permissions for directories created
  valid users = mssql   <- list of users who can login to this share
  ```

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>En el Host 2 (suscriptor), monte el recurso compartido de archivos

Edite el comando con las rutas de acceso correctos y ejecute el siguiente comando en MÁQUINA2:

  ```bash
  sudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssql
  ```

  **Ejemplo**

  ```bash
  mount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssql

  user=mssql <- sets the login name for samba
  uid=mssql   <- makes the mssql user as the owner of the mounted directory
  gid=mssql   <- sets the mssql group as the owner of the mounted directory
  ```

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>En ambos Hosts configurar SQL Server en instancias de Linux para usar el recurso compartido de instantáneas

Agregue la siguiente sección para `mssql.conf` en ambos equipos. Usar siempre que el recurso compartido de archivos para la / / / ruta de acceso. En este ejemplo, sería: `//host1/mssql_data`

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **Ejemplo**

  En host1:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  En host2:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>Configurar publicador con las rutas de acceso compartido

* Al configurar la replicación, use la ruta de acceso de los recursos compartidos (ejemplo `//host1/mssql_data`
* Mapa `//host1/mssql_data` a un directorio local y la asignación agregada a `mssql.conf`.

## <a name="next-steps"></a>Pasos siguientes

[Conceptos: Replicación de SQL Server en Linux](sql-server-linux-replication.md)

[Procedimientos almacenados de replicación](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
