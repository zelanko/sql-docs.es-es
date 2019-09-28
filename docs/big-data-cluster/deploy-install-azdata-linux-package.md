---
title: Instalación de azdata con el instalador en Linux
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versión preliminar) con el instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2795178cb975ecb620528c4a5dc8715b70d447fd
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342008"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Instalación de `azdata` para administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo instalar `azdata` para los clústeres de Big Data de SQL Server 2019 Release Candidate en Linux. Antes de que estos administradores de paquetes estuviesen disponibles, se requiere la instalación de `azdata` `pip`.

Los administradores de paquetes están diseñados para varios sistemas operativos y distribuciones.

- Para Linux (Ubuntu), [instale `azdata` con `apt`](#azdata-apt)

En este momento, no hay ningún administrador de paquetes para instalar `azdata` en otros sistemas operativos o distribuciones. Para estas plataformas, consulte [instalación de `azdata` sin el administrador de paquetes](./deploy-install-azdata.md).

## <a id="linux"></a>Instalación de `azdata` para Linux

el paquete de instalación de `azdata` está disponible para Ubuntu con `apt`.

### <a id="azdata-apt"></a>Instalación de `azdata` con apt (Ubuntu)

>[!NOTE]
>El paquete `azdata` no usa Python del sistema, sino que instala su propio intérprete de Python.

1. Obtener los paquetes necesarios para el proceso de instalación:

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
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. Actualice la información del repositorio e instale `azdata`:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Comprobar la instalación:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

Actualizar solo `azdata`:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Desinstalar

1. Desinstalar con apt-obtener quitar:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Quite la información del repositorio `azdata`:

    >[!NOTE]
    >Este paso no es necesario si planea instalar `azdata` en el futuro.

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. Quite la clave de firma:

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. Quite las dependencias innecesarias que se instalaron con la CLI de Azdata:

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, consulte [¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
