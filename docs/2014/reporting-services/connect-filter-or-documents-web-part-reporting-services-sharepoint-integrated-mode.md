---
title: Conectar el elemento Web filtro o documentos (Reporting Services en el modo integrado de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 062733f1ee68cd90ccc1b9a15d0cadc06b7e6f89
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109714"
---
# <a name="connect-filter-or-documents-web-part-reporting-services-in-sharepoint-integrated-mode"></a>Conectar un elemento web Filtro o Documentos (Reporting Services en el modo integrado de SharePoint)
  Si utiliza un producto de SharePoint, puede crear un panel o una página de elementos web que incluya un elemento web Filtro o un elemento web Documentos, y un elemento web Visor de informes. Las versiones admitidas son [!INCLUDE[SPF2010](../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../includes/sps2010-md.md)]. También se admiten [!INCLUDE[winSPServ3](../includes/winspserv3-md.md)] u [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007. Mediante la conexión de un elemento web Filtro, los usuarios que seleccionan valores de filtro en un elemento web Filtro pueden enviar el valor a un informe con parámetros en la misma página. Mediante la conexión de un elemento web Documentos, los usuarios que hacen clic en informes en la biblioteca de documentos pueden ver el informe en un elemento web Visor de informes adyacente.  
  
 El elemento web Filtro sirve para enviar valores a uno o varios parámetros de un informe. Para utilizar un elemento web Filtro, el informe debe tener parámetros definidos que sean compatibles con los valores, tipo de datos y formato que haya enviado el elemento web.  
  
 El elemento web Documentos está asociado a la biblioteca de documentos del sitio principal. Para ver, agregar o quitar elementos de la biblioteca de documentos, haga clic en **Ver todo el contenido del sitio**. En Bibliotecas, haga clic en **Documentos**. Puede utilizar los menús **Nuevo**, **Cargar**y **Acciones** para administrar los elementos de la biblioteca de documentos.  
  
### <a name="to-connect-a-filter-web-part"></a>Para conectar un elemento web Filtro  
  
1.  Abra o cree un panel o una página de elementos web.  
  
2.  En el menú **Acciones del sitio** , haga clic en **Editar página**.  
  
3.  Haga clic en **Agregar un elemento Web**.  
  
4.  En **todos los elementos Web**, en la categoría **varios** , seleccione **SQL Server Reporting Services visor de informes**.  
  
5.  Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
6.  En otra zona de la misma página o panel de elementos Web, haga clic en **Agregar un elemento Web**.  
  
7.  En **todos los elementos Web**, en la sección **filtros** , seleccione un elemento Web.  
  
8.  Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
9. En la zona que contiene el elemento Web, haga clic en el menú **edición** del elemento Web, seleccione **conexiones**, **Enviar valores de filtro a**y, a continuación, seleccione **visor** - de informes*nombre de informe*.  
  
10. Proteja sus cambios y guarde la página.  
  
### <a name="to-connect-a-documents-web-part"></a>Para conectar un elemento web Documentos  
  
1.  Abra o cree un panel o una página de elementos web.  
  
2.  En el menú **Acciones del sitio** , haga clic en **Editar página**.  
  
3.  Haga clic en **Agregar un elemento Web**.  
  
4.  En **todos los elementos Web**, en la sección **listas y bibliotecas** , seleccione **documentos.**  
  
5.  Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
6.  Haga clic en **Aplicar** en la parte inferior del panel de herramientas y, a continuación, haga clic en **Aceptar** para cerrar el panel.  
  
7.  En otra zona de la misma página o panel de elementos Web, haga clic en **Agregar un elemento Web**.  
  
8.  En **todos los elementos Web**, en la categoría **varios** , seleccione **SQL Server Reporting Services visor de informes.**  
  
9. Haga clic en **Agregar**. El elemento web se agregará a la parte superior de la zona.  
  
10. En la zona que contiene el elemento Web, haga clic en el menú **edición** del elemento Web, seleccione **conexiones**, **obtener definiciones de informe de**y, a continuación, seleccione **documentos**.  
  
11. Proteja sus cambios y guarde la página.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar el elemento Web visor de informes a una página web &#40;Reporting Services en el modo integrado de SharePoint&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [Elemento Web visor de informes en un sitio de SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar el elemento Web visor de informes](../../2014/reporting-services/customize-the-report-viewer-web-part.md)  
  
  
