---
title: Descargue e instale
titleSuffix: Azure Data Studio
description: Descarga e instalar Azure datos Studio para Windows, macOS o Linux
ms.custom: seodec18
ms.date: 01/17/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09e459b61350a100a64a788e0c7746d9a2ae623e
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361625"
---
# <a name="download-and-install-azure-data-studio"></a>Descargue e instale Data Studio de Azure

  > [!div class="nextstepaction"]
  > [Comparta sus comentarios sobre la tabla de contenido dela documentación de SQL!](https://aka.ms/sqldocsurvey)

[!INCLUDE[name-sos](../includes/name-sos.md)] se ejecuta en Windows, macOS y Linux.


Descargue e instale la versión más reciente, la *versión de revisión de enero*:

Versión 1.3.9 corrige algunos problemas detectados en 1.3.8. Para obtener más información, consulte [versión de revisión de enero](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1).

> [!NOTE]
> Si va a actualizar desde SQL Operations Studio y desea conservar la configuración, métodos abreviados de teclado o fragmentos de código, consulte [mover la configuración de usuario](#move-user-settings).

|Plataforma|Descargar|Fecha de la versión| Versión |
|:---|:---|:---|:---|
|Windows|[Instalador de usuario (recomendado)](https://go.microsoft.com/fwlink/?linkid=2049972)<br>[Instalador de sistema](https://go.microsoft.com/fwlink/?linkid=2049975)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2050146)|16 de enero de 2019 |1.3.9|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2049981)|16 de enero de 2019 |1.3.9|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2050157)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2049989)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2049986)|16 de enero de 2019 |1.3.9|

Para obtener más información acerca de la versión más reciente, consulte el [notas de la versión](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Obtener Azure Data Studio para Windows

Esta versión de [!INCLUDE[name-sos](../includes/name-sos-short.md)] incluye una experiencia de instalador de Windows estándar y un archivo .zip:

**Instalador de usuario** (recomendado)

El instalador de usuario se recomienda porque no requiere privilegios de administrador, lo que simplifica las instalaciones y actualizaciones.

1. Descargue y ejecute el [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *usuario* installer para Windows](https://go.microsoft.com/fwlink/?linkid=2049972).
2. Iniciar el [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] app.

**Instalador de sistema**

1. Descargue y ejecute el [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *sistema* installer para Windows](https://go.microsoft.com/fwlink/?linkid=2049975).
2. Iniciar el [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] app.


**archivo zip**

1. Descargar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip para Windows](https://go.microsoft.com/fwlink/?linkid=2050146).
2. Busque el archivo descargado y extráigalo.
3. Ejecute `\azuredatastudio-windows\azuredatastudio.exe`:


## <a name="get-azure-data-studio-for-macos"></a>Obtener Azure Data Studio para Mac OS

1. Descargar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2049981).
2. Para expandir el contenido del archivo zip, haga doble clic en él.
3. Para realizar [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponibles en el *Launchpad*, arrastre *Studio.app de datos de Azure* a la *aplicaciones* carpeta.


## <a name="get-azure-data-studio-for-linux"></a>Obtener Azure Data Studio para Linux

1. Descargar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux mediante uno de los instaladores o el archivo tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2050157)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2049989)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2049986)
1. Para extraer el archivo e inicie [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra una nueva ventana de Terminal y escriba los siguientes comandos:

   **Instalación de Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Instalación de RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **TAR.gz instalación:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > En Debian, Red Hat y Ubuntu, puede tener dependencias que faltan. Use los siguientes comandos para instalar estas dependencias según la versión de Linux:
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```


## <a name="uninstall-azure-data-studio"></a>Desinstalar Azure Data Studio

Si instaló [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] mediante el instalador de Windows, a continuación, desinstale la misma manera que quite cualquier aplicación de Windows.

Si instaló [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] con un archivo .zip o de otro archivo, a continuación, simplemente eliminar los archivos.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

[!INCLUDE[name-sos](../includes/name-sos-short.md)] se ejecuta en Windows, macOS y Linux y es compatible con las siguientes plataformas:

### <a name="windows"></a>Windows
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Requiere Windows 7 (SP1) (64 bits) - [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="recommended-system-requirements"></a>Requisitos del sistema recomendados
Para obtener una experiencia óptima, use los requisitos del sistema recomendados.

|             | Núcleos de CPU | Memoria y RAM |
|:-----------:|:---------:|:----------:|
| Se recomienda |     4     |      8     |
|   Mínima   |     2     |      4     |
|             |           |            |

## <a name="check-for-updates"></a>Compruebe si hay actualizaciones
Para comprobar las actualizaciones más recientes, haga clic en el icono de engranaje en la parte inferior izquierda de la ventana y haga clic en **buscar actualizaciones**

## <a name="supported-sql-offerings"></a>Ofertas de SQL admitidas

* Esta versión de Azure Data Studio funciona con todas las [las versiones compatibles de SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ](https://support.microsoft.com/lifecycle?C2=1044) y proporciona compatibilidad para trabajar con las últimas características de nube de Azure SQL Database y Azure SQL Data Warehouse. Azure Data Studio también proporciona compatibilidad de versión preliminar para instancia administrada de SQL Azure.

## <a name="upgrade-from-sql-operations-studio"></a>Actualización desde SQL Operations Studio

Si aún usa SQL Operations Studio, deberá actualizar a Azure Data Studio. SQL Operations Studio era el nombre de vista previa y la versión preliminar de Azure Data Studio. En septiembre de 2018, hemos [cambió el nombre a Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) y lanzó la versión de disponibilidad General (GA). Dado que SQL Operations Studio ya no se actualiza o admite, pedimos a todos los usuarios de SQL Operations Studio para descargar la versión más reciente de Azure Data Studio para obtener las últimas características, actualizaciones de seguridad y correcciones.
 
Al actualizar desde la versión preliminar anterior de Azure Data Studio más reciente, perderá la configuración actual y las extensiones. Para mover la configuración, siga las instrucciones que aparecen en la siguiente *mover la configuración de usuario* sección:


## <a name="move-user-settings"></a>Mover la configuración de usuario

Si desea mover la configuración personalizada, métodos abreviados de teclado o fragmentos de código, siguen estos pasos. Esto es importante si va a actualizar desde la versión de SQL Operations Studio a Azure Data Studio.

*Si ya tiene Azure Data Studio, o nunca se haya instalado o personalizar SQL Operations Studio, a continuación, puede omitir esta sección.*


1. Abra configuración haciendo clic en el icono de engranaje en la parte inferior izquierda y **configuración.**

   ![Abrir configuración](./media/download/open-settings.png)

2. Haga clic en el **configuración de usuario** pestaña en la parte superior y haga clic en **mostrar en el explorador**

   ![mostrar en el explorador](./media/download/reveal-in-explorer.png)

3. Copie todos los archivos en esta carpeta y guárdelo en una forma sencilla de buscar la ubicación en la unidad local, como la carpeta documentos.

   ![configuración de copia](./media/download/copy-settings.png)

4. En la nueva versión de Azure Data Studio, siga los pasos 1-2 para el paso 3, a continuación, pegue el contenido que ha guardado en la carpeta. Puede copiar manualmente a través de la configuración, los enlaces de teclado o fragmentos de código en sus respectivas ubicaciones.

5. Si se reemplaza una instalación existente, elimine el directorio de instalación anterior antes de la instalación para evitar errores al conectarse a su cuenta de Azure para el Explorador de recursos.

## <a name="next-steps"></a>Pasos siguientes

Consulte uno de los siguientes tutoriales para empezar a trabajar:
- [Conectar y consultar SQL Server](quickstart-sql-server.md)
- [Conectar y consultar la base de datos SQL Azure](quickstart-sql-database.md)
- [Conectar y consultar el almacén de datos de Azure](quickstart-sql-dw.md)

Contribuir a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio) 

[Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) y [recopilación de datos de uso](usage-data-collection.md).
