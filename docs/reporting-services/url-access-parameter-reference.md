---
title: Referencia de parámetros de acceso URL | Microsoft Docs
description: Use los parámetros de este artículo como parte de una dirección URL para configurar la apariencia de los informes de Reporting Services.
ms.date: 05/22/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5c975f457238912c16e33a13f1f2ba598c82cac3
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/26/2020
ms.locfileid: "83859039"
---
# <a name="url-access-parameter-reference"></a>Referencia de parámetros de acceso URL

  Puede usar los parámetros siguientes como parte de una dirección URL para configurar la apariencia de los informes de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Los parámetros más comunes se muestran en esta sección. Los parámetros distinguen entre mayúsculas y minúsculas y empiezan con el prefijo de parámetro *rs:* si se dirige al servidor de informes y *rc:* si se dirige a un Visor HTML. También puede especificar parámetros que son específicos de dispositivos o extensiones de representación. Para más información sobre parámetros específicos del dispositivo, vea [Especificación de la configuración de la información del dispositivo en una dirección URL](../reporting-services/specify-device-information-settings-in-a-url.md).
  
> [!IMPORTANT]  
>  En un servidor de informes en modo SharePoint, es importante que la dirección URL incluya la sintaxis de proxy de `_vti_bin` para enrutar la solicitud a través de SharePoint y el proxy HTTP de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. El proxy aporta el contexto que la solicitud HTTP necesita para garantizar la ejecución correcta del informe de los servidores de informes en modo SharePoint. Para obtener ejemplos, vea [Acceso a elementos del servidor de informes mediante el acceso URL](../reporting-services/access-report-server-items-using-url-access.md).
> 
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.
  

##  <a name="html-viewer-commands-rc"></a><a name="bkmk_htmlviewer"></a> Comandos del Visor HTML (rc:)
 - Los comandos del Visor HTML Se usan para establecer como destino el Visor HTML y tienen el prefijo *rc:* :
  
-   **Toolbar**: Muestra u oculta la barra de herramientas. Si el valor de este parámetro es **false**, se omiten todas las opciones restantes. Si omite este parámetro, la barra de herramientas se muestra automáticamente para los formatos de representación que lo admiten. El valor predeterminado de este parámetro es **true**.
  
    > [!IMPORTANT]  
    >  *rc:Toolbar*=**false** no funciona para las cadenas de acceso URL que usan una dirección IP, en lugar de un nombre de dominio, cuyo destino es un informe hospedado en un sitio de SharePoint.
  
-   **Parámetros**: Muestra u oculta el área de parámetros de la barra de herramientas. Si establece este parámetro en el valor **true**, se muestra el área de parámetros de la barra de herramientas. Si establece este parámetro en **false**, el área de parámetros no se muestra y no puede ser mostrada por el usuario. Si establece este parámetro en un valor de **Collapsed**, no se mostrará el área de parámetros, pero el usuario puede alternarla. El valor predeterminado de este parámetro es **true**.  
  
     Por ejemplo, en modo nativo:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Parameters=Collapsed  
    ```  
  
     Por ejemplo, en modo de SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Parameters=Collapsed  
    ```  
  
-   **Zoom**: Establece el valor de ampliación del informe como porcentaje entero o una constante de cadena. Los valores de cadena estándar incluyen **Page Width** y **Whole Page**. Las versiones de Internet Explorer anteriores a Internet Explorer 5.0 y todos los exploradores que no son de[!INCLUDE[msCoName](../includes/msconame-md.md)] omiten este parámetro. El valor predeterminado de este parámetro es **100**.
  
     Por ejemplo, en modo nativo:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Zoom=Page Width  
    ```  
  
     Por ejemplo, en modo de SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Zoom=Page Width  
    ```  
  
-   **Section**: Establece la página del informe que se mostrará. Cualquier valor que sea mayor que el número de páginas del informe muestra la última página. Cualquier valor que sea menor que **0** muestra la página 1 del informe. El valor predeterminado de este parámetro es **1**.
  
     Para obtener un ejemplo en modo nativo, para mostrar la página 2 del informe:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Section=2  
    ```  
  
     Para obtener un ejemplo en modo de SharePoint, para mostrar la página 2 del informe:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Section=2  
    ```  
  
-   **FindString**: busca un conjunto de texto específico en un informe y resalta el texto.
    
    > [!IMPORTANT]  
    >  *rc:FindString* no funciona a menos que incluya *rc:Toolbar*=**false** en la cadena de acceso URL.
  
     Por ejemplo, en modo nativo:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Toolbar=false&rc:FindString=Mountain-400  
    ```  
  
     Por ejemplo, en modo de SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Toolbar=false&rc:FindString=Mountain-400  
    ```  
  
-   **StartFind**: Especifica la última sección en que se buscará. El valor predeterminado de este parámetro es la última página del informe.  
  
     Para obtener un ejemplo en modo nativo que busca la primera repetición del texto "Mountain-400" en el informe de ejemplo Product Catalog desde la página 1 hasta la página 5:
  
    ```  
    https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
    ```  
  
-   **EndFind**: Establece el número de la última página que se utilizará en la búsqueda. Por ejemplo, un valor de **5** indica que la última página que se va a buscar es la página 5 del informe. El valor predeterminado es el número de la página actual. Utilice este parámetro junto con el parámetro *StartFind* . Vea el ejemplo anterior.
  
-   **FallbackPage**: Establece el número de la página que se mostrará si se produce un error en una búsqueda o en una selección de mapa del documento. El valor predeterminado es el número de la página actual.
  
-   **GetImage**: Obtiene un icono determinado para la interfaz de usuario del Visor HTML.
  
-   **Icon**: Obtiene el icono de una extensión de representación determinada.
  
-   **Stylesheet**: Especifica una hoja de estilos que se va a aplicar al Visor HTML.
  
-   **Device Information Setting**: especifica una configuración de información del dispositivo en forma de `rc:tag=value`, donde *tag* es el nombre de la configuración de información de un dispositivo concreto para la extensión de representación que se usa actualmente. (Vea la descripción del parámetro *Format*). Por ejemplo, puede usar la configuración de información del dispositivo *OutputFormat* para que la extensión de representación IMAGE represente el informe en una imagen JPEG con los siguientes parámetros en la cadena de acceso URL: `...&rs:Format=IMAGE&rc:OutputFormat=JPEG`. Para obtener más información sobre toda la configuración de información del dispositivo específica de la extensión, vea [Configuración de información del dispositivo para las extensiones de representación &#40;Reporting Services&#41;](../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md).
  
##  <a name="report-server-commands-rs"></a><a name="bkmk_reportserver"></a> Comandos del servidor de informes (rs:)
 Los comandos de servidor de informes tienen el prefijo *rs:* y se usan para establecer el servidor de informes como destino:
  
-   **Comando**: Realiza una acción en un elemento de catálogo, según el tipo de elemento. El valor predeterminado se determina mediante el tipo de elemento de catálogo al que se hace referencia en la cadena de acceso URL. Los valores válidos son:
  
    -   **ListChildren** y **GetChildren**: muestra el contenido de una carpeta. Los elementos de carpeta se muestran dentro de una página genérica de navegación por elementos.
  
         Por ejemplo, en modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales&rs:Command=GetChildren  
        ```  
  
         Por ejemplo, una instancia con nombre en modo nativo:
  
        ```  
        https://myssrshost/Reportserver_THESQLINSTANCE?/reportfolder&rs:Command=listChildren  
        ```  
  
         Por ejemplo, en modo de SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rs:Command=GetChildren  
        ```  
  
    -   **Render**: el informe se representa en el explorador para que pueda verlo.
  
         Por ejemplo, en modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
         Por ejemplo, en modo de SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
    -   **GetSharedDatasetDefinition**: muestra la definición XML asociada a un conjunto de datos compartido. Las propiedades del conjunto de datos compartido, incluidos la consulta, los parámetros del conjunto de datos, los valores predeterminados, los filtros del conjunto de datos y opciones de datos como la intercalación y la distinción entre mayúsculas y minúsculas, se guardan en la definición. Para usar este valor, debe tener el permiso para **leer definición de informe** en un conjunto de datos compartido.
  
         Por ejemplo, en modo nativo:
  
        ```  
        https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
        ```  
  
    -   **GetDataSourceContents**: muestra las propiedades de un origen de datos compartido determinado como XML. Si el explorador admite código XML y es un usuario autenticado con el permiso **Leer contenido** en el origen de datos, se muestra la definición del origen de datos.
  
         Por ejemplo, en modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
         Por ejemplo, en modo de SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
    -   **GetResourceContents**: representa un recurso y lo muestra en una página HTML si el recurso es compatible con el explorador. De lo contrario, se le preguntará si quiere abrir o guardar el archivo o recurso en el disco.  
  
         Por ejemplo, en modo nativo:
  
        ```  
        https://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents  
        ```  
  
         Por ejemplo, en modo de SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents  
        ```  
  
    -   **GetComponentDefinition**: muestra la definición XML asociada a un elemento de informe publicado. Para usar este valor, debe tener el permiso **Leer contenido** en un elemento de informe publicado.
  
-   **Format**: Especifica el formato en el que se representará y verá un informe. Los valores habituales son:
  
    -   **HTML5**  
  
    -   **PPTX**  
  
    -   **ATOM**  
  
    -   **HTML4.0**  
  
    -   **MHTML**  
  
    -   **IMAGE**  
  
    -   **EXCEL** (para .xls)
    
    -   **EXCELOPENXML** (para .xlsx)
  
    -   **WORD** (para .doc)
    
    -   **WORDOPENXML** (para .docx)
  
    -   **CSV**  
  
    -   **PDF**  
  
    -   **XML**  
  
     El valor predeterminado es **HTML5**. Para obtener más información, vea [Exportación de un informe con el acceso URL](../reporting-services/export-a-report-using-url-access.md).
  
     Para obtener una lista completa, vea la sección de la extensión **\<Render>** del archivo rsreportserver.config del servidor de informes. Para obtener más información sobre dónde encontrar este archivo, vea [Archivo de configuración RsReportServer.config](../reporting-services/report-server/rsreportserver-config-configuration-file.md).
  
     Por ejemplo, para obtener una copia PDF de un informe directamente desde un servidor de informes en modo nativo:
  
    ```  
    https://myrshost/ReportServer?/myreport&rs:Format=PDF  
    ```  
  
     Por ejemplo, para obtener una copia en PDF de un informe directamente desde un servidor de informes en modo SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
    ```  
  
-   **ParameterLanguage**: proporciona un idioma para los parámetros pasados en una dirección URL que es independiente del idioma del explorador. El valor predeterminado es el idioma del explorador. El valor puede ser un valor de referencia cultural, como **en-us** o **de-de.**
  
     Por ejemplo, en modo nativo, para invalidar el idioma del explorador y especificar un valor de referencia cultural de-DE:
  
    ```  
    https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
    ```  
  
-   **Instantánea**: Representa un informe basándose en una instantánea del historial de informes. Para obtener más información, vea [Representación de instantáneas del historial de informes mediante acceso URL](../reporting-services/render-a-report-history-snapshot-using-url-access.md).
  
     Por ejemplo, en modo nativo, para recuperar una instantánea del historial de informes con fecha 2003-04-07 con una marca de tiempo de 13:40:02:
  
    ```  
    https://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
    ```  
  
-   **PersistStreams**: Representa un informe en un flujo almacenado único. El procesador de imagen utiliza este parámetro para transmitir el informe representado fragmento por fragmento. Después de utilizar este parámetro en una cadena de acceso de dirección URL, utilice la misma cadena de acceso de dirección URL con el parámetro *GetNextStream* en lugar del parámetro *PersistStreams* para obtener el fragmento siguiente en el flujo almacenado. Este comando de dirección URL devuelve en última instancia un flujo de cero bytes para indicar el fin del flujo almacenado. El valor predeterminado es **false**.
  
-   **GetNextStream**: obtiene el siguiente grupo de datos en una transmisión persistente a la que se accede con el parámetro *PersistStreams*. Para obtener más información, vea la descripción de *PersistStreams*. El valor predeterminado es **false**.
  
-   **SessionID**: Especifica una sesión de informe activa establecida entre la aplicación cliente y el servidor de informes. El valor de este parámetro se establece en el identificador de la sesión.
  
     Puede especificar el identificador de sesión como una cookie o como parte de la dirección URL. Cuando el servidor de informes se ha configurado para no usar las cookies de sesión, la primera solicitud sin un identificador de sesión especificado resulta en una redirección con un identificador de sesión. Para obtener más información sobre las sesiones del servidor de informes, vea [Identificación del estado de ejecución](../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).
  
-   **ClearSession**: Un valor de **true** indica al servidor de informes que quite un informe de la sesión de informe. Todas las instancias del informe asociadas a un usuario autenticado se quitan de la sesión de informe. (Una instancia del informe se define como el mismo informe ejecutado varias veces con diferentes valores de parámetro de informe). El valor predeterminado es **false**.
  
-   **ResetSession**: un valor de **true** indica al servidor de informes que restablezca la sesión del informe y que quite la asociación de la sesión del informe con todas las instantáneas de informe. El valor predeterminado es **false**.
  
-   **ShowHideToggle**: Alterna el estado de mostrar u ocultar de una sección del informe. Especifique un entero positivo para representar la sección que desea alternar.
  
##  <a name="report-viewer-web-part-commands-rv"></a><a name="bkmk_webpart"></a> Comandos de elemento web del Visor de informes (rv:)
 Los siguientes nombres de parámetros de informes reservados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se usan para tener como destino el elemento web del Visor de informes integrado en SharePoint. Estos nombres de parámetro tienen como prefijo *rv:* . El elemento web del Visor de informes también acepta el parámetro *rs:ParameterLanguage*.
  
-   **Toolbar**: controla la presentación de la barra de herramientas para el elemento web del Visor de informes. El valor predeterminado es **Full**. Los valores pueden ser:
  
    -   **Full**: muestra la barra de herramientas completa.
  
    -   **Navegación**: solo muestra la paginación en la barra de herramientas.
  
    -   **Ninguna**: no muestra la barra de herramientas.
  
     Por ejemplo, en modo de SharePoint, para mostrar solamente la paginación en la barra de herramientas:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation  
    ```  
  
-   **HeaderArea**: controla la presentación del encabezado para el elemento web del Visor de informes. El valor predeterminado es **Full**. Los valores pueden ser:
  
    -   **Full**: muestra el encabezado completo.
  
    -   **BreadCrumbsOnly**: muestra solo la navegación detallada en el encabezado para informar al usuario de dónde se encuentra en la aplicación.
  
    -   **Ninguna**: no muestra el encabezado.
  
     Por ejemplo, en modo de SharePoint, para mostrar solamente la navegación detallada en el encabezado:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly  
    ```  
  
-   **DocMapAreaWidth**: controla el ancho de la presentación, en píxeles, del área de parámetros en el elemento web del Visor de informes. El valor predeterminado es igual que el valor predeterminado del elemento web del Visor de informes. Debe ser un número entero no negativo.
  
-   **AsyncRender**: Controla si se representa un informe de forma asincrónica. El valor predeterminado es **true**, que especifica que un informe se representa de forma asincrónica. El valor debe ser un valor booleano de **true** o **false**.
  
-   **ParamMode**: controla cómo se muestra el área de mensajes de parámetros del elemento web del Visor de informes en la vista de página completa. El valor predeterminado es **Full**. Los valores válidos son:
  
    -   **Full**: muestra el área de mensajes de parámetros.
  
    -   **Collapsed**: contrae el área de mensajes de parámetros.
  
    -   **Hidden**: oculta el área de mensajes de parámetros.
  
     Por ejemplo, en modo de SharePoint, para ocultar el área de mensajes de parámetros:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed  
    ```  
  
-   **DocMapMode**: controla cómo se muestra el área de mapa de documento del elemento web del Visor de informes en la vista de página completa. El valor predeterminado es **Full**. Los valores válidos son:
  
    -   **Full**: muestra el área de mapa del documento.
  
    -   **Collapsed**: contrae el área de mapa del documento.
  
    -   **Hidden**: oculta el área de mapa del documento.
  
-   **DockToolBar**: controla si la barra de herramientas del elemento web del Visor de informes está acoplada a la parte superior o inferior. Los valores válidos son **Top** y **Bottom**. El valor predeterminado es **Top**.
  
     Por ejemplo, en modo de SharePoint, para acoplar la barra de herramientas a la parte inferior:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom  
    ```  
  
-   **ToolBarItemsDisplayMode**: Controla qué elementos de la barra de herramientas se muestran. Es un valor de enumeración bit a bit. Para incluir un elemento de la barra de herramientas, agregue el valor del elemento al valor total. Por ejemplo, para que no se muestre un menú **Acciones**, use *rv:ToolBarItemsDisplayMode=63* (o 0x3F), que es 1+2+4+8+16+32. Solo para los elementos del menú **Acciones**, use *rv:ToolBarItemsDisplayMode=960* (o 0x3C0). El valor predeterminado es **-1**, que incluye todos los elementos de la barra de herramientas. Los valores válidos son:
  
    -   **1 (0x1)** : el botón **Atrás**  
  
    -   **2 (0x2)** : los controles de búsqueda de texto  
  
    -   **4 (0x4)** : los controles de navegación de páginas  
  
    -   **8 (0x8)** : el botón **Actualizar**  
  
    -   **16 (0x10)** : el cuadro de lista **Zoom**  
  
    -   **32 (0x20)** : el botón **Atom Feed**  
  
    -   **64 (0x40)** : la opción de menú **Imprimir** del menú **Acciones**  
  
    -   **128 (0x80)** : el submenú **Exportar** del menú **Acciones**  
  
    -   **256 (0x100)** : la opción de menú **Abrir con el Generador de informes** del menú **Acciones**  
  
    -   **512 (0x200)** : la opción de menú **Suscribir** del menú **Acciones**  
  
    -   **1024 (0x400)** : la opción de menú **Nueva alerta de datos** de **Acciones**  
  
     Por ejemplo, en modo de SharePoint, para mostrar solamente el botón **Atrás**, los controles de búsqueda de texto y de navegación de páginas y el botón **Actualizar**:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15  
    ```  
  
## <a name="see-also"></a>Consulte también
 - [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)
 - [Exportación de un informe con el acceso URL](../reporting-services/export-a-report-using-url-access.md)
  
  
