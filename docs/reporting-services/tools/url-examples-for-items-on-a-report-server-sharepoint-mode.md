---
title: Ejemplos de direcciones URL para los elementos de un servidor de informes - Modo de SharePoint | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.assetid: 54cb861a-8cec-445c-875d-599fb9bd1973
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7b787bdccdb913bd95051c8e3a4a3dd37fed5c01
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812963"
---
# <a name="url-examples-for-items-on-a-report-server---sharepoint-mode"></a>Ejemplos de direcciones URL para los elementos de un servidor de informes - Modo de SharePoint
  Para publicar informes y elementos relacionados en una biblioteca de SharePoint, puede publicar el contenido con las herramientas de creación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , como, por ejemplo, el Diseñador de informes o puede cargar el contenido mediante acciones del sitio de SharePoint.  
  
 Los sitios de SharePoint usan direcciones web distintas de las del servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo. La jerarquía web de un sitio de SharePoint incluye la aplicación web de SharePoint, un sitio de nivel superior, subsitios opcionales y bibliotecas. Debe saber cómo crear una dirección URL que especifique el servidor de SharePoint y la ubicación en la jerarquía de sitios de SharePoint en la que desea publicar un informe o los elementos relacionados.  
  
 Los elementos relacionados con un informe incluyen los orígenes de datos compartidos, los subinformes, los informes detallados y recursos como archivos de imagen basados en web. Un informe publicado en una biblioteca de SharePoint debe especificar estos elementos relacionados por su ubicación en la biblioteca de SharePoint.  
  
 Use los ejemplos de este tema como ayudar para crear las direcciones URL de los informes y elementos relacionados en sus soluciones de informes.  
  
## <a name="site-hierarchy"></a>Jerarquía de sitios  
 Al configurar un servidor de informes para que se ejecute en el modo integrado de SharePoint, se usa la jerarquía web de SharePoint para obtener acceso a los elementos que se procesan y administran en un servidor de informes.  
  
 Pueden utilizarse los siguientes elementos de la jerarquía web para obtener acceso y proteger el contenido del servidor de informes. No se usan otros objetos, como listas y páginas, para obtener acceso al contenido del servidor de informes y, por lo tanto, no se describen en la siguiente tabla.  
  
|Objeto|Descripción|  
|------------|-----------------|  
|Aplicación web de SharePoint|Una aplicación web de SharePoint puede instalarse como un servidor independiente o en un grupo de servidores que contenga una colección de servidores virtuales. Una aplicación web tiene una dirección URL (por ejemplo, `http:*//servername*`) y puede contener varios sitios.|  
|Sitio|Un sitio es un sitio primario para una aplicación web o un subsitio.|  
|Biblioteca de SharePoint|Una biblioteca contiene documentos o carpetas. Una biblioteca o una carpeta de una biblioteca es el único objeto del sitio que puede almacenar informes, modelos de informe, orígenes de datos compartidos e imágenes externas.|  
|Elemento|Entre los elementos del servidor de informes a los que se puede hacer referencia en una dirección URL, figuran una definición de informe para un informe o subinforme, un modelo de informe, un origen de datos compartido o una imagen externa.|  
  
## <a name="url-syntax-and-rules"></a>Sintaxis y reglas de las direcciones URL  
 Cada uno de los elementos del servidor de informes incluido en una biblioteca se identifica mediante una dirección URL completa que incluye un prefijo de protocolo, un nombre de servidor, un sitio, una biblioteca, un nombre de archivo y una extensión de nombre de archivo para el tipo de archivo.  
  
### <a name="url-for-a-sharepoint-server"></a>Dirección URL para un servidor de SharePoint  
 Debe usar una dirección URL para el servidor de SharePoint al implementar un servidor de informes o un proyecto de modelos de informe desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en el servidor de informes.  
  
 Para buscar el nombre del servidor que se va usar, abra un explorador y busque la biblioteca de SharePoint en que desea publicar el informe. El nombre del servidor aparece justo después del prefijo de protocolo (por ejemplo, `http:*//servername*`).  
  
 No se admite el uso del extremo proxy de dirección URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Un punto de conexión proxy incluye un número de puerto (por ejemplo, `http:*//servername:8080/reportserver*`).  
  
### <a name="url-for-a-sharepoint-server-site-or-subsite"></a>Dirección URL para un sitio o subsitio del servidor de SharePoint  
 Al implementar un informe o un origen de datos de informe, debe usar una dirección URL para el sitio y el subsitio de SharePoint, si lo hay. En la dirección URL, el nombre del sitio aparece justo después del nombre de servidor (por ejemplo, `https://*servername/site*` o `https://*servername/site/subsite*`).  
  
 En una aplicación web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] , el sitio y el subsitio suelen corresponderse con las pestañas del sitio principal. Para buscar el nombre del sitio o el subsitio, haga clic en **Inicio**y, a continuación, en **Todo el contenido del sitio**. Desplácese hasta la parte inferior y busque **Áreas de trabajo y sitios**. Aparece la lista de sitios en esta sección.  
  
### <a name="url-for-a-sharepoint-library"></a>Dirección URL para una biblioteca de SharePoint  
 Al implementar un informe o un elemento relacionado en una biblioteca de SharePoint, debe usar una dirección URL para la biblioteca de SharePoint. La dirección URL que se usa para la biblioteca varía según la versión de SharePoint usada.  
  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 o [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], la biblioteca aparece después del nombre del servidor (por ejemplo, `https://*servername/*Shared Documents`).  
  
 En [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)], la biblioteca aparece después del sitio y el subsitio. Por ejemplo, `https://*servername/site/*Documents`.  
  
 Para buscar la información de ruta de acceso para una biblioteca de SharePoint nueva o para un sitio no conocido, abra un explorador y busque la biblioteca de SharePoint en la que desea publicar los informes. Si la biblioteca está vacía, cargue cualquier archivo. Haga clic con el botón derecho en el archivo y seleccione **Propiedades** para abrir la ventana **Propiedades** . La dirección del archivo contiene los valores de dirección URL necesarios para una operación de publicación.  
  
### <a name="fully-qualified-urls-for-items-on-a-sharepoint-site"></a>Direcciones URL completas para los elementos de un sitio de SharePoint  
 Siempre se obtiene acceso a los elementos almacenados en una biblioteca de SharePoint mediante una dirección URL completa que comienza por la aplicación web (`https://*server*`) como nodo raíz y termina por el nombre del archivo al que se hace referencia.  
  
 Los nombres de archivo de la dirección URL deben incluir una extensión de nombre de archivo.  
  
 No se pueden utilizar direcciones URL relativas para los elementos dependientes en los informes que se publican en un sitio de SharePoint. Por ejemplo, no se puede utilizar una dirección URL relativa para hacer referencia a un origen de datos compartido, un modelo de informe o un subinforme. Siempre debe especificarse la dirección URL completa a una biblioteca de SharePoint para cada elemento. No existe ningún método para predecir si un archivo dependiente puede colocarse como si no existiera una jerarquía predefinida a los sitios que puede utilizar para analizar un formato de dirección URL.  
  
 Cuando se publica o se carga un informe que contiene elementos dependientes, deben establecerse las referencias a los elementos dependientes después de haber publicado el informe. No hay ninguna garantía de que las referencias que funcionaban correctamente en el modo de vista previa del Diseñador de informes funcionen después de publicar el informe. Para obtener más información, vea [Publicar desde una herramienta de creación a una biblioteca de SharePoint](#publishingToDocLib) en este tema.  
  
### <a name="urls-for-external-images"></a>Direcciones URL para imágenes externas  
 Una definición de informe puede incluir un archivo de imagen almacenado como un archivo externo. Puede hacer referencia a ese archivo en la definición de informe estableciendo una dirección URL completa al archivo de imagen. Puede almacenarse en un sitio de SharePoint o en un equipo remoto.  
  
> [!IMPORTANT]  
>  Si la dirección URL externa es para una imagen en un sitio de SharePoint, el icono de imagen rota aparecerá al obtener una vista previa del informe en el Generador de informes. Al cargar el informe en el sitio de SharePoint y representarlo en modo conectado, el icono de la imagen rota aparecerá si solo tiene permisos de **View Items** .  
  
 Independientemente del modo del servidor de informes, las referencias a un archivo de imagen externo en un informe deben ser direcciones URL completas. Además, cuando se hace referencia a un archivo de imagen externo, normalmente es necesario configurar la cuenta de procesamiento de informes en modo desatendido.  
  
### <a name="specifying-subreports-and-drillthrough-reports"></a>Especificar subinformes e informes detallados  
 Los subinformes deben residir en la misma carpeta que el informe principal. No puede especificar una carpeta relativa.  
  
 Para especificar los informes detallados, incluya la dirección URL en una expresión. Por ejemplo, para especificar el informe que se denomina SalesDetails como un informe detallado, en la sección Acción del cuadro de texto o el texto del marcador de posición, establezca ReportName como la expresión siguiente:  
  
```  
="https://site/subsite/documentlibrary/SalesDetails.rdl"  
```  
  
### <a name="reserved-names-on-sharepoint-sites"></a>Nombres reservados en sitios de SharePoint  
 Si crea o construye una dirección URL para un elemento que se encuentra en un sitio de SharePoint, tenga en cuenta que las palabras **Personal** y **Sites** son nombres reservados en el sitio predeterminado.  
  
## <a name="examples-of-urls"></a>Ejemplos de direcciones URL  
 Al publicar elementos en una biblioteca de SharePoint, debe especificar direcciones URL completas a la biblioteca de destino. Una dirección URL completa de SharePoint incluye la aplicación web de SharePoint, el sitio, la biblioteca, la carpeta (opcional), el archivo y la extensión de nombre de archivo. Los siguientes ejemplos ilustran la sintaxis que debe utilizarse.  
  
|Destino|Dirección URL de ejemplo|  
|------------|-----------------|  
|Un servidor de SharePoint.|`https://TestServer`|  
|Un sitio o subsitio del servidor de SharePoint.|`https://TestServer/toplevelsite/subsite`|  
|El informe de ejemplo Company Sales de **Documentos compartidos** en una implementación de [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] o [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] .|`https://TestServer/TestSite/Shared%20Documents/Company%20Sales.rdl`|  
|El informe de ejemplo Company Sales de la carpeta **Documentos/Doc** en una instancia de [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] .|`https://TestServer/TestSite/Documents/Doc/Company%20Sales.rdl`|  
|El informe de ejemplo Company Sales de **Centro de informes** en una instancia de [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] .|`https://TestServer/TestSite/Reports/Doc/Company%20Sales.rdl`|  
  
##  <a name="publishingToDocLib"></a> Publicar desde una herramienta de creación a una biblioteca de SharePoint  
 Cuando se usa una herramienta de creación de informes para publicar informes y sus archivos relacionados en una biblioteca, los archivos se validan antes de agregarse. Si carga informes y archivos relacionados mediante la acción **Cargar** en una biblioteca de SharePoint, no se efectúa ninguna comprobación de validación. No podrá saber si el archivo es válido hasta que obtenga acceso al informe para administrarlo, editarlo o ejecutarlo.  
  
> [!NOTE]  
>  Para publicar los informes en un sitio de SharePoint desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], es posible que necesite agregar el sitio de SharePoint a su lista de ubicaciones de confianza en el explorador Internet Explorer.  
  
### <a name="shared-data-sources"></a>Orígenes de datos compartidos  
 Al publicar un origen de datos compartido con una herramienta de creación de informes, establece la propiedad de proyecto **TargetDataSourceFolder**. La carpeta de orígenes de datos de destino debe ser una dirección URL a una biblioteca de SharePoint. A diferencia de lo que ocurre en el modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , no puede especificar una carpeta relativa; las rutas de acceso relativas no son válidas. Si no existe una carpeta en la ruta de acceso a la biblioteca de documentos, se creará una.  
  
 Al publicar un archivo de origen de datos compartido (.rds) en un sitio de SharePoint, se cambia el archivo de origen de datos a una extensión de nombre de archivo .rsds. El archivo .rsds no puede guardarse localmente desde un sitio de SharePoint ni importarse en un proyecto existente de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Los orígenes de datos compartidos con extensiones de nombre de archivo .rds y .rsds no son intercambiables.  
  
#### <a name="shared-data-sources-from-report-designer"></a>Orígenes de datos compartidos del Diseñador de informes  
 Si va a publicar orígenes de datos compartidos de un proyecto del Diseñador de informes, puede usar una dirección URL que especifique la biblioteca de destino, o bien dejar la propiedad en blanco. A diferencia de lo que ocurre en el modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , no puede especificar una carpeta relativa; las rutas de acceso relativas no son válidas. Si no existe una carpeta en la ruta de acceso a la biblioteca de documentos, se creará una. Si deja la carpeta de orígenes de datos de destino en blanco, el origen de datos se publica en la carpeta de informes de destino.  
  
### <a name="file-names"></a>Nombres de archivo  
 Los nombres de archivo de una dirección URL para los elementos de informe deben incluir una extensión de nombre de archivo. La extensión de nombre de archivo determina el tipo de archivo. Al publicar elementos de informe desde una herramienta de creación de informes, la extensión de nombre de archivo se incluye automáticamente. Si carga un elemento de informe en una biblioteca de SharePoint, debe incluir una extensión de nombre de archivo.  
  
 Si no especifica ninguna extensión de nombre de archivo para los elementos que cargue en un sitio de SharePoint, se producirá el error **rsInvalidDataSourceReference** . Los nombres de archivo no deben incluir caracteres que no se reconozcan como caracteres de nombres de archivo válidos por parte de las aplicaciones de SharePoint. No incluya los siguientes caracteres: # % & * : < > ? / { | }.  
  
## <a name="differences-between-uploading-and-publishing"></a>Diferencias entre cargar y publicar  
 Cuando se usa el Diseñador de informes o el Generador de informes para publicar informes y sus archivos relacionados en una biblioteca, los archivos se validan antes de agregarse. Si carga informes y archivos relacionados mediante la acción **Cargar** en una biblioteca de SharePoint, no se efectúa ninguna comprobación de validación. No podrá saber si el archivo es válido hasta que obtenga acceso al informe para administrarlo, editarlo o ejecutarlo.  
  
## <a name="updating-a-published-item"></a>Actualizar un elemento publicado  
 Después de publicar o cargar un elemento en una biblioteca de SharePoint, debe desproteger el elemento de la biblioteca antes de actualizarlo. Mientras el informe se encuentre desprotegido, usted será el único usuario con permiso para cambiar el informe. Cuando finalice, vuelva a protegerlo.  
  
 Si carga o publica un informe sin desproteger antes el documento (por ejemplo, si carga un elemento con el mismo nombre que un elemento existente), el servidor de informes lo desprotegerá por usted, agregará el informe actualizado como una nueva versión del elemento existente y, a continuación, volverá a protegerlo.  
  
## <a name="external-images-as-resources"></a>Imágenes externas como recursos  
 Un servidor de informes que se ejecuta en modo nativo admite el concepto de recurso, que se define como cualquier archivo almacenado y protegido en el servidor de informes, pero que el servidor de informes no procesa. En el modo nativo, puede ser cualquier tipo de archivo.  
  
 Cuando el servidor de informes se ejecuta en el modo integrado de SharePoint, el concepto de recurso tiene una definición más específica. El servidor de informes conserva el concepto de recurso para almacenar informes que hacen referencia a una imagen externa. Esto último se aplica si el informe es una instantánea o una copia que se mantiene para uso interno.  
  
## <a name="see-also"></a>Ver también  
 [Publicar un informe en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Publicación de un origen de datos compartido en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Páginas de propiedades del proyecto (cuadro de diálogo)](../../reporting-services/tools/project-property-pages-dialog-box.md)  
  
  
