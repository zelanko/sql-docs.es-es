---
title: Requisitos previos para los tutoriales (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 17c8b67d29cb82956a37bc3f83867161486a4f9e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73637864"
---
# <a name="prerequisites-for-tutorials-report-builder"></a>Requisitos previos para los tutoriales (Generador de informes)
  Los tutoriales del Generador de informes tienen como objetivo que pueda ver y guardar los informes en un servidor de informes o un sitio de SharePoint que esté integrado con un servidor de informes. Por lo que se refiere a los datos, todos los tutoriales utilizan consultas literales que deben ser procesadas por una instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 Si no tiene acceso a un servidor de informes, un sitio o un origen de datos de informes, puede obtener información acerca del Generador de informes generando un informe sin conexión. Vea [Tutorial: Crear un informe de gráfico rápido sin conexión &#40;Generador de informes&#41;](report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  
  
## <a name="requirements"></a>Requisitos  
 Debe disponer de los siguientes requisitos previos para poder completar los tutoriales relativos al generador de informes:  
  
-   Acceso a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] generador de informes. Puede ejecutar el Generador de informes mediante la versión independiente del Generador de informes o la versión ClickOnce, a su disposición desde el Administrador de informes o un sitio de SharePoint. Solo el primer paso, cómo abrir Generador de informes, es diferente para las versiones de ClickOnce.  
  
     Para usar Administrador de informes, abra Administrador de informes y haga clic en **generador de informes**. De forma predeterminada, la dirección URL para Administrador de informes\<es http://*ServerName*>/Reports.  
  
     Para utilizar un sitio de SharePoint, navegue hasta el sitio, haga clic en la pestaña Documentos, haga clic en Nuevo documento y, en la lista desplegable, haga clic en Informe del Generador de informes. Por ejemplo, http://\<ServerName>/sites/mysite/Reports. El administrador de SharePoint debe habilitar la característica Informe del Generador de informes para cada biblioteca de documentos.  
  
-   La dirección URL a un servidor de informes de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] o a un sitio de SharePoint integrado con un servidor de informes de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] . Debe tener el permiso para guardar y ver informes, orígenes de datos compartidos, conjuntos de datos compartidos, elementos de informe y modelos. De forma predeterminada, la dirección URL de un servidor de\<informes es http://servername>/ReportServer. De forma predeterminada, la dirección URL de un sitio de\<SharePoint es http://siteName\<> o http://Server>/site.  
  
-   El nombre de una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y las credenciales suficientes para el acceso de solo lectura a cualquier base de datos. Las consultas del conjunto de datos de los tutoriales usan datos literales, pero cada consulta debe ser procesada por una instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] para que devuelva los metadatos requeridos por un conjunto de datos de informe. Por ejemplo, la siguiente cadena de conexión especifica solo un servidor: `data source=<servername>`. Debe tener acceso de lectura a la base de datos predeterminada que le ha asignado el administrador del sistema que otorga los permisos de acceso al servidor. También puede especificar una base de datos, como se muestra en la siguiente cadena de conexión: `data source=<servername>;initial catalog=<database>`.  
  
-   Para el tutorial que incluya un mapa, deberá configurarse el servidor de informes para que admita los mapas de Bing como fondo. Para obtener más información, vea [planear la compatibilidad con informes de mapa](plan-for-map-report-support.md) en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en los libros en [pantalla](https://go.microsoft.com/fwlink/?LinkId=154888) de, en MSDN.Microsoft.com.  
  
-   En el tutorial, [Tutorial: crear informes principales y de obtención de detalles &#40;Generador de informes&#41;](tutorial-creating-drillthrough-and-main-reports-report-builder.md), se utiliza el conjunto de información de demostración de Business Intelligence de contoso. Este conjunto de datos está formado por el almacenamiento de datos de ContosoDW y la base de datos de procesamiento analítico en línea (OLAP) de Contoso_Retail. Los informes que creará en este tutorial recuperan los datos del informe desde el cubo de ventas de Contoso. La base de datos OLAP de Contoso_Retail se puede descargar desde el [Centro de descarga Microsoft](https://www.microsoft.com/download/details.aspx?id=18279). Solo necesita descargar el archivo ContosoBIdemoABF.exe. Contiene la base de datos OLAP.  
  
     El otro archivo, ContosoBIdemoBAK.exe, es para el almacenamiento de datos de ContosoDW, que no se utiliza en este tutorial.  
  
     El sitio web incluye instrucciones de extracción y recuperación del archivo de copia de seguridad ContosoRetail.abf a la base de datos OLAP de Contoso_Retail.  
  
     Debe tener acceso a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en donde instalar la base de datos OLAP.  
  
 El administrador del servidor de informes debe otorgarle los permisos necesarios en el servidor de informes, configurar las ubicaciones de carpeta de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] y configurar las opciones predeterminadas del Generador de informes. Para obtener más información, vea [instalar, desinstalar y generador de informes soporte técnico](install-uninstall-and-report-builder-support.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tutoriales &#40;Generador de informes&#41;](report-builder-tutorials.md)  
  
  
