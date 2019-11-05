---
title: Descarga e instalación de sqlpackage | Microsoft Docs
description: Descarga e instalación de sqlpackage para Windows, macOS o Linux
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
ms.openlocfilehash: f966de4951e5c90dac8d6e48f00f8de6ff067e3c
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2019
ms.locfileid: "73033009"
---
# <a name="download-and-install-sqlpackage"></a>Descarga e instalación de sqlpackage

sqlpackage se ejecuta en Windows, macOS y Linux.

Descargue e instale la versión más reciente de .NET Framework y las versiones preliminares de macOS y Linux:

|Plataforma|Descargar|Fecha de la versión|Versión|Compilar
|:---|:---|:---|:---|:---|
|Windows (x64)|[Instalador MSI](https://go.microsoft.com/fwlink/?linkid=2108813)|29 de octubre de 2019|18.4|15.0.4573.2|
|macOS .NET Core (x64)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2108815)|29 de octubre de 2019| 18.4|15.0.4573.2|
|Linux .NET Core (x64) |[archivo zip](https://go.microsoft.com/fwlink/?linkid=2108814)|29 de octubre de 2019| 18.4|15.0.4573.2|
|Windows .NET Core (x64) |[archivo zip](https://go.microsoft.com/fwlink/?linkid=2109019)|29 de octubre de 2019| 18.4|15.0.4573.2|

Para más información sobre la última versión, consulte las [notas de la versión](release-notes-sqlpackage.md). Para descargar idiomas adicionales, consulte la sección [idiomas disponibles](#available-languages) .

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>Obtención de sqlpackage para Windows

En esta versión de sqlpackage se incluye una experiencia de instalación estándar de Windows y un archivo .zip: 

1. Descargue y ejecute el [instalador de DacFramework.msi para Windows](https://go.microsoft.com/fwlink/?linkid=2108813).
2. Abra una nueva ventana del símbolo del sistema y ejecute sqlpackage.exe.
    - sqlpackage se instala en la carpeta ```C:\Program Files\Microsoft SQL Server\150\DAC\bin```.

## <a name="get-sqlpackage-net-core-for-windows"></a>Obtener sqlpackage .NET Core para Windows

1. Descargue [sqlpackage para Windows](https://go.microsoft.com/fwlink/?linkid=2109019).
2. Para extraer el archivo, haga clic con el botón derecho en el archivo en el explorador de Windows y seleccione "extraer todo..." y seleccione el directorio de destino.
3. Abra una nueva ventana de terminal y el CD en la ubicación donde se extrajo sqlpackage:

   ```cmd
   > sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-macos"></a>Obtener sqlpackage .NET Core para macOS

1. Descargue [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=2108815).
2. Para extraer el archivo e iniciar sqlpackage, abra una nueva ventana de terminal y escriba los siguientes comandos:

   ```bash
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   $ echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   $ source ~/.bash_profile
   $ sqlpackage
   ```

## <a name="get-sqlpackage-net-core-for-linux"></a>Obtener sqlpackage .NET Core para Linux

1. Descargue [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=2108814) mediante uno de los instaladores o el archivo tar.gz:
2. Para extraer el archivo e iniciar sqlpackage, abra una nueva ventana de terminal y escriba los siguientes comandos:

   ```bash
   cd ~
   $ mkdir sqlpackage
   $ unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   $ echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   $ chmod a+x ~/sqlpackage/sqlpackage
   $ source ~/.bashrc
   $ sqlpackage
   ```

   > [!NOTE]
   > En Debian, Red Hat y Ubuntu, puede haber dependencias que faltan. Use los siguientes comandos para instalar estas dependencias según la versión de Linux:

   **Debian:**

   ```bash
   $ sudo apt-get install libunwind8
   ```

   **Redhat:**

   ```bash
   $ yum install libunwind
   $ yum install libicu
   ```

   **Ubuntu:**

   ```bash
   $ sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   $ sudo apt-get install libicu52      # for 14.x
   $ sudo apt-get install libicu55      # for 16.x
   $ sudo apt-get install libicu57      # for 17.x
   $ sudo apt-get install libicu60      # for 18.x
   ```

## <a name="uninstall-sqlpackage-preview"></a>Desinstalación de sqlpackage (versión preliminar)

Si ha instalado sqlpackage con el instalador de Windows, desinstale de la misma manera que quita cualquier aplicación de Windows.

Si ha instalado sqlpackage con un archivo .zip u otro archivo, elimine los archivos.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

sqlpackage se ejecuta en Windows, macOS y Linux, y es compatible con las siguientes plataformas:

### <a name="windows"></a>Windows

- Windows 10
- Windows 8.1
- Windows 7 SP1
- Windows Server 2008 R2
- Windows Server 2012 R2
- Windows Server 2016

### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="available-languages"></a>Idiomas disponibles

Esta versión de sqlpackage puede instalarse en los idiomas siguientes:

Ventanas de sqlpackage:  
[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2108813&clcid=0x40a)

Windows sqlpackage .NET Core:  
[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2109019&clcid=0x40a)

sqlpackage .NET Core macOS:  
[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2108815&clcid=0x40a)

sqlpackage .NET Core Linux:  
[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2108814&clcid=0x40a)

## <a name="next-steps"></a>Next Steps

- Mas información sobre [sqlpackage](sqlpackage.md)

[Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
