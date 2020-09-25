---
title: Instalación de azdata con yum
titleSuffix: ''
description: Obtenga información sobre cómo instalar la herramienta azdata con yum.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eae81ccee65899335b161b3a32fbb260d0a8517a
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914896"
---
# <a name="install-azdata-with-yum"></a>Instalación de `azdata` con yum

Para las distribuciones de Linux con `yum`, hay un paquete para `azdata-cli`. El paquete de la CLI se ha probado en versiones de Linux que usan `yum`:

- RHEL 7, RHEL 8


[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>Instalación con yum

>[!IMPORTANT]
> El paquete RPM de `azdata-cli` depende del paquete python3. En su sistema, esta puede ser una versión de Python anterior al requisito de *Python 3.6.x*. Si esto supone un problema, busque un paquete de python3 de reemplazo o siga las instrucciones de instalación manual que usan [`pip`](../install/deploy-install-azdata-pip.md).

1. Importe la clave del repositorio de Microsoft

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. Cree información del repositorio local

   Para una ejecución de cliente RHEL 7:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```
  
   Para una ejecución de cliente RHEL 8:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

1. Realice la instalación con el comando `yum install`.

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>Comprobación de la instalación

```
azdata
azdata --version
```

## <a name="update"></a>Actualizar

Actualice `azdata-cli` con el comando `yum update`.

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>Desinstalación

1. Quite el paquete de su sistema

   ```bash
   sudo yum remove azdata-cli
   ```

1. Quite la información del repositorio si no piensa volver a instalar `azdata-cli`

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.

Use azdata con [servicios de datos habilitados para Azure Arc](/azure/azure-arc/data/).
