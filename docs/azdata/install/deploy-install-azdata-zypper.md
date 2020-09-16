---
title: Instalación de azdata con zypper
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y administrar Clústeres de macrodatos con zypper.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2445fecc554ff9f7816bbf75483ab49bbee542c1
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734095"
---
# <a name="install-azdata-with-zypper"></a>Instale `azdata` con zypper

Para las distribuciones de Linux con `zypper`, hay un paquete para `azdata-cli`. El paquete de la CLI se ha probado en versiones de Linux que usan `zyper`:

- openSUSE 42.2 (leap) +
- SLES 12 SP 2 +

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>Instalación con zypper
>[!IMPORTANT]
>El paquete RPM de `azdata-cli` depende del paquete python3. En su sistema, esta puede ser una versión de Python anterior al requisito de *Python 3.6.x*. Si esto supone un problema, busque un paquete de python3 de reemplazo o siga las instrucciones de instalación manual que usan [`pip`](../install/deploy-install-azdata-pip.md).

1. Instale las dependencias necesarias para instalar `azdata-cli`

   ```bash
   sudo zypper install -y curl
   ```

1. Importe la clave del repositorio de Microsoft

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Cree información del repositorio local

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   ```

1. Instalar

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

Quite el paquete de su sistema

```bash
   sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.
