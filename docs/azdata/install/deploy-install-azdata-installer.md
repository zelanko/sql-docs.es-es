---
title: Instalación de azdata con Windows Installer
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y administrar clústeres de macrodatos de SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60d3b60f98a93cb6b724cd569fb2871adec3f1ce
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734083"
---
# <a name="install-azdata-to-manage-big-data-clusters-2019-with-windows-installer"></a>Instalación de `azdata` para administrar [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] con Windows Installer

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

En este artículo se describe cómo instalar `azdata` para clústeres de macrodatos de SQL Server 2019 en Windows. Antes de que la instalación de Windows estuviera disponible, la instalación de `azdata` requería `pip`.

>Para Linux (Ubuntu), consulte cómo [instalar `azdata` con el instalador](./deploy-install-azdata-linux-package.md).

En este momento no hay ningún administrador de paquetes para instalar `azdata` en otros sistemas operativos o distribuciones. Para estas plataformas, consulte cómo [instalar `azdata` sin el administrador de paquetes](./deploy-install-azdata.md).

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Instalación de `azdata` con Microsoft Windows Installer

Para instalar `azdata` con Microsoft Windows Installer,

1. quite `azdata` si se instaló con `pip`. Si `azdata` se instaló con Windows Installer, continúe con el paso siguiente.
1. Instale `azdata` mediante Windows Installer.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>Desinstalación si la instalación anterior se realizó con `pip`

Si tiene instaladas versiones anteriores de `azdata`, es importante que las desinstale antes de instalar la versión más reciente.

   Para quitar la versión candidata para lanzamiento de `azdata`, ejecute el siguiente comando.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

Una vez quitada, [instale `azdata` en Windows](#install-azdata-windows).

>[!NOTE]
>Si la instalación anterior se realizó con MSI, no necesitará desinstalar las versiones actuales antes de usar el instalador MSI.

### <a name="install-with-windows-installer"></a><a id="install-azdata-windows"></a>Instalación con Windows Installer

Use Windows Installer para instalar o actualizar `azdata` en Windows.

[Descargue `azdata` Windows Installer](https://aka.ms/azdata-msi).

Cuando el instalador le pregunte si puede realizar cambios en el equipo, haga clic en `Yes`.

### <a name="uninstall-azdata-with-windows-installer"></a>Desinstalación de `azdata` con Windows Installer

Para desinstalar `azdata` con Windows Installer, siga las instrucciones para el sistema operativo correspondiente.

| Plataforma      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| Inicio > Configuración > Aplicaciones                                |
| Windows 8     | Inicio > Panel de Control > Programas > Desinstalar un programa |

El programa que se va a desinstalar se denomina `Azdata CLI`. Seleccione esta aplicación y, después, haga clic en el botón `Uninstall`.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md).