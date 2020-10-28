---
title: Instalación de la CLI de Azure Data (azdata) con pip
titleSuffix: ''
description: Obtenga información sobre cómo instalar la herramienta azdata con pip.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4aa52ebe56cbe4af3d2983a9ed800ebbc1538971
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257459"
---
# <a name="install-azure-data-cli-azdata-with-pip"></a>Instalación de [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] con `pip`

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

En este artículo se explica cómo instalar la herramienta [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] en Windows, Linux o macOS/OS X mediante `pip`.

> [!TIP]
> Para obtener una experiencia más sencilla, `azdata` se puede instalar con un [administrador de paquetes](./deploy-install-azdata.md) para Windows, Linux (distribuciones de Ubuntu, Debian, RHEL, CentOS, openSUSE y SLE) y macOS.

## <a name="prerequisites"></a><a id="prerequisites"></a> Requisitos previos

`azdata` es una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar recursos de datos mediante API REST. La versión mínima de Python necesaria es v3.5. Para descargar e instalar la herramienta `azdata`, se requiere `pip`. En las instrucciones siguientes se proporcionan ejemplos para Windows, Linux (Ubuntu) y macOS/OS X. Para instalar Python en otras plataformas, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download). Además, instale y actualice la versión más reciente del paquete Python `requests`:

```bash
pip3 install -U requests
```

## <a name="windows-azdata-installation"></a><a id="windows"></a> Instalación de `azdata` en Windows

1. En un cliente de Windows, descargue el paquete de Python necesario desde [https://www.python.org/downloads/](https://www.python.org/downloads/). Para Python 3.5.3 y versiones posteriores, al instalar Python también se instala pip3.

   > [!TIP]
   > Al instalar Python3, seleccione agregar Python al elemento `PATH`. Si no lo hace, más adelante podrá buscar dónde se encuentra pip3 y agregarlo manualmente al elemento `PATH`.

1. Abra una nueva sesión de Windows PowerShell para que obtenga la ruta de acceso más reciente con Python.

1. A partir de la versión SQL Server 2019 CU5, azdata tiene una versión semántica independiente del servidor. Si tiene instaladas versiones anteriores de `azdata`, es importante que las desinstale antes de instalar la versión más reciente.

   Por ejemplo, para 2019-cu4, ejecute el siguiente comando:

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu4/requirements.txt
   ```

  > [!NOTE]
  > En los ejemplos anteriores, reemplace `2019-cu6` por la versión y CU de la instalación de `azdata`. 

1. Instalar `azdata`.

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

1. Actualice pip3.

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. A partir de la versión SQL Server 2019 CU5, azdata tiene una versión semántica independiente del servidor. Si tiene instaladas versiones anteriores de `azdata`, es importante que las desinstale antes de instalar la versión más reciente.

   Por ejemplo, para `2019-cu6`, ejecute el siguiente comando:

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu6/requirements.txt
   ```

  > [!NOTE]
  > En los ejemplos anteriores, reemplace `2019-cu6` por la versión y CU de la instalación de `azdata`.

1. Instalar `azdata`.

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > El modificador `--user` instala `azdata` en el directorio de instalación del usuario de Python. En Linux, habitualmente es `~/.local/bin`. Agregue este directorio a la ruta de acceso o bien navegue hasta el directorio de instalación del usuario y ejecute `./azdata` desde allí.

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> Instalación de `azdata` en macOS u OS X

Para instalar `azdata` en macOS u OS X complete estos pasos. Para cada paso, ejecute el ejemplo en Terminal.

1. En un cliente macOS, instale [Homebrew](https://brew.sh), si aún no lo tiene instalado:

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Instale, como mínimo, la versión 3.0 de Python y pip:

   ```bash
   brew install python3
   ```

1. Instale las dependencias:

   ```bash
   pip3 install -U requests
   brew install freetds
   ```

1. A partir de la versión SQL Server 2019 CU5, azdata tiene una versión semántica independiente del servidor. Si tiene instaladas versiones anteriores de `azdata`, es importante que las desinstale antes de instalar la versión más reciente. Por ejemplo, el comando siguiente quita la versión RC1 de `azdata`:

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instale la CLI de Azure Data.

   ```bash
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md) para obtener más información sobre los clústeres de macrodatos.

Use azdata con [servicios de datos habilitados para Azure Arc](/azure/azure-arc/data/).
