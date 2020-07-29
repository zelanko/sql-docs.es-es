---
title: Instalación de azdata con instalador en Linux
titleSuffix: SQL Server big data clusters
description: Aprenda a instalar la herramienta azdata para instalar y administrar clústeres de macrodatos de SQL Server con el instalador (Linux).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 304515dcd288978c0d85ab992312eb2444430bfc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773642"
---
# <a name="install-azdata-with-apt"></a>Instalación de `azdata` con apt

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

En este artículo se explica cómo instalar `azdata` para clústeres de macrodatos de SQL Server 2019 en Linux. Antes de que estos administradores de paquetes estuviesen disponibles, la instalación de `azdata` exigía `pip`.

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-azdata-for-linux"></a><a id="linux"></a>Instalar `azdata` para Linux

El paquete de instalación `azdata` está disponible para Ubuntu con `apt`.

### <a name="install-azdata-with-apt-ubuntu"></a><a id="azdata-apt"></a>Instalar `azdata` con apt (Ubuntu)

>[!NOTE]
>El paquete `azdata` no usa el sistema Python, sino que instala su propio intérprete de Python.

1. Obtenga los paquetes necesarios para el proceso de instalación:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
    ```

2. Descargue e instale la clave de firma:

    ```bash
    curl -sL https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
    ```

3. Agregue la información del repositorio `azdata`.

   Para el cliente Ubuntu 16.04, ejecute:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

   Para el cliente Ubuntu 18.04, ejecute:
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
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

### <a name="update"></a>Actualizar

Actualice `azdata` únicamente:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Desinstalación

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

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.
