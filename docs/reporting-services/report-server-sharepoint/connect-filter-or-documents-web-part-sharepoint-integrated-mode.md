---
title: Conectar el elemento web filtro o documentos con un elemento web del Visor de informes de Reporting Services | Documentos de Microsoft
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 87d4b4a3f0c01804329f3a7b0688632c20ed6c9b
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>Conectar el elemento web filtro o documentos con un elemento web del Visor de informes de Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Si está usando un producto de SharePoint, puede crear un elemento web o panel de página que incluya un elemento web filtro o elemento web documentos y un elemento web Visor de informes. Las versiones admitidas son [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. También se admiten [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] u [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007. Al conectar un elemento web filtro, los usuarios que seleccionan valores de filtro en un elemento web filtro pueden enviar el valor a un informe con parámetros en la misma página. Al conectar un elemento web documentos, los usuarios que hacen clic en informes en la biblioteca de documentos pueden ver el informe en un elemento web de Visor de informes adyacente.

> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

 El elemento web filtro sirve para enviar valores a uno o varios parámetros en un informe. Para usar un elemento web filtro, el informe debe tener parámetros definidos que son compatibles con los valores, el tipo de datos y el formato que haya enviado el elemento web.  
  
 El elemento web documentos está asociado a la biblioteca de documentos del sitio principal. Para ver, agregar o quitar elementos de la biblioteca de documentos, haga clic en **Ver todo el contenido del sitio**. En Bibliotecas, haga clic en **Documentos**. Puede utilizar los menús **Nuevo**, **Cargar**y **Acciones** para administrar los elementos de la biblioteca de documentos.  
  
## <a name="connect-a-filter-web-part"></a>Conectar un elemento web filtro
  
1.  Abra o cree un panel o página de elementos web.  
  
2.  En el menú **Acciones del sitio** , haga clic en **Editar página**.  
  
3.  Haga clic en **agregar un elemento web**.  
  
4.  En **todos los elementos web**, en la **varios** categoría, seleccione **Visor de informes de SQL Server Reporting Services**.  
  
5.  Haga clic en **Agregar**. El elemento web se agrega en la parte superior de la zona.  
  
6.  En otra zona en la misma página de elementos web o un panel, haga clic en **agregar un elemento web**.  
  
7.  En **todos los elementos web**, en la **filtros** sección, seleccione un elemento web.  
  
8.  Haga clic en **Agregar**. El elemento web se agrega en la parte superior de la zona.  
  
9. En la zona que contiene el elemento web, haga clic en el elemento web **editar** menú, elija **conexiones**, seleccione **enviar valores de filtro a**y, a continuación, seleccione **informes Visor de** - *nombre del informe*.  
  
10. Proteja sus cambios y guarde la página.  
  
## <a name="connect-a-documents-web-part"></a>Conectar un elemento web documentos  
  
1.  Abra o cree un panel o página de elementos web.  
  
2.  En el menú **Acciones del sitio** , haga clic en **Editar página**.  
  
3.  Haga clic en **agregar un elemento web**.  
  
4.  En **todos los elementos web**, en la **listas y bibliotecas** sección, seleccione **documentos.**  
  
5.  Haga clic en **Agregar**. El elemento web se agrega en la parte superior de la zona.  
  
6.  Haga clic en **Aplicar** en la parte inferior del panel de herramientas y, a continuación, haga clic en **Aceptar** para cerrar el panel.  
  
7.  En otra zona en la misma página de elementos web o un panel, haga clic en **agregar un elemento web**.  
  
8.  En **todos los elementos web**, en la **varios** categoría, seleccione **Visor de informes de SQL Server Reporting Services.**  
  
9. Haga clic en **Agregar**. El elemento web se agrega en la parte superior de la zona.  
  
10. En la zona que contiene el elemento web, haga clic en el elemento web **editar** menú, elija **conexiones**, seleccione **obtener las definiciones de informe de**y, a continuación, seleccione  **Documentos**.  
  
11. Proteja sus cambios y guarde la página.  
  
## <a name="see-also"></a>Vea también

 [Agregar el elemento web Visor de informes a una página web](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [Elemento web Visor de informes en un sitio de SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalización del elemento web Visor de informes](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
