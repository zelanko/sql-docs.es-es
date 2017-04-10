---
title: "Publicar un informe en una biblioteca de SharePoint | Microsoft Docs"
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
  - "implementar [Reporting Services], informes en modo integrado de SharePoint"
  - "integración de SharePoint [Reporting Services], publicar en una biblioteca"
  - "publicar informes [Reporting Services], en una biblioteca de SharePoint"
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# Publicar un informe en una biblioteca de SharePoint
  Para publicar un informe en un sitio de SharePoint configurado para la integración de SharePoint, debe establecer las propiedades del proyecto en el Diseñador de informes. En las propiedades de proyecto, todas las referencias a servidores, informes y orígenes de datos compartidos deben ser direcciones URL completas. En la definición de informe, todas las referencias a subinformes, informes detallados y recursos, como imágenes basadas en web, deben ser direcciones URL completas.  
  
 Debe disponer del permiso **Miembro** o **Propietario** en el sitio de SharePoint para establecer las propiedades en el proyecto. Para más información, vea [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### Para publicar un informe en un sitio de SharePoint  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra un nuevo proyecto de servidor de informes o uno existente.  
  
2.  En el menú **Proyecto** , haga clic en **Propiedades**. Se abrirá el cuadro de diálogo *\<proyecto>***Páginas de propiedades**.  
  
3.  En la lista **Configuración** , seleccione el nombre de una configuración de generación de soluciones para usarla en la generación y publicación del informe. La configuración actual aparece como **Activo**(*\<configuración>*).  
  
4.  Si desea publicar los orígenes de datos compartidos del proyecto y sobrescribir los publicados anteriormente, establezca **OverwriteDataSources** en **True**.  
  
5.  (Opcional) Para **TargetDataSourceFolder**, escriba una dirección URL a una biblioteca de SharePoint o una carpeta de biblioteca (por ejemplo, *http://servidorDePrueba/sitioDePrueba/Documentos/orígenesDeDatos)*.  
  
     Si no se especifica ningún valor, se usa el valor **TargetReportFolder** .  
  
6.  Para **TargetReportFolder**, escriba una dirección URL a una biblioteca o una carpeta de biblioteca (por ejemplo, *http://servidorDePrueba/sitioDePrueba/Documentos/Informes*).  
  
7.  Para **TargetServerURL**, escriba una dirección URL a un sitio de primer nivel o a un subsitio de SharePoint. Si no especifica ningún sitio, se usa el sitio de primer nivel predeterminado (por ejemplo, *http://nombreDeServidor*, *http://nombreDeServidor/sitio* o *http://nombreDeServidor/sitio/subsitio*).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. En el Explorador de soluciones, haga clic con el botón derecho en el informe que quiera publicar y haga clic en **Implementar**. El informe se publicará en la ubicación especificada en **TargetReportFolder**. Los errores de implementación se mostrarán en la ventana de resultados.  
  
## Vea también  
 [Páginas de propiedades del proyecto (cuadro de diálogo)](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Establecer propiedades de implementación &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Publicar informes en un servidor de informes](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Usar una conexión de datos de Office &#40;.odc&#41; con informes &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-data/use an office data connection (.odc) with reports.md)  
  
  