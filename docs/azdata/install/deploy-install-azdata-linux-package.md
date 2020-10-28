---
title: Instalación de la CLI de Azure Data (azdata) con apt
description: Aprenda a instalar la herramienta de la CLI de Azure Data (azdata) con apt.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f248978e09be4670d702805873a5ae6f4f7c9de
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257468"
---
# <a name="install-azure-data-cli-azdata-with-apt"></a>Instalación de [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] con apt

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Para las distribuciones de Linux con `apt`, hay un paquete para `azdata-cli`. El paquete de la CLI se ha probado en versiones de Linux que usan `apt`:

- Ubuntu 16.04, Ubuntu 18.04

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-apt"></a>Desinstalación con apt

>[!IMPORTANT]
> El paquete RPM de `azdata-cli` depende del paquete python3. En su sistema, esta puede ser una versión de Python anterior al requisito de *Python 3.6.x* . Si esto supone un problema, busque un paquete de python3 de reemplazo o siga las instrucciones de instalación manual que usan [`pip`](../install/deploy-install-azdata-pip.md).

1. Instale las dependencias necesarias para instalar `azdata-cli`.

   ```bash
   sudo apt-get update
   sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
   ```

2. Importe la clave del repositorio de Microsoft.

   ```bash
   curl -sL https://packages.microsoft.com/keys/microsoft.asc |
   gpg --dearmor |
   sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
   ```

3. Cree la información del repositorio local.

   Para el cliente Ubuntu 16.04, ejecute:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   Para el cliente Ubuntu 18.04, ejecute:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
    ```

   Para el cliente Ubuntu 20.04, ejecute:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/prod.list)
    ```

4. Instalar `azdata-cli`.

   ```bash
   sudo apt-get update
   sudo apt-get install -y azdata-cli
   ```

## <a name="verify-install"></a>Comprobación de la instalación

```bash
azdata
azdata --version
```

## <a name="update"></a>Actualizar

Actualice `azdata-cli` con los comandos `apt-get update` y `apt-get install`.

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

## <a name="uninstall"></a>Desinstalación

1. Elimine el paquete de su equipo.

   ```bash
   sudo apt-get remove -y azdata-cli
   ```

2. Quite la información del repositorio si no piensa volver a instalar `azdata-cli`.

   ```bash
   sudo rm /etc/apt/sources.list.d/azdata-cli.list
   ```

3. Quite la clave del repositorio.

   ```bash
   sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
   ```

4. Quite las dependencias que ya no sean necesarias.

   ```bash
   sudo apt autoremove
   ```

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.

Use azdata con [servicios de datos habilitados para Azure Arc](/azure/azure-arc/data/).