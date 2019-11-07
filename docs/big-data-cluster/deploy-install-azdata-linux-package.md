---
title: Instalación de azdata con instalador en Linux
titleSuffix: SQL Server big data clusters
description: Aprenda a instalar la herramienta azdata para instalar y administrar clústeres de macrodatos de SQL Server con el instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d8d4a34e89de7c136e1e80b43929531a2d10eba
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532071"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Instalación de `azdata` para administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo instalar `azdata` para clústeres de macrodatos de SQL Server 2019 en Linux. Antes de que estos administradores de paquetes estuviesen disponibles, la instalación de `azdata` exigía `pip`.

Los administradores de paquetes están diseñados para distintos sistemas operativos y distribuciones.

- En Windows y Linux (distribución de Ubuntu), se puede instalar con un [administrador de paquetes](./deploy-install-azdata-installer.md) a fin de simplificar la experiencia.
- En Linux (Ubuntu), [instale `azdata` con `apt`](#azdata-apt).

En este momento no hay ningún administrador de paquetes para instalar `azdata` en otros sistemas operativos o distribuciones. Para estas plataformas, vea [Instalación de `azdata` sin el administrador de paquetes](./deploy-install-azdata.md).

## <a id="linux"></a>Instalar `azdata` para Linux

El paquete de instalación `azdata` está disponible para Ubuntu con `apt`.

### <a id="azdata-apt"></a>Instalar `azdata` con apt (Ubuntu)

>[!NOTE]
>El paquete `azdata` no usa el sistema Python, sino que instala su propio intérprete de Python.

1. Obtenga los paquetes necesarios para el proceso de instalación:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. Descargue e instale la clave de firma:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. Agregue la información del repositorio `azdata`:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

4. Actualice la información del repositorio e instale `azdata`:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Compruebe la instalación:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

Actualice `azdata` únicamente:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Desinstalar

1. Desinstale con apt-get remove:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Quite la información del repositorio `azdata`:

    >[!NOTE]
    >Este paso no es necesario si planea instalar `azdata` en el futuro

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. Quite la clave de firma:

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. Quite las dependencias innecesarias que se hayan instalado con la CLI de Azdata:

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
