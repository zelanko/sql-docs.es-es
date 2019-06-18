---
title: Obtener datos de conjuntos de datos compartidos en informes móviles de Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cac1a32b49fde5b41c0a8ef21706d873ce037cd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061166"
---
# <a name="get-data-from-shared-datasets-in-reporting-services-mobile-reports"></a>Obtener datos de conjuntos de datos compartidos en informes móviles de Reporting Services
Además de [cargar datos de archivos de Excel](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md), el Publicador de informes móviles de Microsoft SQL Server también puede obtener acceso a los datos de prácticamente cualquier origen. El acceso a los datos requiere un origen de datos compartido, configurado en un portal web de Reporting Services. Más información sobre la [creación de orígenes de datos compartidos](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) y la [creación de conjuntos de datos compartidos](../../reporting-services/report-data/manage-shared-datasets.md).  
  
Después de que los orígenes de datos compartidos y los conjuntos de datos compartidos están configurados en el servidor de Reporting Services, puede usarlos en informes móviles creados en [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].   
  
Después de conectarse a un servidor de [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] desde [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)], conectar un informe móvil a un conjunto de datos compartidos es algo sencillo.   
  
1. En la pestaña **Datos** , seleccione **Agregar datos**.  
  
2. Seleccione **Servidor de informes**.   
  
3.  Si esta es la primera vez que se conecta al servidor, rellene la información del nombre del servidor y su nombre y contraseña. Escriba el nombre del servidor en el cuadro Dirección del servidor en este formato:  
  
    \<"nombreServidor">/reports/  
  
    En este ejemplo:  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. Cuando se seleccione el servidor de [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , verá los conjuntos de datos disponibles en carpetas. Seleccione un conjunto de datos para importar los datos en [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
Después de haber importado el conjunto de datos, puede diseñar el informe móvil tal como haría con datos simulados o datos locales de un archivo de Excel.  
  
De forma predeterminada, el conjunto de datos compartido está siempre actualizado con los datos más recientes, porque cada vez que alguien ve un informe móvil basado en ese conjunto de datos, SQL Server ejecuta la consulta subyacente y devuelve los datos más recientes. Es obvio que si muchas personas ven su informe móvil, esta no será la mejor situación, así que puede configurar el almacenamiento en caché para ejecutar la consulta periódicamente y almacenar en caché el conjunto de datos resultante. En esta entrada de blog se explica [cómo funciona el almacenamiento en caché y la actualización de datos en el portal web](https://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/).  
  
## <a name="add-edit-or-remove-a-report-server"></a>Agregar, editar o quitar un servidor de informes  
  
Si ya ha establecido una conexión a un servidor de informes, al seleccionar **Agregar datos** en la pestaña Datos, no verá una opción para agregar otro servidor de informes. En su lugar, siga estos pasos.  
  
1. En la esquina superior izquierda, seleccione **Conexiones**.  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   El panel Conexión del servidor se abrirá en la parte derecha.  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. Agregue una nueva conexión de servidor, o bien edite o quite conexiones existentes.  
  
### <a name="see-also"></a>Vea también  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [Portal web (modo nativo de SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPad](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPhone](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  

