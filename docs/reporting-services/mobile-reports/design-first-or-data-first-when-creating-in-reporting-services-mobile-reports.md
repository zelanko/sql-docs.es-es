---
title: "Dise&#241;ar primero o datos en primer lugar al crear informes de Reporting Services m&#243;viles | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a7b355fa-312b-4074-bc9b-776269d4fb51
caps.latest.revision: 17
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 17
---
# Dise&#241;ar primero o datos en primer lugar al crear informes de Reporting Services m&#243;viles
  
Con [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)], puede crear informes móviles de con un escalado adecuado hasta cualquier tamaño de pantalla en una superficie de diseño con cuadrícula ajustable de filas y columnas y elementos flexibles de informes móviles.   
  
Al crear informes móviles, tiene la opción de elegir entre dos enfoques básicos: empezar primero con los datos o empezar primero con el diseño. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] admite ambas opciones.   
  
## Primero el diseño  
  
En el diagrama siguiente se muestran los componentes de la vista de diseño del [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]:   
  
![SS_MRP_LayoutTab](../../reporting-services/mobile-reports/media/ss-mrp-layouttab.png)  
  
En el enfoque con prioridad en el diseño, primero se creará un diseño de informe móvil sin importar ningún dato. Se trata de una buena manera de crear un informe móvil cuando no está seguro de si los datos tienen el formato correcto. Sin datos reales, los elementos de la galería se enlazan automáticamente a los datos simulados generados, que puede exportar y usar como plantilla para describir los datos necesarios.  
  
## Primero lo datos  
En el enfoque en que se da prioridad a los datos, en primer lugar se importan todos los datos necesarios, luego se diseña el informe móvil y se establecen las propiedades de los elementos del informe móvil. Esto tiene la ventaja de poder conectar cada elemento con datos reales cuando se agregan al diseño. Cuando se usa un enfoque en que se da prioridad a los datos, asegúrese de que los datos reales tienen el formato correcto para utilizarlos con [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)].   
  
 En el diagrama siguiente se muestran todos los componentes de la vista de datos del [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]:  
  
![SS_MRP_DataTab](../../reporting-services/mobile-reports/media/ss-mrp-datatab.png)  
  
### Vea también  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPad](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports) (Power BI para iOS)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPhone](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  
