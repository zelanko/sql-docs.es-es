---
title: "Conectar un elemento web Filtro o Documentos (Reporting Services en el modo integrado de SharePoint) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "elemento web Filtro [Reporting Services]"
  - "integración de SharePoint [Reporting Services], elementos web"
  - "elemento web Visor de informes [Reporting Services]"
  - "elemento web Documentos [Reporting Services]"
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Conectar un elemento web Filtro o Documentos (Reporting Services en el modo integrado de SharePoint)
  Si utiliza un producto de SharePoint, puede crear un panel o una página de elementos web que incluya un elemento web Filtro o un elemento web Documentos, y un elemento web Visor de informes. Las versiones admitidas son [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. También se admiten [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] u [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007. Mediante la conexión de un elemento web Filtro, los usuarios que seleccionan valores de filtro en un elemento web Filtro pueden enviar el valor a un informe con parámetros en la misma página. Mediante la conexión de un elemento web Documentos, los usuarios que hacen clic en informes en la biblioteca de documentos pueden ver el informe en un elemento web Visor de informes adyacente.  
  
 El elemento web Filtro sirve para enviar valores a uno o varios parámetros de un informe. Para utilizar un elemento web Filtro, el informe debe tener parámetros definidos que sean compatibles con los valores, tipo de datos y formato que haya enviado el elemento web.  
  
 El elemento web Documentos está asociado a la biblioteca de documentos del sitio principal. Para ver, agregar o quitar elementos de la biblioteca de documentos, haga clic en **Ver todo el contenido del sitio**. En Bibliotecas, haga clic en **Documentos**. Puede utilizar los menús **Nuevo**, **Cargar**y **Acciones** para administrar los elementos de la biblioteca de documentos.  
  
### Para conectar un elemento web Filtro  
  
1.  Abra o cree un panel o una página de elementos web.  
  
2.  En el menú **Acciones del sitio** , haga clic en **Editar página**.  
  
3.  Haga clic en **Agregar elemento web**.  
  
4.  En **Todos los elementos web**, en la categoría **Varios** , seleccione **Visor de informes de SQL Reporting Services**.  
  
5.  Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
6.  En otra zona del mismo panel o página de elementos web, haga clic en **Agregar elemento web**.  
  
7.  En **Todos los elementos web**, en la sección **Filtros** , seleccione un elemento web.  
  
8.  Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
9. En la zona que contiene el elemento web, haga clic en el menú **Edición** del elemento web, seleccione **Conexiones**, **Enviar valores de filtro a** y, después, elija **Visor de informes** - *nombre de informe*.  
  
10. Proteja sus cambios y guarde la página.  
  
### Para conectar un elemento web Documentos  
  
1.  Abra o cree un panel o una página de elementos web.  
  
2.  En el menú **Acciones del sitio** , haga clic en **Editar página**.  
  
3.  Haga clic en **Agregar elemento web**.  
  
4.  En **Todos los elementos web**, en la sección **Listas y bibliotecas** , seleccione **Documentos**.  
  
5.  Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
6.  Haga clic en **Aplicar** en la parte inferior del panel de herramientas y, a continuación, haga clic en **Aceptar** para cerrar el panel.  
  
7.  En otra zona del mismo panel o página de elementos web, haga clic en **Agregar elemento web**.  
  
8.  En **Todos los elementos web**, en la categoría **Varios** , seleccione **Visor de informes de SQL Reporting Services.**  
  
9. Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
10. En la zona que contiene el elemento web, haga clic en el menú **Edición** del elemento web, seleccione **Conexiones**, **Ruta de acceso del sistema de archivos al archivo de definición del informe**y **Documentos**.  
  
11. Proteja sus cambios y guarde la página.  
  
## Vea también  
 [Agregar el elemento web Visor de informes a una página web &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/add the report viewer web part to a web page.md)   
 [Elemento web Visor de informes en un sitio de SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar el elemento web Visor de informes](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  
  
  