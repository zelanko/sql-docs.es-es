---
title: Descarga e instalación de Azure Data Studio
description: Descargue e instale Azure Data Studio para Windows, macOS o Linux. En este artículo se proporcionan fechas de lanzamiento, números de versión, requisitos del sistema y vínculos de descarga.
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: seodec18
ms.date: 8/12/2020
ms.openlocfilehash: 29f5f31d999e96a17cd1653323c75251c8873572
ms.sourcegitcommit: e4c36570c34cd7d7ae258061351bce6e54ea49f6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88147216"
---
# <a name="download-and-install-azure-data-studio"></a>Descarga e instalación de Azure Data Studio

Azure Data Studio se ejecuta en Windows, macOS y Linux.

Descargue e instale la versión más reciente:

> [!NOTE]
> Si actualiza desde SQL Operations Studio y quiere mantener la configuración, los métodos abreviados de teclado o los fragmentos de código, vea [Migrar la configuración del usuario](#move-user-settings).

|Plataforma|Descargar|Fecha de la versión| Versión |
|:---|:---|:---|:---|
| Windows | [Instalador de usuario (recomendado)](https://go.microsoft.com/fwlink/?linkid=2138608)<br>[Instalador del sistema](https://go.microsoft.com/fwlink/?linkid=2138704)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2138705) | 12 de agosto de 2020 | 1.21.0 |
| macOS | [.zip](https://go.microsoft.com/fwlink/?linkid=2138609) | 12 de agosto de 2020 | 1.21.0 |
| Linux | [.deb](https://go.microsoft.com/fwlink/?linkid=2138508)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2138507)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2138706) | 12 de agosto de 2020| 1.21.0 |

Para más información sobre la última versión, consulte las [notas de la versión](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Descargar Azure Data Studio para Windows

En esta versión de Azure Data Studio, se incluye una experiencia de Windows Installer estándar y un archivo .zip.

Le recomendamos que use el *instalador de usuario*, ya que no se necesitan privilegios de administrador, lo que simplifica tanto el proceso de instalación como las actualizaciones. El instalador de usuario no necesita privilegios de administrador porque la ubicación se encuentra en la carpeta AppData local del usuario (LOCALAPPDATA). Además, el instalador de usuario también proporciona una experiencia de actualización en segundo plano más fluida. Para obtener más información, vea [Configuración del usuario para Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Instalador de usuario** (recomendado)

1. Descargue y ejecute el instalador de *usuario* de [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2138608).
2. Inicie la aplicación [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Instalador del sistema**

1. Descargue y ejecute el instalador del *sistema* de [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2138704).
2. Inicie la aplicación [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**archivo zip**

1. Descargue el archivo .zip de [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2138705).
2. Busque el archivo descargado y extraiga su contenido.
3. Ejecute `\azuredatastudio-windows\azuredatastudio.exe`:

## <a name="get-azure-data-studio-for-macos"></a>Descargar Azure Data Studio para macOS

1. Descargue [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2138609).
2. Para extraer el contenido del archivo zip, haga doble clic en este.
3. Para que Azure Data Studio esté disponible en *Launchpad*, arrastre *Azure Data Studio.app* hasta la carpeta *Aplicaciones*.

## <a name="get-azure-data-studio-for-linux"></a>Descargar Azure Data Studio para Linux

1. Descargue [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux con uno de los instaladores, o bien descargue el archivo tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2138508)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2138507)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2138706)
1. Para extraer el archivo e iniciar [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra una ventana de terminal y escriba los comandos siguientes:

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

   **Instalación de tar.gz:**

   ```bash
   cd ~
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc
   azuredatastudio
   ```

   > [!NOTE]
   > En Debian, Red Hat y Ubuntu, puede haber dependencias que faltan. Use los siguientes comandos para instalar estas dependencias según la versión de Linux:

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

## <a name="download-insiders-build-of-azure-data-studio"></a>Descargar la compilación para los participantes del programa Insider de Azure Data Studio

En general, los usuarios tienen que descargar la versión estable de Azure Data Studio anterior. Pero, si quiere probar las características de la versión beta y enviarnos sus comentarios, puede descargar una [compilación para participantes del programa Insider de Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main).

## <a name="uninstall-azure-data-studio"></a>Desinstalar Azure Data Studio

Si ha instalado [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] con Windows Installer, use el mismo método que para desinstalar cualquier aplicación de Windows.

Si ha instalado [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] con un archivo .zip o de otro tipo, simplemente elimine los archivos.

## <a name="supported-operating-systems"></a>Sistemas operativos compatibles

Azure Data Studio se ejecuta en Windows, macOS y Linux, y es compatible con las plataformas siguientes:

### <a name="windows"></a>Windows

- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Windows 7 (SP1) 64 bits: se necesita [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

### <a name="macos"></a>macOS

- macOS 10.15 Catalina
- macOS 10.14 Mojave
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="recommended-system-requirements"></a>Requisitos del sistema recomendados

| Recomendados/mínimos | Núcleos de CPU | Memoria/RAM |
|---------------------|-----------|------------|
| Recomendado         |     4     |   8 GB     |
|   Mínima           |     2     |   4 GB     |

## <a name="check-for-updates"></a>Buscar actualizaciones

Para buscar las actualizaciones más recientes, haga clic en el icono de engranaje de la parte inferior izquierda de la ventana y seleccione **Buscar actualizaciones**.

En un entorno sin conexión, las actualizaciones se pueden aplicar mediante la [instalación de la versión más reciente](#download-and-install-azure-data-studio) directamente sobre una versión instalada previamente.  No es necesario desinstalar versiones anteriores de Azure Data Studio, ya que el instalador actualiza una aplicación instalada actualmente, si existe.

## <a name="supported-sql-offerings"></a>Ofertas de SQL admitidas

- La versión de Azure Data Studio funciona con todas las [versiones admitidas de SQL Server 2014[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) y, además, proporciona la compatibilidad para trabajar con las características de nube más recientes en Azure SQL Database y Azure SQL Data Warehouse. Azure Data Studio también proporciona compatibilidad de vista previa con instancias administradas de Azure SQL.

## <a name="upgrade-from-sql-operations-studio"></a>Actualizar desde SQL Operations Studio

Si aún usa SQL Operations Studio, necesita actualizar Azure Data Studio. SQL Operations Studio era el nombre de la versión preliminar de Azure Data Studio. En septiembre de 2018, [cambiamos el nombre a Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) y publicamos la versión de disponibilidad general. Como SQL Operations Studio ya no se actualiza ni se admite, pedimos a todos los usuarios de SQL Operations Studio que descarguen la versión más reciente de Azure Data Studio para obtener las características, actualizaciones de seguridad y secciones más recientes.

Al actualizar desde la versión preliminar anterior a la versión más reciente de Azure Data Studio, perderá las extensiones y la configuración actuales. Para migrar la configuración, siga las instrucciones en la siguiente sección, *Migrar la configuración del usuario*:

## <a name="move-user-settings"></a>Migrar la configuración del usuario

Para migrar configuraciones personalizadas, métodos abreviados de teclado o fragmentos de código, siga este procedimiento. Esto es importante si va a actualizar desde la versión de SQL Operations Studio a Azure Data Studio.

*Si ya tiene Azure Data Studio o nunca ha instalado ni personalizado SQL Operations Studio, puede omitir esta sección.*

1. Para abrir la configuración, haga clic en el icono de engranaje de la parte inferior izquierda y seleccione **Configuración**.

   ![abrir configuración](./media/download/open-settings.png)

2. Haga clic con el botón derecho en la pestaña **Configuración de usuario** de la parte superior y seleccione **Mostrar en el Explorador**.

   ![mostrar en el Explorador](./media/download/reveal-in-explorer.png)

3. Copie todos los archivos de esta carpeta y guárdelos en una ubicación a la que pueda acceder fácilmente desde la unidad local (por ejemplo, la carpeta Documentos).

   ![copiar configuración](./media/download/copy-settings.png)

4. En la nueva versión de Azure Data Studio, siga los pasos 1-2 y, después, para el paso 3, pegue el contenido que haya guardado en la carpeta. También puede copiar de forma manual la configuración, los enlaces de teclado o los fragmentos de código en las ubicaciones correspondientes.

5. Si reemplaza una instalación existente, elimine el directorio de instalación anterior antes de la instalación para evitar errores relacionados con su cuenta de Azure en el explorador de recursos.

## <a name="next-steps"></a>Pasos siguientes

Para empezar, vea una de las siguientes guías de inicio rápido:

- [Conectar y consultar SQL Server](quickstart-sql-server.md)
- [Conectar y consultar Azure SQL Database](quickstart-sql-database.md)
- [Conectar y consultar almacenamiento de datos de Azure](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Declaración de privacidad de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) y [recopilación de datos de uso](usage-data-collection.md).
