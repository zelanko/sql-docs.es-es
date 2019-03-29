---
title: Descargue e instale sqlpackage | Microsoft Docs
description: Descargue e instale sqlpackage para Windows, macOS o Linux
ms.custom: tools|sos
ms.date: 06/19/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 5a45803f4ce2a91962a5bba824a468ca436f7839
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527217"
---
# <a name="download-and-install-sqlpackage"></a>Descargue e instale sqlpackage

Sqlpackage se ejecuta en Windows, macOS y Linux.

Descargue e instale la versión más reciente de .NET Framework y macOS y Linux las versiones preliminares:

|Plataforma|Descargar|Fecha de la versión|Versión|Compilar
|:---|:---|:---|:---|:---|
|Windows|[Instalador MSI](https://go.microsoft.com/fwlink/?linkid=2069405)|1 de febrero de 2019|18.1|15.0.4316.1|
|macOS (versión preliminar) de .NET Core|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2069126)|1 de febrero de 2019 | 18.1 |15.0.4316.1|
|.NET Core (versión preliminar) de Linux|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2069122)|1 de febrero de 2019 | 18.1 |15.0.4316.1|

Para obtener más información acerca de la versión más reciente, consulte el [notas de la versión](release-notes-sqlpackage.md).

## <a name="get-sqlpackage-for-windows"></a>Obtener sqlpackage para Windows

Esta versión de sqlpackage incluye una experiencia de instalador de Windows estándar y un archivo .zip: 

1. Descargue y ejecute el [DacFramework.msi installer para Windows](https://go.microsoft.com/fwlink/?linkid=2069405).
2. Abra una nueva ventana de símbolo del sistema y ejecute sqlpackage.exe
    - Sqlpackage se instala en el ```C:\Program Files\Microsoft SQL Server\150\DAC\bin``` carpeta
    - Instalar el x86 versión en un x64 máquina, sqlpackage se instala en el ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin``` carpeta

## <a name="get-sqlpackage-preview-for-macos"></a>Obtener sqlpackage (versión preliminar) para macOS

1. Descargar [sqlpackage para macOS](https://go.microsoft.com/fwlink/?linkid=2069126).
2. Para extraer el archivo e inicia sqlpackage, abra una nueva ventana de Terminal y escriba los siguientes comandos:

   **Instalación del archivo .zip:**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-preview-for-linux"></a>Obtener sqlpackage (versión preliminar) para Linux

1. Descargar [sqlpackage para Linux](https://go.microsoft.com/fwlink/?linkid=2069122) mediante uno de los instaladores o el archivo tar.gz:
2. Para extraer el archivo e inicia sqlpackage, abra una nueva ventana de Terminal y escriba los siguientes comandos:

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
   > En Debian, Red Hat y Ubuntu, puede tener dependencias que faltan. Use los siguientes comandos para instalar estas dependencias según la versión de Linux:

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
