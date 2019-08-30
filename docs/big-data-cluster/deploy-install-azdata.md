---
title: Instalación de azdata con PIP
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] administrar (versión preliminar) con PIP.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a72e2ab39a17adef6c330f1ae17dcdc8a5dd8ddf
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160732"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>Instalar `azdata` para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] usar`pip`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo instalar `azdata` la herramienta para el candidato de versión comercial en Windows `pip`o Linux mediante.

## <a id="prerequisites"></a> Requisitos previos

`azdata`es una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar el clúster de Big Data a través de las API de REST. La versión mínima de Python necesaria es v3.5. También debe tener `pip` el que se usa para descargar e instalar `azdata` la herramienta. Las instrucciones siguientes proporcionan ejemplos para Windows y Ubuntu. Para instalar Python en otras plataformas, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Además, también debe instalar y actualizar la versión más reciente del paquete de Python de *solicitudes*:
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Si va a instalar una versión más reciente de los clústeres de Big Data, debe hacer una copia de seguridad de los datos y `azdata` eliminar el clúster anterior antes de actualizar e instalar la nueva versión. Para obtener más información, consulte el artículo sobre [actualización a una nueva versión](deployment-upgrade.md).

## <a id="windows"></a>Instalación `azdata` de Windows

1. En un cliente de Windows, descargue el paquete de Python necesario desde [https://www.python.org/downloads/](https://www.python.org/downloads/). Para Python 3.5.3 y versiones posteriores, al instalar Python también se instala pip3. 

   > [!TIP] 
   > Al instalar Python3, seleccione Agregar Python a la **ruta de acceso**. Si no lo hace, puede buscar más adelante dónde se encuentra pip3 y agregarlo manualmente a la **ruta de acceso**.

1. Abra una nueva sesión de Windows PowerShell para que obtenga la ruta de acceso más reciente con Python.

1. Si tiene instaladas versiones anteriores de la herramienta (antes de la versión de CTP 3,2, la herramienta se llamaba **mssqlctl**), es importante desinstalarla antes de instalar la versión más reciente `azdata`de. El siguiente comando quita la versión CTP 3,1 de **mssqlctl**.

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Si tiene instaladas las versiones anteriores `azdata` de, es importante desinstalarla antes de instalar la versión más reciente.

   Para CTP 3,2, ejecute el siguiente comando.

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. Instale `azdata` con el siguiente comando:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Instalación `azdata` de Linux

En Linux, debe instalar Python 3.5 y, después, actualizar pip. En el ejemplo siguiente se muestran los comandos que funcionarían para Ubuntu. Para otras plataformas Linux, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Instale los paquetes de Python necesarios:

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip
   ```

1. Actualice pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Si tiene instaladas versiones anteriores de la herramienta (antes de la versión de CTP 3,2, la herramienta se llamaba **mssqlctl**), es importante desinstalarla antes de instalar la versión más reciente `azdata`de. El siguiente comando quita la versión CTP 3,1 de **mssqlctl**.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Si tiene instaladas las versiones anteriores `azdata` de, es importante desinstalarla antes de instalar la versión más reciente.

   Para CTP 3,2, ejecute el siguiente comando.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. Instale `azdata` con el siguiente comando:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > El `--user` modificador `azdata` se instala en el directorio de instalación de usuario de Python. En Linux, habitualmente es `~/.local/bin`. Agregue este directorio a la ruta de acceso o bien navegue hasta el directorio de instalación del usuario y ejecute `./azdata` desde allí.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, vea [¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
