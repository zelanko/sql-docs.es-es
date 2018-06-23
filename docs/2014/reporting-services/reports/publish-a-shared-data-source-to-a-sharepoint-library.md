---
title: Publicar un origen de datos compartido en una biblioteca de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 876609eeb6f6a1490f4d2c7ad9196b08e2558646
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201522"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>Publicar un origen de datos compartido en una biblioteca de SharePoint
  Para publicar un origen de datos compartido en un servidor de informes que se ejecuta en el modo integrado de SharePoint, debe establecer las propiedades de proyecto de informe en el Diseñador de informes. En las propiedades de proyecto, todas las referencias a servidores, informes y orígenes de datos compartidos deben ser direcciones URL completas.  
  
 Debe disponer del permiso **Miembro** o **Propietario** en el sitio de SharePoint. Para obtener más información, vea [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>Para publicar un origen de datos compartido en un sitio de SharePoint  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra un proyecto de servidor de informes nuevo o uno existente.  
  
2.  En el menú **Proyecto** , haga clic en **Propiedades**. Se abre el cuadro de diálogo ***Páginas de propiedades de *\<proyecto>**.  
  
3.  Elija la **Configuración** que utilice para publicar en un sitio de SharePoint.  
  
4.  Si desea publicar los orígenes de datos compartidos del proyecto y sobrescribir los publicados anteriormente, establezca **OverwriteDataSources** en **True**.  
  
5.  (Opcional) Para **TargetDataSourceFolder**, escriba una dirección URL a una biblioteca de SharePoint o a una carpeta de bibliotecas. Por ejemplo, *http://TestServer/TestSite/Documents/DataSources*.  
  
     Si no se especifica ningún valor, se usa el valor **TargetReportFolder** .  
  
6.  Para **TargetReportFolder**, escriba una dirección URL a una biblioteca o a una carpeta de bibliotecas. Por ejemplo, http:*//TestServer/TestSite/Documents/Reports*.  
  
7.  Para **TargetServerURL**, escriba una dirección URL a un sitio de nivel superior o a un subsitio de SharePoint. Si no especifica ningún sitio, se usa el sitio de nivel superior predeterminado. Por ejemplo, http://*nombreDeServidor*, http://*nombreDeServidor*/*sitio*o http://*nombreDeServidor*/*sitio*/*subsitio*.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. En el Explorador de soluciones, haga clic con el botón derecho en el origen de datos compartido que quiera publicar y, después, haga clic en **Implementar**. El origen de datos se publicará en la ubicación especificada en **TargetDataSourceFolder**. Los errores de implementación se mostrarán en la ventana de resultados.  
  
    > [!NOTE]  
    >  Después de publicar un origen de datos compartido en un sitio de SharePoint, se cambia la extensión de nombre de archivo a .rsds. Puede editar y administrar un origen de datos compartido directamente en el sitio de SharePoint. Para más información, vea [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Vea también  
 [Publicar un informe en una biblioteca de SharePoint](publish-a-report-to-a-sharepoint-library.md)   
 [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Páginas de propiedades del proyecto (cuadro de diálogo)](../tools/project-property-pages-dialog-box.md)   
 [Establecer propiedades de implementación &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)   
 [Publicación de informes en un servidor de informes](publishing-reports-to-a-report-server.md)   
 [Usar una conexión de datos de Office &#40;.odc&#41; con informes &#40;modo integrado de Reporting Services en SharePoint&#41;](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  