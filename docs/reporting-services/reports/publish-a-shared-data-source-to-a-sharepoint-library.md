---
title: "Publicar un origen de datos compartido en una biblioteca de SharePoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "orígenes de datos [Reporting Services], publicar en una biblioteca de SharePoint"
  - "integración de SharePoint [Reporting Services], publicar en una biblioteca"
  - "publicar informes [Reporting Services], en una biblioteca de SharePoint"
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 14
---
# Publicar un origen de datos compartido en una biblioteca de SharePoint
  Para publicar un origen de datos compartido en un servidor de informes que se ejecuta en el modo integrado de SharePoint, debe establecer las propiedades de proyecto de informe en el Diseñador de informes. En las propiedades de proyecto, todas las referencias a servidores, informes y orígenes de datos compartidos deben ser direcciones URL completas.  
  
 Debe disponer del permiso **Miembro** o **Propietario** en el sitio de SharePoint. Para obtener más información, vea [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### Para publicar un origen de datos compartido en un sitio de SharePoint  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra un proyecto de servidor de informes nuevo o uno existente.  
  
2.  En el menú **Proyecto** , haga clic en **Propiedades**. Se abrirá el cuadro de diálogo **Páginas de propiedades** de *\<project>*.  
  
3.  Elija la **Configuración** que utilice para publicar en un sitio de SharePoint.  
  
4.  Si desea publicar los orígenes de datos compartidos del proyecto y sobrescribir los publicados anteriormente, establezca **OverwriteDataSources** en **True**.  
  
5.  (Opcional) Para **TargetDataSourceFolder**, escriba una dirección URL a una biblioteca de SharePoint o a una carpeta de bibliotecas. Por ejemplo, *http://TestServer/TestSite/Documents/DataSources*.  
  
     Si no se especifica ningún valor, se usa el valor **TargetReportFolder** .  
  
6.  Para **TargetReportFolder**, escriba una dirección URL a una biblioteca o a una carpeta de bibliotecas. Por ejemplo, http:*//TestServer/TestSite/Documents/Reports*.  
  
7.  Para **TargetServerURL**, escriba una dirección URL a un sitio de nivel superior o a un subsitio de SharePoint. Si no especifica ningún sitio, se usa el sitio de nivel superior predeterminado. Por ejemplo, http://*nombreDeServidor*, http://*nombreDeServidor*/*sitio* o http://*nombreDeServidor*/*sitio*/*subsitio*.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. En el Explorador de soluciones, haga clic con el botón derecho en el origen de datos compartido que quiera publicar y, después, haga clic en **Implementar**. El origen de datos se publicará en la ubicación especificada en **TargetDataSourceFolder**. Los errores de implementación se mostrarán en la ventana de resultados.  
  
    > [!NOTE]  
    >  Después de publicar un origen de datos compartido en un sitio de SharePoint, se cambia la extensión de nombre de archivo a .rsds. Puede editar y administrar un origen de datos compartido directamente en el sitio de SharePoint. Para obtener más información, vea [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md).  
  
## Vea también  
 [Publicar un informe en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Páginas de propiedades del proyecto (cuadro de diálogo)](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Establecer propiedades de implementación &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Publicar informes en un servidor de informes](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Usar una conexión de datos de Office &#40;.odc&#41; con informes &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-data/use an office data connection (.odc) with reports.md)  
  
  