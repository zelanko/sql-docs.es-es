---
title: Instalación de la CLI de Azure Data (azdata) con zypper
titleSuffix: ''
description: Aprenda a instalar la herramienta de la CLI de Azure Data (azdata) con zypper.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d43a1f9c65aa17fae3d262a51f45105b5f583cdd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257518"
---
# <a name="install-azure-data-cli-azdata-with-zypper"></a>Instale [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] con zypper

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

Para las distribuciones de Linux con `zypper`, hay un paquete para `azdata-cli`. El paquete de la CLI se ha probado en versiones de Linux que usan `zypper`:

- openSUSE 42.2 (leap) +
- SLES 12 SP 2 +

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>Instalación con zypper

>[!IMPORTANT]
>El paquete RPM de `azdata-cli` depende del paquete python3. En su sistema, esta puede ser una versión de Python anterior al requisito de *Python 3.6.x* . Si esto supone un problema, busque un paquete de python3 de reemplazo o siga las instrucciones de instalación manual que usan [`pip`](../install/deploy-install-azdata-pip.md).

1. Instale las dependencias necesarias para instalar `azdata-cli`.

   ```bash
   sudo zypper install -y curl
   ```

1. Importe la clave del repositorio de Microsoft.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Cree la información del repositorio local.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
   ```

1. Instalar `azdata-cli`.

   ```bash
   sudo zypper install --from packages-microsoft-com-mssql-server-2019 -y azdata-cli
   ```

## <a name="verify-install"></a>Comprobación de la instalación

```bash
azdata
azdata --version
```

## <a name="update"></a>Actualizar

Actualice `azdata-cli` con el comando `zypper update`.

```bash
sudo zypper refresh
sudo zypper update azdata-cli
```

## <a name="uninstall"></a>Desinstalación

Elimine el paquete de su equipo.

```bash
sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.

Use azdata con [servicios de datos habilitados para Azure Arc](/azure/azure-arc/data/).