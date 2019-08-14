---
title: Configuración de repositorios de Linux para SQL Server 2017 y 2019
description: Vea y configure repositorios de origen para SQL Server 2019 y SQL Server 2017 en Linux. El repositorio de origen afecta a la versión de SQL Server que se aplica durante la instalación y la actualización.
author: VanMSFT
ms.author: vanto
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 33616b9a7767156e4cfd69d233f7dcfe5fc080f6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67967523"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Configuración de repositorios para instalar y actualizar SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
En este artículo se explica cómo configurar el repositorio correcto para las instalaciones y las actualizaciones de SQL Server 2017 y SQL Server 2019 en Linux. En la parte superior, la selección actual es **Red Hat (RHEL)** .
::: zone-end

::: zone pivot="ld2-sles"
En este artículo se explica cómo configurar el repositorio correcto para las instalaciones y las actualizaciones de SQL Server 2017 y SQL Server 2019 en Linux. En la parte superior, la selección actual es **SUSE (SLES)** .
::: zone-end

::: zone pivot="ld2-ubuntu"
En este artículo se explica cómo configurar el repositorio correcto para las instalaciones y las actualizaciones de SQL Server 2017 y SQL Server 2019 en Linux. En la parte superior, la selección actual es **Ubuntu**.
::: zone-end

> [!TIP]
> Ya está disponible la versión preliminar de SQL Server 2019. Para probarla, use este artículo para configurar el nuevo repositorio **mssql-server-preview**. Luego instale con las instrucciones de la [guía de instalación](sql-server-linux-setup.md).

## <a id="repositories"></a> Repositorios

Al instalar SQL Server en Linux, debe configurar un repositorio de Microsoft. Este repositorio se usa para adquirir el paquete del motor de base de datos, **mssql-server**, y los paquetes de SQL Server relacionados. Actualmente hay tres repositorios principales:

| Repositorio | Nombre | Descripción |
|---|---|---|
| **Versión preliminar (2017)** | **mssql-server** | Repositorio SQL Server 2017 CTP y RC (descontinuado). |
| **Versión preliminar (2019)** | **mssql-server-preview** | Repositorio SQL Server 2019 versión preliminar y RC. |
| **CU** | **mssql-server-2017** | Repositorio SQL Server 2017 Actualización acumulativa (CU). |
| **GDR** | **mssql-server-2017-gdr** | Repositorio SQL Server 2017 GDR solo para actualizaciones críticas. |

## <a id="cuversusgdr"></a> Actualización acumulativa frente a GDR

Es importante tener en cuenta que hay dos tipos principales de repositorios para cada distribución:

- **Actualización acumulativa (CU)** : el repositorio Actualización acumulativa (CU) contiene paquetes para la versión básica de SQL Server y las correcciones de errores o mejoras desde esa versión. Las actualizaciones acumulativas son específicas de una versión de lanzamiento, como SQL Server 2017. Se publican periódicamente.

- **GDR**: el repositorio GDR contiene paquetes para la versión básica de SQL Server y solo correcciones críticas y actualizaciones de seguridad desde esa versión. Estas actualizaciones también se agregan a la siguiente versión CU.

Cada versión CU y GDR contiene el paquete de SQL Server completo y todas las actualizaciones anteriores para ese repositorio. Se puede actualizar desde una versión GDR a una versión CU si se cambia el repositorio configurado para SQL Server. También se puede [cambiar a una versión anterior](sql-server-linux-setup.md#rollback) dentro de la versión principal (por ejemplo: 2017).

> [!NOTE]
> Puede actualizar desde una versión GDR a una versión CU en cualquier momento mediante el cambio de repositorios. No se admite la actualización desde una versión CU a una versión GDR.

## <a name="configure-repositories"></a>Configuración de repositorios

::: zone pivot="ld2-rhel"
Siga los pasos de las secciones siguientes para configurar repositorios en Red Hat Enterprise Server (RHEL).
::: zone-end

::: zone pivot="ld2-sles"
Siga los pasos de las secciones siguientes para configurar repositorios en SUSE Linux Enterprise Server (SLES).
::: zone-end

::: zone pivot="ld2-ubuntu"
Siga los pasos de las secciones siguientes para configurar repositorios en Ubuntu.
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>Buscar repositorios configurados previamente

<!--RHEL-->
::: zone pivot="ld2-rhel"
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Vea los archivos del directorio **/etc/yum.repos.d** con el siguiente comando:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. Busque un archivo que configure el directorio de SQL Server, como **mssql-server.repo**.

3. Imprima el contenido del archivo.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. La propiedad **name** es el repositorio configurado. Puede identificarlo con la tabla de la sección [Repositorios](#repositories) de este artículo.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Use **zypper info** para obtener información sobre cualquier repositorio configurado previamente.

   ```bash
   sudo zypper info mssql-server
   ```

2. La propiedad **Repository** es el repositorio configurado. Puede identificarlo con la tabla de la sección [Repositorios](#repositories) de este artículo.

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
En primer lugar, compruebe si ya ha registrado un repositorio de SQL Server.

1. Vea el contenido del archivo **/etc/apt/sources.list**.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Examine la dirección URL del paquete de mssql-server. Puede identificarlo con la tabla de la sección [Repositorios](#repositories) de este artículo.

::: zone-end

## <a name="remove-old-repository"></a>Eliminación de un repositorio antiguo

<!--RHEL-->
::: zone pivot="ld2-rhel"
En caso necesario, quite el repositorio antiguo con el siguiente comando.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Este comando supone que el archivo identificado en la sección anterior se denominaba **mssql-server.repo**.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
En caso necesario, quite el repositorio antiguo. Use uno de los siguientes comandos en función del tipo de repositorio configurado previamente.

| Repositorio | Comando para quitar |
|---|---|
| **Versión preliminar (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **Versión preliminar (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
En caso necesario, quite el repositorio antiguo. Use uno de los siguientes comandos en función del tipo de repositorio configurado previamente.

| Repositorio | Comando para quitar |
|---|---|
| **Versión preliminar (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **Versión preliminar (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>Configuración de un nuevo repositorio

<!--RHEL-->
::: zone pivot="ld2-rhel"
Configure el nuevo repositorio que se va a usar para las instalaciones y las actualizaciones de SQL Server. Use uno de los siguientes comandos para configurar el repositorio que prefiera.

| Repositorio | Versión | Comando |
|---|---|---|
| **Versión preliminar (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Configure el nuevo repositorio que se va a usar para las instalaciones y las actualizaciones de SQL Server. Use uno de los siguientes comandos para configurar el repositorio que prefiera.

| Repositorio | Versión | Comando |
|---|---|---|
| **Versión preliminar (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Configure el nuevo repositorio que se va a usar para las instalaciones y las actualizaciones de SQL Server.

1. Importe las claves de GPG del repositorio público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Use uno de los siguientes comandos para configurar el repositorio que prefiera.

   | Repositorio | Versión | Comando |
   |---|---|---|
   | **Versión preliminar (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Ejecute **apt-get update**.

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>Pasos siguientes

Una vez configurado el repositorio correcto, puede continuar con la [instalación](sql-server-linux-setup.md#platforms) o la [actualización](sql-server-linux-setup.md#upgrade) de SQL Server y los paquetes relacionados del nuevo repositorio.

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> En este punto, si decide usar el [Inicio rápido de RHEL](quickstart-install-connect-red-hat.md), recuerde que ya ha configurado el repositorio de destino. No repita ese paso en los tutoriales. Esto es especialmente así si configura el repositorio GDR, ya que el inicio rápido usa el repositorio CU.
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> En este punto, si decide usar el [Inicio rápido de SLES](quickstart-install-connect-suse.md), recuerde que ya ha configurado el repositorio de destino. No repita ese paso en los tutoriales. Esto es especialmente así si configura el repositorio GDR, ya que el inicio rápido usa el repositorio CU.
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> En este punto, si decide usar el [Inicio rápido de Ubuntu](quickstart-install-connect-ubuntu.md), recuerde que ya ha configurado el repositorio de destino. No repita ese paso en los tutoriales. Esto es especialmente así si configura el repositorio GDR, ya que el inicio rápido usa el repositorio CU.
::: zone-end

Para obtener más información sobre cómo instalar SQL Server 2017 en Linux, vea [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).
