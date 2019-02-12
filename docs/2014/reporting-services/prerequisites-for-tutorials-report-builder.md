---
title: Requisitos previos para los tutoriales (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5c964a2cfe70eafd08bbd1ba73373a9d7acee34e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030236"
---
# <a name="prerequisites-for-tutorials-report-builder"></a>Requisitos previos para los tutoriales (Generador de informes)
  Los tutoriales del Generador de informes tienen como objetivo que pueda ver y guardar los informes en un servidor de informes o un sitio de SharePoint que esté integrado con un servidor de informes. Por lo que se refiere a los datos, todos los tutoriales utilizan consultas literales que deben ser procesadas por una instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 Si no tiene acceso a un servidor de informes, un sitio o un origen de datos de informes, puede obtener información acerca del Generador de informes generando un informe sin conexión. Consulte [Tutorial: Crear un informe de gráfico rápido sin conexión &#40;generador de informes&#41;](report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  
  
## <a name="requirements"></a>Requisitos  
 Debe disponer de los siguientes requisitos previos para poder completar los tutoriales relativos al generador de informes:  
  
-   Acceso al Generador de informes de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Puede ejecutar el Generador de informes mediante la versión independiente del Generador de informes o la versión ClickOnce, a su disposición desde el Administrador de informes o un sitio de SharePoint. El primer paso, cómo abrir el generador de informes es diferente para las versiones de ClickOnce.  
  
     Para usar el Administrador de informes, abra el Administrador de informes y haga clic en **Report Builder**. De forma predeterminada, la dirección URL del Administrador de informes es http://\<*servername*> / reports.  
  
     Para utilizar un sitio de SharePoint, navegue hasta el sitio, haga clic en la pestaña Documentos, haga clic en Nuevo documento y, en la lista desplegable, haga clic en Informe del Generador de informes. Por ejemplo, http://\<servername >/sitios/mySite/reports. El administrador de SharePoint debe habilitar la característica Informe del Generador de informes para cada biblioteca de documentos.  
  
-   La dirección URL a un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] informe de servidor o un sitio de SharePoint que está integrado con un [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] servidor de informes. Debe tener el permiso para guardar y ver informes, orígenes de datos compartidos, conjuntos de datos compartidos, elementos de informe y modelos. De forma predeterminada, la dirección URL de un servidor de informes es http://\<servername > / reportserver. De forma predeterminada, la dirección URL para un sitio de SharePoint es http://\<sitename > o http://\<server > / site.  
  
-   El nombre de un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] instancia y las credenciales suficientes para tener acceso de solo lectura a cualquier base de datos. Las consultas del conjunto de datos de los tutoriales usan datos literales, pero cada consulta debe ser procesada por una instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] para que devuelva los metadatos requeridos por un conjunto de datos de informe. Por ejemplo, la siguiente cadena de conexión especifica solo un servidor: `data source=<servername>`. Debe tener acceso de lectura a la base de datos predeterminada que le ha asignado el administrador del sistema que otorga los permisos de acceso al servidor. También puede especificar una base de datos, como se muestra en la siguiente cadena de conexión: `data source=<servername>;initial catalog=<database>`.  
  
-   Para el tutorial que incluya un mapa, deberá configurarse el servidor de informes para que admita los mapas de Bing como fondo. Para obtener más información, consulte [planear la compatibilidad de informe de mapa de](plan-for-map-report-support.md) en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] documentación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [libros](https://go.microsoft.com/fwlink/?LinkId=154888) en msdn.microsoft.com.  
  
-   El tutorial, [Tutorial: Crear informes principales y obtención de detalles &#40;Report Builder&#41;](tutorial-creating-drillthrough-and-main-reports-report-builder.md), usa el conjunto de datos de demostración de Contoso business intelligence. Este conjunto de datos está formado por el almacenamiento de datos de ContosoDW y la base de datos de procesamiento analítico en línea (OLAP) de Contoso_Retail. Los informes que creará en este tutorial recuperan los datos del informe desde el cubo de ventas de Contoso. La base de datos OLAP de Contoso_Retail se puede descargar desde el [Centro de descarga Microsoft](https://go.microsoft.com/fwlink/?LinkID=191575). Solo necesita descargar el archivo ContosoBIdemoABF.exe. Contiene la base de datos OLAP.  
  
     El otro archivo, ContosoBIdemoBAK.exe, es para el almacenamiento de datos de ContosoDW, que no se utiliza en este tutorial.  
  
     El sitio web incluye instrucciones de extracción y recuperación del archivo de copia de seguridad ContosoRetail.abf a la base de datos OLAP de Contoso_Retail.  
  
     Debe tener acceso a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en donde instalar la base de datos OLAP.  
  
 El administrador del servidor de informes debe otorgarle los permisos necesarios en el servidor de informes, configurar las ubicaciones de carpeta de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] y configurar las opciones predeterminadas del Generador de informes. Para obtener más información, consulte [instalar, desinstalar y asistencia del generador de informes](install-uninstall-and-report-builder-support.md).  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales &#40;generador de informes&#41;](report-builder-tutorials.md)  
  
  
