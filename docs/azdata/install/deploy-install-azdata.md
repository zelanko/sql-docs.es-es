---
title: Instalación de azdata
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y administrar Clústeres de macrodatos.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 408dec76480a36ff2280926147b948859fa7088d
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734098"
---
# <a name="install-azdata"></a>Instalar `azdata`

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

`azdata` es una utilidad de línea de comandos escrita en Python para arrancar y administrar el clúster de macrodatos mediante las API REST. 

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

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.
