---
title: Instalación de la CLI de Azure Data (azdata) con Windows Installer
titleSuffix: ''
description: Aprenda a instalar la herramienta de la CLI de Azure Data (azdata) con el instalador.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9dd953a78a992a9a5fed7135ae0aee02f88e4de9
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257498"
---
# <a name="install-azure-data-cli-azdata-with-windows-installer"></a>Instalación de [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] con Windows Installer

[!INCLUDE [azdata](../../includes/applies-to-version/azdata.md)]

En este artículo se describe cómo instalar `azdata` en Windows con un instalador. Use `azdata` para administrar los clústeres de macrodatos de SQL Server o los servicios de datos habilitados para Azure Arc.

## <a name="steps-to-install-azdata-with-the-microsoft-windows-installer"></a>Pasos para instalar `azdata` con Microsoft Windows Installer

Para instalar `azdata` con Microsoft Windows Installer,

1. quite `azdata` si se instaló con `pip`. Si `azdata` se instaló con Windows Installer, continúe con el paso siguiente.
1. Instale `azdata` mediante [Windows Installer](https://aka.ms/azdata-msi).

### <a name="uninstall-azdata-with-windows-installer"></a>Desinstalación de `azdata` con Windows Installer

Para desinstalar `azdata` con Windows Installer, siga las instrucciones para el sistema operativo correspondiente.

| Plataforma      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| Inicio > Configuración > Aplicaciones                                |
| Windows 8     | Inicio > Panel de Control > Programas > Desinstalar un programa |

El programa que se va a desinstalar se denomina `Azdata CLI`. Seleccione esta aplicación y, después, haga clic en el botón `Uninstall`.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).

Use `azdata` con los [servicios de datos habilitados para Azure Arc](/azure/azure-arc/data/).
