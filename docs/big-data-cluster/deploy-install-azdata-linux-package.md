---
title: Instalación de azdata con el instalador en Linux
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] administrar (versión preliminar) con el instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e11e4851294ac8ffd8efa66e2156dcd47bce3aa0
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160681"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>Instalar `azdata` para administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo `azdata` instalar para SQL Server 2019 Big Data clusters Release Candidate en Linux. Antes de que estos administradores de paquetes estuviesen disponibles `azdata` , `pip`se requiere la instalación de.

Los administradores de paquetes están diseñados para varios sistemas operativos y distribuciones.

- Para Linux (Ubuntu), [instale `azdata` con `apt` ](#azdata-apt)

En este momento, no hay administradores de paquetes para instalar `azdata` en otros sistemas operativos o distribuciones. Para estas plataformas, vea [instalar `azdata` sin el administrador de paquetes](./deploy-install-azdata.md).

## <a id="linux"></a>Instalación `azdata` para Linux

`azdata`el paquete de instalación está disponible para `apt`Ubuntu con.

### <a id="azdata-apt"></a>Instalación `azdata` con apt (Ubuntu)

>[!NOTE]
>El `azdata` paquete no usa Python del sistema, sino que instala su propio intérprete de Python.

1. Obtener los paquetes necesarios para el proceso de instalación:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. Descargue e instale la clave de firma:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```

3. Agregue la `azdata` información del repositorio:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. Actualizar información del repositorio e `azdata`instalar:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. Comprobar la instalación:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Actualizar

Solo `azdata` actualización:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Desinstalar

1. Desinstalar con apt-obtener quitar:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. Quite la `azdata` información del repositorio:

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

Para obtener más información sobre los clústeres de Big Data, vea [¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
