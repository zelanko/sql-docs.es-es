---
title: Descargue e instale sqlpackage | Microsoft Docs
description: Descargue e instale sqlpackage para Windows, macOS o Linux
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sqlpackage
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: fa682766fe4330a34cff39600b6296403031a3e4
ms.sourcegitcommit: 0dff9dd43e80eee900eb92d25df9ca18397f3485
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37080043"
---
# <a name="download-and-install-sqlpackage"></a>Descargue e instale sqlpackage

Sqlpackage se ejecuta en Windows, macOS y Linux.

Descargue e instale la versión más reciente de .NET Framework y macOS y Linux las versiones preliminares:

|Plataforma|Descargar|Fecha de la versión|Versión|Compilar|
|:---|:---|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=875508)|22 de junio de 2018|17.8|14.0.4079.2|
|macOS (versión preliminar)|[.zip](https://go.microsoft.com/fwlink/?linkid=873927)|9 de mayo de 2018 |0.0.1|15.0.4057.1|
|Linux (versión preliminar)|[.zip](https://go.microsoft.com/fwlink/?linkid=873926)|9 de mayo de 2018 |0.0.1|15.0.4057.1|

Para obtener más información acerca de la versión más reciente, consulte el [notas de la versión](sqlpackage-release-notes.md).

## <a name="get-sqlpackage-for-windows"></a>Obtener sqlpackage para Windows

Esta versión de sqlpackage incluye una experiencia de instalador de Windows estándar y un archivo .zip: 

1. Descargue y ejecute el [DacFramework.msi installer para Windows](https://go.microsoft.com/fwlink/?linkid=875508).
2. Abra una nueva ventana de símbolo del sistema y ejecute sqlpackage.exe
    - Sqlpackage se instala en el ```C:\Program Files\Microsoft SQL Server\140\DAC\bin``` carpeta

## <a name="get-sqlpackage-preview-for-macos"></a>Obtener sqlpackage (versión preliminar) para macOS

1. Descargar [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=873927).
2. Para extraer el archivo e inicia sqlpackage, abra una nueva ventana de Terminal y escriba los siguientes comandos:

   **Instalación del archivo .zip:**

   ```bash
   mv ~/Downloads/sqlpackage-linux-<version string> ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-preview-for-linux"></a>Obtener sqlpackage (versión preliminar) para Linux

1. Descargar [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=873926) mediante uno de los instaladores o el archivo tar.gz:
2. Para extraer el archivo e inicia sqlpackage, abra una nueva ventana de Terminal y escriba los siguientes comandos:

   **Instalación del archivo .zip:**

   ```bash
   cd ~
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bashrc
   source ~/.bashrc
   sqlpackage
   ```

   > [!NOTE]
   > En Debian, Red Hat y Ubuntu, puede tener dependencias que faltan. Use los siguientes comandos para instalar estas dependencias según la versión de Linux:

   **Debian:**

   ```bash
   sudo apt-get install libuwind8
   ```

   **Redhat:**

   ```bash
   yum install libunwind
   yum install libicu
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   sudo apt-get install libicu52      # for 14.x
   sudo apt-get install libicu55      # for 16.x
   sudo apt-get install libicu57      # for 17.x
   sudo apt-get install libicu60      # for 18.x
   ```

## <a name="uninstall-sqlpackage-preview"></a>Desinstalar sqlpackage (versión preliminar)

Si instaló sqlpackage con el instalador de Windows, a continuación, desinstale la misma manera que quite cualquier aplicación de Windows.

Si ha instalado sqlpackage con un archivo .zip o de otro archivo, basta con eliminar los archivos.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

Sqlpackage se ejecuta en Windows, macOS y Linux y es compatible con las siguientes plataformas:

### <a name="windows"></a>Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2

### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- Obtenga más información sobre [sqlpackage](sqlpackage.md)

[Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)