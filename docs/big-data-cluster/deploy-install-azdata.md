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
ms.openlocfilehash: 40338c4083241fedd113bca3a1beb839dbdd3fca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75721803"
---
# <a name="install-azdata"></a>Instalar `azdata`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

`azdata` es una utilidad de línea de comandos escrita en Python para arrancar y administrar el clúster de macrodatos mediante las API REST. 

## <a name="find-latest-version"></a>Búsqueda de la versión más reciente

La lista de archivos de la versión más reciente siempre está disponible en [https://aka.ms/azdata](https://aka.ms/azdata).

Para averiguar la versión instalada y ver si tiene que actualizar, ejecute `azdata --version`.

## <a name="os-specific-instructions"></a>Instrucciones específicas del sistema operativo

* [Instalación en Windows](deploy-install-azdata-installer.md)
* [Instalación en macOS](deploy-install-azdata-macos.md)
* Instalación en Linux o en el [subsistema de Windows para Linux (WSL)](/windows/wsl/about/)
   * [Instalación con apt en Debian o Ubuntu](deploy-install-azdata-linux-package.md)
   * [Instalación con yum en RHEL o CentOS](deploy-install-azdata-yum.md)
   * [Instalación con Zypper en openSUSE o SLE](deploy-install-azdata-zypper.md)
   * [Instalación desde un script](deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.
