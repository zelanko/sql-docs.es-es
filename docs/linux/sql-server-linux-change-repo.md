---
title: Configurar repositorios de Linux para SQL Server 2017 y 2019 | Microsoft Docs
description: Compruebe y configure los repositorios de código fuente para 2019 de SQL Server y SQL Server 2017 en Linux. El repositorio de origen afecta a la versión de SQL Server que se aplica durante la instalación y actualización.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 9b5d9e27db92ba048f0b6400c00313e81a1899f7
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269450"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Configurar repositorios de instalación y actualización de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe cómo configurar el repositorio correcto para las actualizaciones e instalaciones de SQL Server 2017 y 2019 de SQL Server en Linux.

> [!TIP]
> Ya está disponible la versión preliminar de SQL Server 2019. Para probarlo, use este artículo para configurar el nuevo **mssql-server-vista previa** repositorio. A continuación, instalar con las instrucciones de la [Guía de instalación](sql-server-linux-setup.md).

## <a id="repositories"></a> Repositorios

Al instalar SQL Server en Linux, debe configurar un repositorio de Microsoft. Este repositorio se usa para adquirir el paquete del motor de base de datos, **mssql-server**y relacionados con los paquetes de SQL Server. Actualmente hay tres repositorios principales:

| Repositorio | Nombre | Descripción |
|---|---|---|
| **Vista previa (2017)** | **MSSQL-server** | Repositorio de SQL Server 2017 CTP y RC (suspendido). |
| **Vista previa (2019)** | **MSSQL-server-versión preliminar** | Vista previa de SQL Server 2019 y repositorio RC. |
| **CU** | **MSSQL-server-2017** | Repositorio de SQL Server 2017 actualización acumulativa (CU). |
| **GDR** | **MSSQL-server-2017-gdr** | Repositorio de SQL Server 2017 GDR de sólo las actualizaciones críticas. |

## <a id="cuversusgdr"></a> Actualización acumulativa frente a GDR

Es importante tener en cuenta que hay dos tipos principales de repositorios para cada distribución:

- **Las actualizaciones acumulativas (CU)**: repositorio de la actualización acumulativa (CU) contiene los paquetes para la versión de SQL Server de base y las correcciones de errores o mejoras desde esa versión. Las actualizaciones acumulativas son específicas para una versión de lanzamiento, como SQL Server 2017. Se publican periódicamente.

- **GDR**: repositorio de la GDR contiene paquetes para el lanzamiento de SQL Server base y solo correcciones críticas y actualizaciones de seguridad desde esa versión. Estas actualizaciones también se agregan a la próxima versión CU.

Cada versión de la unidad de capacidad y GDR contiene el paquete completo de SQL Server y todas las actualizaciones anteriores de ese repositorio. Se admite la actualización desde una versión GDR a una versión CU cambiando su repositorio configurado para SQL Server. También puede [degradar](sql-server-linux-setup.md#rollback) a cualquier versión dentro de la versión principal (p. ej.: 2017).

> [!NOTE]
> Puede actualizar desde una versión GDR a CU liberar en cualquier momento cambiando repositorios. Actualizar desde una unidad de capacidad no se admite la versión a una versión de GDR. 

## <a id="configure"></a> Configuración de un repositorio

Las secciones siguientes describen cómo comprobar y configurar un repositorio para las plataformas admitidos siguientes:

- [Red Hat Enterprise Server](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a> Configurar repositorios RHEL
Use los pasos siguientes para configurar repositorios en Red Hat Enterprise Server (RHEL).

### <a name="check-for-previously-configured-repositories-rhel"></a>Buscar repositorios configurados previamente (RHEL)
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Ver los archivos en el **/etc/yum.repos.d** directorio con el siguiente comando:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. Busque un archivo que se configura el directorio de SQL Server, como **mssql server.repo**.

3. Imprimir el contenido del archivo.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. El **nombre** propiedad es el repositorio configurado. Puede identificar con la tabla en la [repositorios](#repositories) sección de este artículo.

### <a name="remove-old-repository-rhel"></a>Eliminar repositorio antiguo (RHEL)
Si es necesario, quite el repositorio antiguo con el siguiente comando.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Este comando supone que el archivo identificado en la sección anterior se denominaba **mssql server.repo**.

### <a name="configure-new-repository-rhel"></a>Configurar el nuevo repositorio (RHEL)
Configure el repositorio nuevo que se usará para las actualizaciones y las instalaciones de SQL Server. Utilice uno de los comandos siguientes para configurar el repositorio de su elección.

| Repositorio | Versión | Comando |
|---|---|---|
| **Vista previa (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a> Configurar repositorios SLES
Use los pasos siguientes para configurar repositorios en SLES.

### <a name="check-for-previously-configured-repositories-sles"></a>Buscar repositorios configurados previamente (SLES)
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Use **zypper información** para obtener información sobre cualquier repositorio configurado previamente.

   ```bash
   sudo zypper info mssql-server
   ```

2. El **repositorio** propiedad es el repositorio configurado. Puede identificar con la tabla en la [repositorios](#repositories) sección de este artículo.

### <a name="remove-old-repository-sles"></a>Eliminar repositorio antiguo (SLES)
Si es necesario, quite el repositorio antiguo. Utilice uno de los siguientes comandos en función del tipo de repositorio configurado previamente.

| Repositorio | Comando para quitar |
|---|---|
| **Vista previa (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **Vista previa (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>Configurar el nuevo repositorio (SLES)
Configure el repositorio nuevo que se usará para las actualizaciones y las instalaciones de SQL Server. Utilice uno de los comandos siguientes para configurar el repositorio de su elección.

| Repositorio | Versión | Comando |
|---|---|---|
| **Vista previa (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a> Configurar repositorios de Ubuntu
Use los pasos siguientes para configurar repositorios en Ubuntu.

### <a name="check-for-previously-configured-repositories-ubuntu"></a>Buscar repositorios configurados anteriormente (Ubuntu)
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Ver el contenido de la **/etc/apt/sources.list** archivo.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Examine la dirección URL del paquete de mssql-server. Puede identificar con la tabla en la [repositorios](#repositories) sección de este artículo.

### <a name="remove-old-repository-ubuntu"></a>Eliminar repositorio antiguo (Ubuntu)
Si es necesario, quite el repositorio antiguo. Utilice uno de los siguientes comandos en función del tipo de repositorio configurado previamente.

| Repositorio | Comando para quitar |
|---|---|
| **Vista previa (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **Vista previa (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>Configurar el nuevo repositorio (Ubuntu)
Configure el repositorio nuevo que se usará para las actualizaciones y las instalaciones de SQL Server.

1. Importe las claves GPG repositorio público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Utilice uno de los comandos siguientes para configurar el repositorio de su elección.

   | Repositorio | Versión | Comando |
   |---|---|---|
   | **Vista previa (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Ejecute **apt-get actualización**.

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>Pasos siguientes

Después de haber configurado el repositorio correcto, puede continuar con [instalar](sql-server-linux-setup.md#platforms) o [actualizar](sql-server-linux-setup.md#upgrade) SQL Server y los relacionados con los paquetes desde el repositorio de nuevo.

> [!IMPORTANT]
> En este punto, si opta por utilizar uno de los artículos de la instalación, como el [inicios rápidos](sql-server-linux-setup.md#platforms), recuerde que ya ha configurado el repositorio de destino. No repita este paso en los tutoriales. Esto es especialmente cierto si configura el repositorio GDR, ya que los tutoriales utilizan el repositorio de CU.

Para obtener más información sobre cómo instalar SQL Server 2017 en Linux, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).
