---
title: Instalación de azdata
titleSuffix: SQL Server big data clusters
description: Aprenda a instalar la herramienta azdata para instalar y administrar clústeres de macrodatos SQL Server 2019 (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9444842081456563f411ad618f32b8dbd59f7513
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426445"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>Instalación de azdata para administrar clústeres de macrodatos SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo instalar la herramienta **azdata** para CTP 3,2 en Windows o Linux.

## <a id="prerequisites"></a> Requisitos previos

**azdata** es una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar el clúster de Big Data a través de las API de REST. La versión mínima de Python necesaria es v 3.5. También debe tener `pip` el que se usa para descargar e instalar la herramienta **azdata** . Las instrucciones siguientes proporcionan ejemplos para Windows y Ubuntu. Para instalar Python en otras plataformas, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Además, también debe instalar y actualizar la versión más reciente del paquete de Python de *solicitudes* :
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Si va a instalar una versión más reciente de los clústeres de Big Data, debe hacer una copia de seguridad de los datos y eliminar el clúster anterior *antes* de actualizar **azdata** e instalar la nueva versión. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

## <a id="windows"></a>Instalación de Windows azdata

1. En un cliente de Windows, descargue el paquete de Python [https://www.python.org/downloads/](https://www.python.org/downloads/)necesario desde. Para Python 3.5.3 y versiones posteriores, PIP3 también se instala al instalar Python. 

   > [!TIP] 
   > Al instalar Python3, seleccione Agregar Python a la **ruta de acceso**. Si no lo hace, puede encontrar más adelante dónde se encuentra PIP3 y agregarlo manualmente a la **ruta de acceso**.

1. Abra una nueva sesión de Windows PowerShell para que obtenga la ruta de acceso más reciente con Python.

1. Si tiene instaladas las versiones anteriores de la herramienta (previosly con el nombre **mssqlctl**), es importante desinstalarla antes de instalar la versión más reciente de **azdata**.

   Para CTP 3,1 o una versión anterior, ejecute el siguiente comando. Reemplace `ctp3.1` en el comando por la versión de **mssqlctl** que está desinstalando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Si tiene instaladas las versiones anteriores de **azdata** , es importante desinstalarlas antes de instalar la versión más reciente.

   Para CTP 3,2 o posterior, ejecute el siguiente comando. Reemplace `ctp3.2` en el comando por la versión de **azdata** que está desinstalando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale **azdata** con el siguiente comando:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Instalación de Linux azdata

En Linux, debe instalar Python 3,5 y, a continuación, actualizar pip. En el ejemplo siguiente se muestran los comandos que funcionarían para Ubuntu. Para otras plataformas Linux, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Instale los paquetes de Python necesarios:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. Actualizar PIP3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Si tiene versiones anteriores de la herramienta instaladas (anteriormente denominadas **mssqlctl**), es importante desinstalarlas antes de instalar la versión más reciente de **azdata**.

   Para CTP 3,1 o una versión anterior, ejecute el siguiente comando. Reemplace `ctp3.1` en el comando por la versión de **mssqlctl** que está desinstalando. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. Si tiene instaladas las versiones anteriores de **azdata** , es importante desinstalarlas antes de instalar la versión más reciente.

   Para CTP 3,2 o posterior, ejecute el siguiente comando. Reemplace `ctp3.2` en el comando por la versión de **azdata** que está desinstalando.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. Instale **azdata** con el siguiente comando:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > El `--user` modificador instala azdata en el directorio de instalación de usuario de Python. Normalmente `~/.local/bin` se encuentra en Linux. Agregue este directorio a la ruta de acceso o navegue hasta el directorio de instalación del `./azdata` usuario y ejecútelo desde allí.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, consulte [¿Qué son los clústeres de macrodatos SQL Server 2019?](big-data-cluster-overview.md).
