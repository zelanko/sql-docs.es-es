---
title: Publicar un origen de datos compartido en una biblioteca de SharePoint | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fd8444cc0bcdfe29268504cf2441c10d67a9ad0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65577517"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>Publicar un origen de datos compartido en una biblioteca de SharePoint
  Para publicar un origen de datos compartido en un servidor de informes que se ejecuta en el modo integrado de SharePoint, debe establecer las propiedades de proyecto de informe en el Diseñador de informes. En las propiedades de proyecto, todas las referencias a servidores, informes y orígenes de datos compartidos deben ser direcciones URL completas.  
  
 Debe disponer del permiso **Miembro** o **Propietario** en el sitio de SharePoint. Para obtener más información, vea [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>Para publicar un origen de datos compartido en un sitio de SharePoint  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra un proyecto de servidor de informes nuevo o uno existente.  
  
2.  En el menú **Proyecto** , haga clic en **Propiedades**. Se abre el cuadro de diálogo **Páginas de propiedades** de _\<proyecto>_ .  
  
3.  Elija la **Configuración** que utilice para publicar en un sitio de SharePoint.  
  
4.  Si desea publicar los orígenes de datos compartidos del proyecto y sobrescribir los publicados anteriormente, establezca **OverwriteDataSources** en **True**.  
  
5.  (Opcional) Para **TargetDataSourceFolder**, escriba una dirección URL a una biblioteca de SharePoint o a una carpeta de bibliotecas. Por ejemplo, `https://TestServer/TestSite/Documents/DataSources`.  
  
     Si no se especifica ningún valor, se usa el valor **TargetReportFolder** .  
  
6.  Para **TargetReportFolder**, escriba una dirección URL a una biblioteca o a una carpeta de bibliotecas. Por ejemplo, `https://TestServer/TestSite/Documents/Reports`.  
  
7.  Para **TargetServerURL**, escriba una dirección URL a un sitio de nivel superior o a un subsitio de SharePoint. Si no especifica ningún sitio, se usa el sitio de nivel superior predeterminado. Por ejemplo, `https://servername`, `https://servername/site` o `https://servername/site/subsite`.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. En el Explorador de soluciones, haga clic con el botón derecho en el origen de datos compartido que quiera publicar y, después, haga clic en **Implementar**. El origen de datos se publicará en la ubicación especificada en **TargetDataSourceFolder**. Los errores de implementación se mostrarán en la ventana de resultados.  
  
    > [!NOTE]  
    >  Después de publicar un origen de datos compartido en un sitio de SharePoint, se cambia la extensión de nombre de archivo a .rsds. Puede editar y administrar un origen de datos compartido directamente en el sitio de SharePoint. Para más información, vea [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
## <a name="see-also"></a>Consulte también  
 [Publicar un informe en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Páginas de propiedades del proyecto (cuadro de diálogo)](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Establecer propiedades de implementación &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Publicar informes en un servidor de informes](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Usar una conexión de datos de Office &#40;.odc&#41; con informes &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
