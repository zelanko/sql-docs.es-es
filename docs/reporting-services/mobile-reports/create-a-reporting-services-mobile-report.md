---
title: Creación de un informe móvil de Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e84dc855-aede-4fb4-b721-e6d8787961f4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3fd0fc3530ec35da61e2314ef7a80a58d9bdd7d
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710706"
---
# <a name="create-a-reporting-services-mobile-report"></a>Creación de un informe móvil de Reporting Services
Con el Publicador de informes móviles de Microsoft SQL Server, puede crear informes móviles de SQL Server Reporting Services con un escalado adecuado hasta cualquier tamaño de pantalla en una superficie de diseño con cuadrícula ajustable de filas y columnas, y elementos flexibles de informes móviles.  
  
La primera vez que crea un informe móvil, puede instalar el Publicador de informes móviles de Microsoft SQL Server en la máquina local desde el portal web de Reporting Services. También puede instalarlo desde el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkID=733527). Después de la primera ejecución, puede iniciarlo desde el portal web o localmente.   
    
1. En la barra superior del portal web de Reporting Services, seleccione **Nuevo** > **Informe móvil**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. En la pestaña **Diseño** del Publicador de informes móviles, seleccione un navegador, medidor, gráfico, mapa o cuadrícula de datos y arrástrela a la cuadrícula de diseño.  
  
3. Agarre la esquina inferior derecha del elemento y arrástrelo hasta el tamaño que desee.  
  
   ![SSMRP_ResizeChart](../../reporting-services/mobile-reports/media/ssmrp-resizechart.png)  
  
   Esta es la cuadrícula de diseño **Maestra** , donde crea los elementos que desea en el informe. Posteriormente, puede [diseñar el informe para una tableta o un teléfono](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md).     
     
   En **Visual Properties** (Propiedades visuales) debajo de la cuadrícula de diseño, observe las distintas propiedades que puede establecer.  
     
4. Seleccione la pestaña **Datos** en la esquina superior izquierda y verá que el gráfico ya ha simulado los datos asociados con él.   
  
   ![SSMRP_SimTable](../../reporting-services/mobile-reports/media/ssmrp-simtable.png)  
  
5. Seleccione **Agregar datos** en la esquina superior derecha.  
  
6. Seleccione **Local Excel** (Excel Local) o **Servidor de informes**.  
  
   >**Sugerencias**: Si va a agregar datos desde Excel, asegúrese de:  
    >* [Preparar los datos de Excel](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md) para trabajar en el informe móvil.  
    >* Cerrar el archivo primero.  
7. Seleccione las hojas de cálculo que desee y seleccione **Importar**.   
   Puede agregar más de una hoja de cálculo de un libro a la vez.  
    
     ![SSMRP_AddExcelData](../../reporting-services/mobile-reports/media/ssmrp-addexceldata.png)  
  
8. En la pestaña **Datos** , en el cuadro **Propiedades datos** , seleccione la tabla y el campo que desee en el gráfico.  
  
   ![SSMRP_DataProps](../../reporting-services/mobile-reports/media/ssmrp-dataprops.png)  
  
9. De nuevo en la pestaña **Diseño** , en el cuadro **Visual Properties** (Propiedades visuales) puede establecer propiedades como **Título**, **Unidad de tiempo**y **Formato de número**.  
  
   ![SSMRP_ChartVizProps](../../reporting-services/mobile-reports/media/ssmrp-chartvizprops.png)  
    
10. Seleccione **Vista previa** en la parte superior izquierda para ver cómo se presenta el informe.  
  
11. Es el momento de guardar el informe. Seleccione el icono Guardar situado en la parte superior izquierda y elija **Save Locally (Guardar localmente)** o **Save to Server (Guardarlo en el servidor)**.  
  
   Para guardarlo en un servidor, necesita tener acceso a un servidor de informes de SQL Server Reporting Services.  
     
   ### <a name="see-also"></a>Vea también  
     
-   [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-   [Diseñar un informe de Reporting Services móvil para tableta o teléfono](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)  
  
   
