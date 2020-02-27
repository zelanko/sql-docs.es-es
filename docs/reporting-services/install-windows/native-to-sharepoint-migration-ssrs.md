---
title: Migración del modo nativo al modo de SharePoint | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: c5b15bec-6fde-4174-bcde-d043307244dd
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4ae49e1110a1d539cbe7095f946be7fc522b80b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082624"
---
# <a name="native-to-sharepoint-migration-ssrs"></a>Migración del modo nativo al modo de SharePoint (SSRS)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  No se puede actualizar o convertir desde un modo de servidor de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a otro. Por ejemplo, no puede actualizar o convertir un servidor de informes en modo nativo al modo de SharePoint. No puede copiar las bases de datos del servidor de informes entre distintos modos porque usan distintos esquemas de la base de datos. Puede migrar el contenido de un servidor de informes a otro. Las herramientas que use dependen del modo del servidor de informes configurado para los servidores de origen y de destino.  
  
##  <a name="bkmk_native_to_sharepoint"></a> Herramienta de migración de Reporting Services  
 La herramienta admite la migración de contenido de una implementación en modo nativo a una implementación en modo de SharePoint. La herramienta no admite la migración del modo de SharePoint al modo de SharePoint o del modo de SharePoint al modo nativo.  
  
 Para más información, consulte la página de la [herramienta de migración de Reporting Services](https://www.microsoft.com/download/details.aspx?id=29560) (https://www.microsoft.com/download/details.aspx?id=29560).  
  
## <a name="use-script-to-migrate-content"></a>Usar Script para migrar contenido  
 Si la herramienta de migración no satisface sus necesidades, puede migrar manualmente los datos del servidor de informes. A continuación se muestra un resumen de los pasos necesarios para migrar elementos de informe de una implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a otra. El método admite el modo nativo o de SharePoint como servidores de origen o de destino.  
  
1.  Realice copias de seguridad y restaure las claves de cifrado. Esta es la clave que se emplea para cifrar datos. La clave de cifrado también se usa para cifrar contraseñas, como las contraseñas almacenadas para las conexiones a orígenes de datos. Sin embargo, las contraseñas no se pueden migrar y deberá especificarlas de nuevo en el entorno de destino.  
  
2.  **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Scripts de RSS:** Escriba un script de Visual Basic que llame a los métodos SOAP del servicio web del servidor de informes para copiar datos entre las bases de datos. Emplee la utilidad **RS.exe** para ejecutar el script. Rs.exe se instala con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
    -   [Script rs.exe para copiar contenido entre servidores de informes de servicios de informes de ejemplo](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md). En los temas se explica cómo usar el script de ejemplo que puede descargar de CodePlex.  
  
    -   El script de rss de ejemplo de CodePlex, [Script Reporting Services RS.exe que migra contenido de un servidor de informes a otro](https://azuresql.codeplex.com/releases/view/115207).  
  
    -   [Scripting y PowerShell con Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md)  
  
 En la tabla siguiente se resumen los objetos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que puede migrar mediante scripts:  
  
|Object|Se puede incluir en scripts|Comentarios|  
|------------|---------------------|--------------|  
|Informes|Sí|Tras la migración, vuelva a escribir las contraseñas para los orígenes de datos.|  
|Orígenes de datos|Sí|Tras la migración, vuelva a vincular los informes con los orígenes de datos.|  
|Modelos|Sí||  
|Conjuntos de datos|Sí||  
|Elementos de informe||Tras la migración, compruebe o actualice la ruta de acceso a los elementos de informe.|  
|Programaciones|Sí|Vea el método ListSchedules en [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md).|  
|Suscripciones|sí|Vea el método List Subscriptions en [Subscription and Delivery Methods](../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md) y el método <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A> .|  
|Instantáneas|||

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
