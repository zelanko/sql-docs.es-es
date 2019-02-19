---
title: Diseñar primero o datos en primer lugar al crear informes móviles de Reporting Services | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: a7b355fa-312b-4074-bc9b-776269d4fb51
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bad5837441bf272e600e0c7f8ca85252be53a618
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295883"
---
# <a name="design-first-or-data-first-when-creating-in-reporting-services-mobile-reports"></a>Diseñar primero o datos en primer lugar al crear informes de Reporting Services móviles
  
Con [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)], puede crear informes móviles de con un escalado adecuado hasta cualquier tamaño de pantalla en una superficie de diseño con cuadrícula ajustable de filas y columnas y elementos flexibles de informes móviles.   
  
Al crear informes móviles, tiene la opción de elegir entre dos enfoques básicos: empezar primero con los datos o empezar primero con el diseño. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] admite ambas opciones.   
  
## <a name="design-first"></a>Primero el diseño  
  
En el diagrama siguiente se muestran los componentes de la vista de diseño del [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] :   
  
![SS_MRP_LayoutTab](../../reporting-services/mobile-reports/media/ss-mrp-layouttab.png)  
  
En el enfoque con prioridad en el diseño, primero se creará un diseño de informe móvil sin importar ningún dato. Se trata de una buena manera de crear un informe móvil cuando no está seguro de si los datos tienen el formato correcto. Sin datos reales, los elementos de la galería se enlazan automáticamente a los datos simulados generados, que puede exportar y usar como plantilla para describir los datos necesarios.  
  
## <a name="data-first"></a>Primero lo datos  
En el enfoque en que se da prioridad a los datos, en primer lugar se importan todos los datos necesarios, luego se diseña el informe móvil y se establecen las propiedades de los elementos del informe móvil. Esto tiene la ventaja de poder conectar cada elemento con datos reales cuando se agregan al diseño. Cuando se usa un enfoque en que se da prioridad a los datos, asegúrese de que los datos reales tienen el formato correcto para utilizarlos con [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)].   
  
 En el diagrama siguiente se muestran todos los componentes de la vista de datos del [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] :  
  
![SS_MRP_DataTab](../../reporting-services/mobile-reports/media/ss-mrp-datatab.png)  
  
### <a name="see-also"></a>Vea también  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPad](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPhone](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  

