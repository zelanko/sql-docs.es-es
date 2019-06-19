---
title: Configurar repositorios de Linux para SQL Server 2017 y 2019 | Microsoft Docs
description: Compruebe y configure los repositorios de código fuente para 2019 de SQL Server y SQL Server 2017 en Linux. El repositorio de origen afecta a la versión de SQL Server que se aplica durante la instalación y actualización.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 5e21110eb8a24c736b08833d10b509b5494adc48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713336"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Configurar repositorios de instalación y actualización de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
En este artículo se describe cómo configurar el repositorio correcto para las actualizaciones e instalaciones de SQL Server 2017 y 2019 de SQL Server en Linux. En la parte superior, la selección actual es **Red Hat (RHEL)** .
::: zone-end

::: zone pivot="ld2-sles"
En este artículo se describe cómo configurar el repositorio correcto para las actualizaciones e instalaciones de SQL Server 2017 y 2019 de SQL Server en Linux. En la parte superior, la selección actual es **SUSE (SLES)** .
::: zone-end

::: zone pivot="ld2-ubuntu"
En este artículo se describe cómo configurar el repositorio correcto para las actualizaciones e instalaciones de SQL Server 2017 y 2019 de SQL Server en Linux. En la parte superior, la selección actual es **Ubuntu**.
::: zone-end

> [!TIP]
> Ya está disponible la versión preliminar de SQL Server 2019. Para probarlo, use este artículo para configurar el nuevo **mssql-server-vista previa** repositorio. A continuación, instalar con las instrucciones de la [Guía de instalación](sql-server-linux-setup.md).

## <a id="repositories"></a> Repositorios

Al instalar SQL Server en Linux, debe configurar un repositorio de Microsoft. Este repositorio se usa para adquirir el paquete del motor de base de datos, **mssql-server**y relacionados con los paquetes de SQL Server. Actualmente hay tres repositorios principales:

| Repositorio | NOMBRE | Descripción |
|---|---|---|
| **Preview (2017)** | **mssql-server** | Repositorio de SQL Server 2017 CTP y RC (suspendido). |
| **Preview (2019)** | **mssql-server-preview** | Vista previa de SQL Server 2019 y repositorio RC. |
| **CU** | **mssql-server-2017** | Repositorio de SQL Server 2017 actualización acumulativa (CU). |
| **GDR** | **mssql-server-2017-gdr** | Repositorio de SQL Server 2017 GDR de sólo las actualizaciones críticas. |

## <a id="cuversusgdr"></a> Actualización acumulativa frente a GDR

Es importante tener en cuenta que hay dos tipos principales de repositorios para cada distribución:

- **Las actualizaciones acumulativas (CU)** : El repositorio de actualización acumulativa (CU) contiene los paquetes para la versión de SQL Server de base y las correcciones de errores o mejoras desde esa versión. Las actualizaciones acumulativas son específicas para una versión de lanzamiento, como SQL Server 2017. Se publican periódicamente.

- **GDR**: El repositorio GDR contiene paquetes para el lanzamiento de SQL Server base y solo correcciones críticas y actualizaciones de seguridad desde esa versión. Estas actualizaciones también se agregan a la próxima versión CU.

Cada versión de la unidad de capacidad y GDR contiene el paquete completo de SQL Server y todas las actualizaciones anteriores de ese repositorio. Se admite la actualización desde una versión GDR a una versión CU cambiando su repositorio configurado para SQL Server. También puede [degradar](sql-server-linux-setup.md#rollback) a cualquier versión dentro de la versión principal (p. ej.: 2017).

> [!NOTE]
> Puede actualizar desde una versión GDR a CU liberar en cualquier momento cambiando repositorios. Actualizar desde una unidad de capacidad no se admite la versión a una versión de GDR.

## <a name="configure-repositories"></a>Configuración de repositorios

::: zone pivot="ld2-rhel"
Use los pasos en las secciones siguientes para configurar repositorios en Red Hat Enterprise Server (RHEL).
::: zone-end

::: zone pivot="ld2-sles"
Use los pasos en las secciones siguientes para configurar repositorios en SUSE Linux Enterprise Server (SLES).
::: zone-end

::: zone pivot="ld2-ubuntu"
Use los pasos en las secciones siguientes para configurar repositorios en Ubuntu.
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>Comprobación de repositorios previamente configurados

<!--RHEL-->
::: zone pivot="ld2-rhel"
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

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Use **zypper información** para obtener información sobre cualquier repositorio configurado previamente.

   ```bash
   sudo zypper info mssql-server
   ```

2. El **repositorio** propiedad es el repositorio configurado. Puede identificar con la tabla en la [repositorios](#repositories) sección de este artículo.

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Ver el contenido de la **/etc/apt/sources.list** archivo.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Examine la dirección URL del paquete de mssql-server. Puede identificar con la tabla en la [repositorios](#repositories) sección de este artículo.

::: zone-end

## <a name="remove-old-repository"></a>Eliminar repositorio antiguo

<!--RHEL-->
::: zone pivot="ld2-rhel"
Si es necesario, quite el repositorio antiguo con el siguiente comando.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Este comando supone que el archivo identificado en la sección anterior se denominaba **mssql server.repo**.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Si es necesario, quite el repositorio antiguo. Utilice uno de los siguientes comandos en función del tipo de repositorio configurado previamente.

| Repositorio | Comando para quitar |
|---|---|
| **Preview (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **Preview (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Si es necesario, quite el repositorio antiguo. Utilice uno de los siguientes comandos en función del tipo de repositorio configurado previamente.

| Repositorio | Comando para quitar |
|---|---|
| **Preview (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **Preview (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>Configurar el nuevo repositorio

<!--RHEL-->
::: zone pivot="ld2-rhel"
Configure el repositorio nuevo que se usará para las actualizaciones y las instalaciones de SQL Server. Utilice uno de los comandos siguientes para configurar el repositorio de su elección.

| Repositorio | Versión | Comando |
|---|---|---|
| **Preview (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Configure el repositorio nuevo que se usará para las actualizaciones y las instalaciones de SQL Server. Utilice uno de los comandos siguientes para configurar el repositorio de su elección.

| Repositorio | Versión | Comando |
|---|---|---|
| **Preview (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Configure el repositorio nuevo que se usará para las actualizaciones y las instalaciones de SQL Server.

1. Importe las claves GPG repositorio público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Utilice uno de los comandos siguientes para configurar el repositorio de su elección.

   | Repositorio | Versión | Comando |
   |---|---|---|
   | **Preview (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Ejecute **apt-get actualización**.

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>Pasos siguientes

Después de haber configurado el repositorio correcto, puede continuar con [instalar](sql-server-linux-setup.md#platforms) o [actualizar](sql-server-linux-setup.md#upgrade) SQL Server y los relacionados con los paquetes desde el repositorio de nuevo.

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> En este punto, si opta por usar el [inicio rápido RHEL](quickstart-install-connect-red-hat.md), recuerde que ya ha configurado el repositorio de destino. No repita este paso en los tutoriales. Esto es especialmente cierto si configura el repositorio GDR, dado que el inicio rápido usa el repositorio de CU.
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> En este punto, si opta por usar el [inicio rápido SLES](quickstart-install-connect-suse.md), recuerde que ya ha configurado el repositorio de destino. No repita este paso en los tutoriales. Esto es especialmente cierto si configura el repositorio GDR, dado que el inicio rápido usa el repositorio de CU.
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> En este punto, si opta por usar el [inicio rápido de Ubuntu](quickstart-install-connect-ubuntu.md), recuerde que ya ha configurado el repositorio de destino. No repita este paso en los tutoriales. Esto es especialmente cierto si configura el repositorio GDR, dado que el inicio rápido usa el repositorio de CU.
::: zone-end

Para obtener más información sobre cómo instalar SQL Server 2017 en Linux, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).
