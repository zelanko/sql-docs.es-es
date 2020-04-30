---
title: Instalación de versiones anteriores de la documentación de SQL Server sin conexión
description: Obtenga información sobre cómo instalar la documentación sin conexión de SQL Server 2019, 2017, 2016, 2014 y 2012. Utilice SQL Server Management Studio (SSMS) para ver el contenido sin conexión.
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: markingmyname
ms.author: maghan
ms.date: 04/20/2020
ms.openlocfilehash: 1420e18fbf335e22d44bf78d526ab35c8b1434e5
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087875"
---
# <a name="install-previous-versions-of-sql-server-documentation-to-view-offline-in-ssms"></a>Instalación de versiones anteriores de la documentación de SQL Server para la visualización sin conexión en SSMS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo descargar y ver el contenido de SQL Server sin conexión en [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md). El contenido sin conexión le permite acceder a la documentación sin conexión a Internet (aunque se necesita una conexión a Internet para descargarla).

La documentación sin conexión está disponible para varias versiones anteriores de SQL Server. Aunque también puede [ver el contenido de las versiones anteriores en línea](https://docs.microsoft.com/previous-versions/sql/), una opción sin conexión proporciona una manera cómoda de acceder al contenido anterior.

## <a name="how-to-download-and-configure-offline-content"></a>Descarga y configuración del contenido sin conexión

Puede usar la descarga e instalación de los paquetes de Ayuda de SQL Server desde el disco local o los orígenes en línea. En las siguientes secciones se explica cómo cargar contenido sin conexión para diferentes versiones de SQL Server:

- [SQL Server 2019](#sql2019)
- [SQL Server 2017](#sql2017)
- [SQL Server 2016](#sql2016)
- [SQL Server 2014](#sql2014)
- [SQL Server 2012](#sql2012)

## <a name="sql-server-2019"></a><a id="sql2019"></a> SQL Server 2019

Siga estos pasos para cargar la documentación sin conexión de SQL Server 2019.

1. En SSMS, seleccione **Agregar y quitar contenido de la Ayuda** en el menú Ayuda.

   ![Agregar y quitar contenido del Visor de Ayuda](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   El Visor de Ayuda se abre en la pestaña Administrar contenido.

2. Para buscar el contenido de Ayuda más reciente de SQL Server 2019, en la pestaña **Administrar contenido**, elija **En línea** en el origen de la instalación y, a continuación, escriba *SQL Server 2019* en la barra de búsqueda.

   ![Búsqueda de documentación de SQL Server 2019 en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2019-search.png)

   > [!Note]
   > En Ruta de acceso del almacén local de la pestaña Administrar contenido, se muestra dónde se instala el contenido en el equipo local. Para cambiar la ubicación, seleccione **Mover**, especifique otra ruta de carpeta en el campo **A** y, después, seleccione **Aceptar**. Si se produce un error en la instalación de la Ayuda después de cambiar la ruta de acceso del almacén local, cierre y vuelva a abrir el Visor de Ayuda. Compruebe que la nueva ubicación aparece en la ruta de acceso del almacén local y vuelva a intentar realizar la instalación.

3. Para instalar el contenido de Ayuda más reciente de SQL Server 2019, seleccione **Agregar** junto a cada paquete de contenido (libro) que desee instalar y, a continuación, seleccione **Actualizar** en la parte inferior derecha.

   ![Libros de SQL Server 2019 sobre adición y actualización en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2019-add-update.png)

   > [!NOTE]
   > Si el Visor de Ayuda se bloquea al agregar contenido, cambie la línea Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" en los archivos %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings a una fecha en el futuro. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio)(El Visor de Ayuda de Visual Studio se bloquea).

4. Puede comprobar si el contenido de SQL Server 2019 está cargado; para ello, busque *sql server 2019* en el panel de contenido de la izquierda.

   ![Libros de SQL Server 2019 actualizados automáticamente](../sql-server/media/sql-server-help-installation/sql-2019-content.png)

## <a name="sql-server-2017"></a><a id="sql2017"></a> SQL Server 2017

Siga estos pasos para cargar la documentación sin conexión de SQL Server 2017.

1. En SSMS, seleccione **Agregar y quitar contenido de la Ayuda** en el menú Ayuda.

   ![Agregar y quitar contenido en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   El Visor de Ayuda se abre en la pestaña Administrar contenido.

2. Para buscar el contenido de Ayuda más reciente de SQL Server 2017, en la pestaña **Administrar contenido**, elija **En línea** en el origen de la instalación y, a continuación, escriba *SQL Server 2017* en la barra de búsqueda.

   ![Búsqueda de libros de SQL Server 2017 en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2017-search.png)

   > [!Note]
   > En Ruta de acceso del almacén local de la pestaña Administrar contenido, se muestra dónde se instala el contenido en el equipo local. Para cambiar la ubicación, seleccione **Mover**, especifique otra ruta de carpeta en el campo **A** y, después, seleccione **Aceptar**. Si se produce un error en la instalación de la Ayuda después de cambiar la ruta de acceso del almacén local, cierre y vuelva a abrir el Visor de Ayuda. Compruebe que la nueva ubicación aparece en la ruta de acceso del almacén local y vuelva a intentar realizar la instalación.

3. Para instalar el contenido de Ayuda más reciente de SQL Server 2017, seleccione **Agregar** junto a cada paquete de contenido (libro) que desee instalar y, a continuación, seleccione **Actualizar** en la parte inferior derecha.

   ![Libros de SQL Server 2017 sobre adición y actualización en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2017-add-update.png)

   > [!NOTE]
   > Si el Visor de Ayuda se bloquea al agregar contenido, cambie la línea Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" en los archivos %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings a una fecha en el futuro. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio)(El Visor de Ayuda de Visual Studio se bloquea).

4. Puede comprobar si el contenido de SQL Server 2017 está cargado; para ello, busque *sql server 2017* en el panel de contenido de la izquierda.

   ![Libros de SQL Server 2017 actualizados automáticamente](../sql-server/media/sql-server-help-installation/sql-2017-content.png)

## <a name="sql-server-2016"></a><a id="sql2016"></a> SQL Server 2016

Siga estos pasos para cargar la documentación sin conexión de SQL Server 2016.

1. En SSMS, seleccione **Agregar y quitar contenido de la Ayuda** en el menú Ayuda.

   ![Agregar y quitar contenido en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   El Visor de Ayuda se abre en la pestaña Administrar contenido.

2. Para buscar el contenido de Ayuda más reciente de SQL Server 2016, en la pestaña **Administrar contenido**, elija **En línea** en el origen de la instalación y, a continuación, escriba *SQL Server 2016* en la barra de búsqueda.

   ![Búsqueda de libros de SQL Server 2016 en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2016-search.png)

   > [!Note]
   > En Ruta de acceso del almacén local de la pestaña Administrar contenido, se muestra dónde se instala el contenido en el equipo local. Para cambiar la ubicación, seleccione **Mover**, especifique otra ruta de carpeta en el campo **A** y, después, seleccione **Aceptar**. Si se produce un error en la instalación de la Ayuda después de cambiar la ruta de acceso del almacén local, cierre y vuelva a abrir el Visor de Ayuda. Compruebe que la nueva ubicación aparece en la ruta de acceso del almacén local y vuelva a intentar realizar la instalación.

3. Para instalar el contenido de Ayuda más reciente de SQL Server 2016, seleccione **Agregar** junto a cada paquete de contenido (libro) que desee instalar y, a continuación, seleccione **Actualizar** en la parte inferior derecha.

   ![Libros de SQL Server 2016 sobre adición y actualización en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2016-add-update.png)

   > [!NOTE]
   > Si el Visor de Ayuda se bloquea al agregar contenido, cambie la línea Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" en los archivos %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings a una fecha en el futuro. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio)(El Visor de Ayuda de Visual Studio se bloquea).

4. Puede comprobar si el contenido de SQL Server 2016 está cargado; para ello, busque *sql server 2016* en el panel de contenido de la izquierda.

   ![Libros de SQL Server 2016 actualizados automáticamente](../sql-server/media/sql-server-help-installation/sql-2016-content.png)

## <a name="sql-server-2014"></a><a id="sql2014"></a> SQL Server 2014

Siga estos pasos para cargar la documentación sin conexión de SQL Server 2014.

1. Descargue el contenido de la [Documentación del producto de Microsoft SQL Server 2014 para los entornos restringidos de firewall y proxy](https://www.microsoft.com/download/details.aspx?id=42557) del centro de descarga y guárdelo en una carpeta.

2. Descomprima el archivo para ver el archivo .msha.

   ![Archivo de instalación de la documentación de Ayuda de SQL Server 2014](../sql-server/media/sql-server-help-installation/sql-2014-help-content-setup-msha.png)

3. En SSMS, seleccione **Agregar y quitar contenido de la Ayuda** en el menú Ayuda.

   ![Agregar y quitar contenido en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   El Visor de Ayuda se abre en la pestaña Administrar contenido.

4. Para instalar el último contenido de Ayuda, seleccione **Disco** en Origen de la instalación y, después, haga clic en los puntos suspensivos (...).

   ![Origen del disco de Administrar contenido en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > En Ruta de acceso del almacén local de la pestaña Administrar contenido, se muestra dónde se encuentra el contenido en el equipo local. Para cambiar la ubicación, seleccione **Mover**, especifique otra ruta de carpeta en el campo **A** y, después, seleccione **Aceptar**.
   Si se produce un error en la instalación de la Ayuda después de cambiar la ruta de acceso del almacén local, cierre y vuelva a abrir el Visor de ayuda. Compruebe que la nueva ubicación aparece en la ruta de acceso del almacén local y vuelva a intentar realizar la instalación.

5. Encuentre la carpeta donde se descomprimió el contenido. Seleccione el archivo **HelpContentSetup.msha** en la carpeta y, después, seleccione **Abrir**.

   ![Abrir el archivo Setup.msha del contenido de Ayuda de SQL Server 2014](../sql-server/media/sql-server-help-installation/sql-2014-open-msha.png)

6. Escriba *sql server 2014* en la barra de búsqueda. Una vez que vea el contenido disponible de 2014, seleccione **Agregar** junto a cada paquete de contenido (libro) que desee instalar en el Visor de Ayuda y, a continuación, seleccione **Actualizar**.

   ![Búsqueda de libros de SQL Server 2014 en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2014-search.png)

   ![Libros de SQL Server 2014 sobre adición y actualización en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2014-add-update.png)

    > [!NOTE]
    > Si el Visor de Ayuda se bloquea al agregar contenido, cambie la línea Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" en los archivos %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings a una fecha en el futuro. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio)(El Visor de Ayuda de Visual Studio se bloquea).

7. Puede comprobar si el contenido de SQL Server 2014 está instalado; para ello, busque *sql server 2014* en el panel de contenido de la izquierda.

   ![Libros de SQL Server 2014 actualizados automáticamente](../sql-server/media/sql-server-help-installation/sql-2014-content.png)

## <a name="sql-server-2012"></a><a id="sql2012"></a> SQL Server 2012

Siga estos pasos para cargar la documentación sin conexión de SQL Server 2012.

1. Descargue el contenido de la [Documentación del producto de Microsoft SQL Server 2012 para los entornos restringidos de firewall y proxy](https://www.microsoft.com/download/details.aspx?id=35750) del centro de descarga y guárdelo en una carpeta.

2. Descomprima el archivo para ver el archivo .msha.

   ![Archivo de instalación del contenido de Ayuda de SQL Server 2012](../sql-server/media/sql-server-help-installation/sql-2012-help-content-setup-msha.png)

3. En SSMS, seleccione **Agregar y quitar contenido de la Ayuda** en el menú Ayuda.

   ![Agregar y quitar contenido en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   El Visor de Ayuda se abre en la pestaña Administrar contenido.

4. Para instalar el último contenido de Ayuda, seleccione **Disco** en Origen de la instalación y, después, haga clic en los puntos suspensivos (...).

   ![Origen del disco de Administrar contenido en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > En Ruta de acceso del almacén local de la pestaña Administrar contenido, se muestra dónde se encuentra el contenido en el equipo local. Para cambiar la ubicación, seleccione **Mover**, especifique otra ruta de carpeta en el campo **A** y, después, seleccione **Aceptar**.
   Si se produce un error en la instalación de la Ayuda después de cambiar la ruta de acceso del almacén local, cierre y vuelva a abrir el Visor de ayuda. Compruebe que la nueva ubicación aparece en la ruta de acceso del almacén local y vuelva a intentar realizar la instalación.

5. Encuentre la carpeta donde se descomprimió el contenido. Seleccione el archivo **HelpContentSetup.msha** en la carpeta y, después, seleccione **Abrir**.

   ![Abrir el archivo Setup.msha del contenido de Ayuda de SQL Server 2012](../sql-server/media/sql-server-help-installation/sql-2012-open-msha.png)

6. Escriba *sql server 2012* en la barra de búsqueda. Una vez que vea el contenido disponible de 2012, seleccione **Agregar** junto a cada paquete de contenido (libro) que desee instalar en el Visor de Ayuda y, a continuación, seleccione **Actualizar**.

   ![Búsqueda de libros de SQL Server 2012 en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2012-search.png)

   ![Libros de SQL Server 2012 sobre adición y actualización en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/sql-2012-add-update.png)

    > [!NOTE]
    > Si el Visor de Ayuda se bloquea al agregar contenido, cambie la línea Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" en los archivos %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings a una fecha en el futuro. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio)(El Visor de Ayuda de Visual Studio se bloquea).

7. Puede comprobar si el contenido de SQL Server 2012 está cargado; para ello, busque *sql server 2012* en el panel de contenido de la izquierda.

   ![Documentación de SQL Server 2012 actualizada automáticamente](../sql-server/media/sql-server-help-installation/sql-2012-content.png)

## <a name="view-offline-documentation"></a>Visualización de la documentación sin conexión

Puede ver el contenido de la Ayuda de SQL Server en el menú **AYUDA** de la última versión de [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md).

### <a name="view-offline-help-content-in-ssms"></a>Visualización del contenido de la Ayuda sin conexión en SSMS

Para ver la Ayuda instalada en SSMS, seleccione **Iniciar en el Visor de Ayuda** en el menú Ayuda para iniciar el Visor de Ayuda.

   ![Iniciar en el Visor de Ayuda](../sql-server/media/sql-server-help-installation/helpviewer-view-offline.png)  

Este se abrirá en la pestaña Administrar contenido, con la tabla de contenido de la Ayuda instalada en el panel izquierdo. Seleccione los artículos de la tabla de contenido para que se muestren en el panel de la derecha.

> [!TIP]
> Si el panel de contenido no está visible, seleccione Contenido en el margen izquierdo. Seleccione el icono de marcador para mantener abierto el panel de contenido.  

   ![Visor de Ayuda con contenido](../sql-server/media/sql-server-help-installation/view-offline-all.png)

## <a name="life-cycle-policy"></a>Directiva del ciclo de vida

Revise el ciclo de vida de los productos de Microsoft para obtener información sobre la compatibilidad de un producto, un servicio o una tecnología específicos:

- [Directiva del ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle/selectindex)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el contenido archivado y el Visor de Ayuda, consulte los vínculos siguientes.

- [Un vínculo directo a las versiones anteriores de la documentación de SQL Server](https://docs.microsoft.com/previous-versions/sql/)
- [Visor de Ayuda de Microsoft (Visual Studio)](https://docs.microsoft.com/visualstudio/help-viewer/overview)
- [Documentación de SQL Server, inicio](../sql-server/index.yml?view=sql-server-2016)
- [Control del sistema de versiones de la documentación de SQL](../sql-server/versioning-system-monikers-ui-sql-server.md?view=sql-server-2016)