---
title: Instalación de azdata mediante pip
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta azdata para instalar y administrar clústeres de macrodatos con pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 034514c13a65171fca9eb1fc20b6c496329816a1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773633"
---
# <a name="install-azdata-with-pip"></a>Instalación de `azdata` con `pip`

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

En este artículo se explica cómo instalar la herramienta `azdata` en Windows o Linux mediante `pip`.

Para Windows y Linux (distribución de Ubuntu), se puede realizar la instalación con un [administrador de paquetes](./deploy-install-azdata-installer.md) a fin de obtener una experiencia más sencilla.

## <a name="prerequisites"></a><a id="prerequisites"></a> Requisitos previos

`azdata` es una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar el clúster de macrodatos mediante las API REST. La versión mínima de Python necesaria es v3.5. Para descargar e instalar la herramienta `azdata` se requiere `pip`. Las instrucciones siguientes proporcionan ejemplos para Windows y Ubuntu. Para instalar Python en otras plataformas, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).
Además, instale y actualice la versión más reciente del paquete Python `requests`:

```bash
pip3 install -U requests
```

> [!IMPORTANT]
> Si va a instalar una versión más reciente de los clústeres de macrodatos, haga una copia de seguridad de los datos y elimine el clúster anterior actualizando `azdata` e instalando la versión nueva. Para obtener más información, consulte el artículo sobre [actualización a una nueva versión](deployment-upgrade.md).

## <a name="windows-azdata-installation"></a><a id="windows"></a> Instalación de `azdata` en Windows

1. En un cliente de Windows, descargue el paquete de Python necesario desde [https://www.python.org/downloads/](https://www.python.org/downloads/). Para Python 3.5.3 y versiones posteriores, al instalar Python también se instala pip3. 

   > [!TIP] 
   > Al instalar Python3, seleccione agregar Python al elemento `PATH`. Si no lo hace, más adelante podrá buscar dónde se encuentra pip3 y agregarlo manualmente al elemento `PATH`.

1. Abra una nueva sesión de Windows PowerShell para que obtenga la ruta de acceso más reciente con Python.

1. Si tiene instaladas versiones anteriores de `azdata`, es importante que las desinstale antes de instalar la versión más reciente.

   En CTP 3.2 o RC1, ejecute el comando siguiente.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   or
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale `azdata` con el comando siguiente:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="linux-azdata-installation"></a><a id="linux"></a> Instalación de `azdata` en Linux

En Linux, debe instalar Python 3.5 y, después, actualizar pip. En el ejemplo siguiente se muestran los comandos que funcionarían para Ubuntu. Para otras plataformas Linux, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Instale los paquetes de Python necesarios:

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. Actualice pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Si tiene instaladas versiones anteriores de `azdata`, es importante que las desinstale antes de instalar la versión más reciente.

   En CTP 3.2 o RC1, ejecute el comando siguiente.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   or
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale `azdata` con el comando siguiente:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > El modificador `--user` instala `azdata` en el directorio de instalación del usuario de Python. En Linux, habitualmente es `~/.local/bin`. Agregue este directorio a la ruta de acceso o bien navegue hasta el directorio de instalación del usuario y ejecute `./azdata` desde allí.

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> Instalación de `azdata` en macOS u OS X

Para instalar `azdata` en macOS u OS X complete estos pasos. Para cada paso, ejecute el ejemplo en Terminal.

1. En un cliente macOS, instale [Homebrew](https://brew.sh), si aún no lo tiene instalado:

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Instale, como mínimo, la versión 3.0 de Python y pip:

   ```
   brew install python3
   ```

1. Instale las dependencias:

   ```
   pip3 install -U requests
   brew install freetds
   ```

1. Si tiene instaladas versiones anteriores de la herramienta, es importante que las desinstale antes de instalar la versión más reciente de `azdata`. El comando siguiente quita la versión de `azdata`.

   ```
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale `azdata` con el comando siguiente:

   ```
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.
