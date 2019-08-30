---
title: Instalación de azdata con Windows Installer
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] administrar (versión preliminar) con el instalador.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8dd5d2c7d0210880a82d774185a3f2a915608ec
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158150"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-with-windows-installer"></a>Instalar `azdata` para administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] con Windows Installer

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo `azdata` instalar para SQL Server 2019 Big Data clusters Release Candidate en Windows. Antes de que la instalación de Windows estuviera disponible, `azdata` se `pip`requiere la instalación de.

>Para Linux (Ubuntu), vea [instalar `azdata` con el instalador](./deploy-install-azdata-linux-package.md).

En este momento, no hay administradores de paquetes para instalar `azdata` en otros sistemas operativos o distribuciones. Para estas plataformas, vea [instalar `azdata` sin el administrador de paquetes](./deploy-install-azdata.md).

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Instale `azdata` con el Microsoft Windows Installer

Para instalar `azdata` con el Microsoft Windows Installer,

1. Quite `azdata` si se instaló con `pip`. Si `azdata` se instaló mediante Windows Installer, continúe con el paso siguiente.
1. Instale `azdata` mediante el Windows Installer.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>Desinstalar si la instalación anterior se realizó con`pip`

Si tiene instaladas las versiones anteriores de **mssqlctl** , quítelas. El siguiente comando quita la versión CTP 3,1 de **mssqlctl**.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

Si tiene instaladas las versiones anteriores `azdata` de, es importante desinstalarla antes de instalar la versión más reciente.

   Para CTP 3,2, ejecute el siguiente comando.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

Una vez quitado, [ `azdata` instale en Windows](#install-azdata-windows).

>[!NOTE]
>Si la instalación anterior se realizó con el MSI, no tendrá que desinstalar las versiones actuales antes de usar el instalador de MSI.

### <a id="install-azdata-windows"></a>Instalación con Windows Installer

Use el Windows Installer para instalar o actualizar `azdata` en Windows.

[Descargue el `azdata` Windows Installer](http://aka.ms/azdata-msi).

Cuando el instalador le pregunte si puede realizar cambios en el equipo, haga `Yes`clic en.

### <a name="uninstall-azdata-with-windows-installer"></a>Desinstalar `azdata` con Windows Installer

Para desinstalar `azdata` con Windows Installer, siga las instrucciones del sistema operativo adecuado.

| Plataforma      | Instrucciones                                           |
| ------------- |--------------------------------------------------------|
| Windows 10    | Inicio de la configuración de > > aplicaciones                                |
| Windows 8     | Iniciar > panel de control > programas > Desinstalar un programa |

Se llama **`Azdata CLI`** al programa que se va a desinstalar. Seleccione esta aplicación y, a continuación `Uninstall` , haga clic en el botón.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, vea [¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
