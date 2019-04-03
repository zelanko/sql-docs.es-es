---
title: Instalación de mssqlctl
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo instalar la herramienta mssqlctl para instalar y administrar clústeres de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c306ec99f0bd2aff89116e955283dd585f9d7cce
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860666"
---
# <a name="install-mssqlctl-to-manage-sql-server-big-data-clusters"></a>Instalar mssqlctl para administrar clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo instalar el **mssqlctl** herramienta en Windows o Linux.

**mssqlctl** es una utilidad de línea de comandos escrita en Python que habilita los administradores para arrancar y administrar el clúster de macrodatos mediante las API de REST de clúster. La versión de Python mínima requerida es v3.5. También debe tener `pip` que se utiliza para descargar e instalar **mssqlctl** herramienta. Las instrucciones siguientes proporcionan ejemplos para Windows y Ubuntu. Para instalar Python en otras plataformas, consulte el [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

> [!IMPORTANT]
> Si va a instalar una versión más reciente de los clústeres de datos de gran tamaño, debe los datos de copia de seguridad y eliminar el clúster antiguo *antes* actualizar **mssqlctl** e instalar la nueva versión. Para obtener más información, consulte [actualizar a una nueva versión](deployment-guidance.md#upgrade).

## <a id="windows"></a> Instalación de Windows mssqlctl

1. En un cliente de Windows, descargue el paquete de Python necesario [ https://www.python.org/downloads/ ](https://www.python.org/downloads/). Python3.5.3 y versiones posteriores, pip3 también se instala al instalar Python. 

   > [!TIP] 
   > Al instalar Python3, seleccione esta opción para agregar Python a su **ruta de acceso**. Si no lo hace, puede encontrar más adelante en el que se encuentra pip3 y agregarlo manualmente a su **ruta de acceso**.

1. Abra una nueva sesión de Windows PowerShell para que obtiene la ruta de acceso más reciente con Python en él.

1. Si tiene cualquier versión anterior de **mssqlctl** instalado, es importante que desinstale **mssqlctl** primero antes de instalar la versión más reciente.

   Si está mssqlctl unisntalling correspondiente a la versión 2.2 o inferior de la versión de CTP, ejecute:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   Para CTP2.3 o ejecución superior (reemplace `ctp-2.3` en el comando con la versión de mssqlctl está desinstalando):

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. Instalar **mssqlctl** con el siguiente comando:

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt
   ```

## <a id="linux"></a> Instalación de Linux mssqlctl

En Linux, debe instalar Python 3.5 y, a continuación, actualizar pip. El ejemplo siguiente muestra los comandos que funcionarían para Ubuntu. Para otras plataformas Linux, consulte el [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Instalar los paquetes de Python necesarios:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. Actualizar pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. Si tiene cualquier versión anterior de **mssqlctl** instalado, es importante que desinstale **mssqlctl** primero antes de instalar la versión más reciente.

   Si está mssqlctl unisntalling correspondiente a la versión 2.2 o inferior de la versión de CTP, ejecute:

   ```bash
   pip3 uninstall mssqlctl
   ```

   Para CTP2.3 o ejecución superior (reemplace `ctp-2.3` en el comando con la versión de mssqlctl está desinstalando):

   ```bash
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. Instalar **mssqlctl** con el siguiente comando:

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.4/mssqlctl/requirements.txt --user
   ```

   > [!NOTE]
   > El `--user` modificador instala mssqlctl al directorio de instalación de usuario de Python. Este suele ser `~/.local/bin` en Linux. Ya sea agregar este directorio a la ruta de acceso o vaya al directorio de instalación de usuario y ejecute `./mssqlctl` desde allí.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
