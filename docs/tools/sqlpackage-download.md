---
title: Descargue e instale sqlpackage | Documentos de Microsoft
description: Descargue e instale sqlpackage para Windows, Mac OS o Linux
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 4e5528ca046de83385171890fbda389928e41cf3
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703852"
---
# <a name="download-and-install-sqlpackage"></a>Descargue e instale sqlpackage

Sqlpackage se ejecuta en Windows, Mac OS y Linux.

Descargue e instale la versión más reciente de .NET Framework y macOS y vistas previas de Linux:

|Plataforma|Descargar|Fecha de la versión|Versión|Compilar|
|:---|:---|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=875508)|25 de enero de 2018|17.4.1|14.0.3917.1|
|macOS (versión preliminar)|[.zip](https://go.microsoft.com/fwlink/?linkid=873927)|9 de mayo de 2018 |0.0.1|15.0.4057.1|
|Linux (versión preliminar)|[.zip](https://go.microsoft.com/fwlink/?linkid=873926)|9 de mayo de 2018 |0.0.1|15.0.4057.1|

## <a name="get-sqlpackage-for-windows"></a>Obtener sqlpackage para Windows

Esta versión de sqlpackage incluye una experiencia de instalador de Windows estándar y .zip: 

**Instalador**

1. Descargue y ejecute la [DacFramework.msi instalador para Windows](https://go.microsoft.com/fwlink/?linkid=875508).
2. Abra una nueva ventana de símbolo del sistema y ejecute sqlpackage.exe
    - Sqlpackage se instala en el ```C:\Program Files\Microsoft SQL Server\140\DAC\bin``` carpeta

## <a name="get-sqlpackage-preview-for-macos"></a>Obtener sqlpackage (versión preliminar) para macOS

1. Descargar [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=873927).
2. Para extraer el archivo e iniciar sqlpackage, abra una nueva ventana de Terminal y escriba los siguientes comandos:

   **Instalación del archivo .zip:**
   ```bash 
   mv ~/Downloads/sqlpackage-linux-<version string> ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage 
   ``` 

## <a name="get-sqlpackage-preview-for-linux"></a>Obtener sqlpackage (versión preliminar) para Linux

1. Descargar [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=873926) mediante uno de los instaladores o el archivo tar.gz:
2. Para extraer el archivo e iniciar sqlpackage, abra una nueva ventana de Terminal y escriba los siguientes comandos:

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
   > En Debian, Redhat y Ubuntu, pueden tener dependencias que faltan. Use los comandos siguientes para instalar estas dependencias según su versión de Linux:
   

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

Si ha instalado sqlpackage con Windows installer, a continuación, desinstale la misma manera que quite cualquier aplicación de Windows.

Si instaló sqlpackage con .zip o en otro contenedor, basta con eliminar los archivos.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

Sqlpackage se ejecuta en Windows, Mac OS y Linux y es compatible con las siguientes plataformas:

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
- macOS 10.13 Sierra alta
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- Obtenga más información sobre [sqlpackage](sqlpackage.md)

[Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
