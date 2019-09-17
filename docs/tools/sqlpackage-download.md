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
ms.openlocfilehash: 01654df047d2dc78014c6e8c41edbb370d15da60
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874392"
---
# <a name="download-and-install-sqlpackage"></a>Descarga e instalación de sqlpackage

sqlpackage se ejecuta en Windows, macOS y Linux.

Descargue e instale la versión más reciente de .NET Framework y las versiones preliminares de macOS y Linux:

|Plataforma|Descargar|Fecha de la versión|Versión|Compilar
|:---|:---|:---|:---|:---|
|Windows|[Instalador MSI](https://go.microsoft.com/fwlink/?linkid=2102893)|6 de septiembre de 2019|18,3|15.0.4532.1|
|macOS .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2102894)|6 de septiembre de 2019| 18,3|15.0.4532.1|
|Linux .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2102978)|6 de septiembre de 2019| 18,3|15.0.4532.1|
|Windows .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2102979)|6 de septiembre de 2019| 18,3|15.0.4532.1|

Para más información sobre la última versión, consulte las [notas de la versión](release-notes-sqlpackage.md).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>Obtención de sqlpackage para Windows

En esta versión de sqlpackage se incluye una experiencia de instalación estándar de Windows y un archivo .zip: 

1. Descargue y ejecute el [instalador de DacFramework.msi para Windows](https://go.microsoft.com/fwlink/?linkid=2102893).
2. Abra una nueva ventana del símbolo del sistema y ejecute sqlpackage.exe.
    - sqlpackage se instala en la carpeta ```C:\Program Files\Microsoft SQL Server\150\DAC\bin```.
    - Si se instala la versión x86 en una máquina x64, sqlpackage se instala en la carpeta ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin```.

## <a name="get-sqlpackage-net-core-preview-for-windows"></a>Obtener sqlpackage .NET Core (versión preliminar) para Windows

1. Descargue [sqlpackage para Windows](https://go.microsoft.com/fwlink/?linkid=2102979).
2. Para extraer el archivo, haga clic con el botón derecho en el archivo en el explorador de Windows y seleccione "extraer todo..." y seleccione el directorio de destino.
3. Abra una nueva ventana de terminal, puede abrir el CD en la ubicación donde se Exracted sqlpackage:

   **Instalación del archivo .zip:**

   ```bash
   sqlpackage
   ```

## <a name="get-sqlpackage-net-core-preview-for-macos"></a>Obtener sqlpackage .NET Core (versión preliminar) para macOS

1. Descargue [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=2102894).
2. Para extraer el archivo e iniciar sqlpackage, abra una nueva ventana de terminal y escriba los siguientes comandos:

   **Instalación del archivo .zip:**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-net-core-preview-for-linux"></a>Obtención de sqlpackage .NET Core (versión preliminar) para Linux

1. Descargue [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=2102978) mediante uno de los instaladores o el archivo tar.gz:
2. Para extraer el archivo e iniciar sqlpackage, abra una nueva ventana de terminal y escriba los siguientes comandos:

   **Instalación del archivo .zip:**

   ```bash
   cd ~
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   chmod a+x ~/sqlpackage/sqlpackage
   source ~/.bashrc
   sqlpackage
   ```

   > [!NOTE]
   > En Debian, Red Hat y Ubuntu, puede haber dependencias que faltan. Use los siguientes comandos para instalar estas dependencias según la versión de Linux:

   **Debian:**

   ```bash
   sudo apt-get install libunwind8
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

## <a name="uninstall-sqlpackage-preview"></a>Desinstalación de sqlpackage (versión preliminar)

Si ha instalado sqlpackage con el instalador de Windows, desinstale de la misma manera que quita cualquier aplicación de Windows.

Si ha instalado sqlpackage con un archivo .zip u otro archivo, basta con eliminar los archivos.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

sqlpackage se ejecuta en Windows, macOS y Linux, y es compatible con las siguientes plataformas:

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

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- Mas información sobre [sqlpackage](sqlpackage.md)

[Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
