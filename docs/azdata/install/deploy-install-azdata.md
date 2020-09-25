---
title: Instalación de azdata
titleSuffix: ''
description: Obtenga información sobre cómo instalar la herramienta azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 7939aa1575aaeec8edff33a9a9f7101a1014abc2
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914917"
---
# <a name="install-azdata"></a>Instalar `azdata`

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/azdata.md)]

`azdata` es una utilidad de línea de comandos escrita en Python para arrancar los servicios de datos y administrarlos mediante las API REST. 

## <a name="find-latest-version"></a>Búsqueda de la versión más reciente

La lista de archivos de la versión más reciente siempre está disponible en [https://aka.ms/azdata](https://aka.ms/azdata).

Para averiguar la versión instalada y ver si tiene que actualizar, ejecute `azdata --version`.

## <a name="os-specific-instructions"></a>Instrucciones específicas del sistema operativo

* [Instalación en Windows](../install/deploy-install-azdata-installer.md)
* [Instalación en macOS](../install/deploy-install-azdata-macos.md)
* Instalación en Linux o en el [subsistema de Windows para Linux (WSL)](/windows/wsl/about/)
   * [Instalación con apt en Debian o Ubuntu](../install/deploy-install-azdata-linux-package.md)
   * [Instalación con yum en RHEL o CentOS](../install/deploy-install-azdata-yum.md)
   * [Instalación con Zypper en openSUSE o SLE](../install/deploy-install-azdata-zypper.md)
   * [Instalación desde un script](../install/deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>Pasos siguientes

Use azdata con Clústeres de macrodatos, vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Use azdata con [servicios de datos habilitados para Azure Arc](/azure/azure-arc/data/).
