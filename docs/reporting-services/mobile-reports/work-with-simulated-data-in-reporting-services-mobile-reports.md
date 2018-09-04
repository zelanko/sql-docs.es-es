---
title: Trabajar con datos simulados en los informes móviles de Reporting Services | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 6baabc36-58fb-4a98-bb9c-c42bafb16d0f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 038765210b219d91297cd738838350a8b877b25a
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277346"
---
# <a name="work-with-simulated-data-in-reporting-services-mobile-reports"></a>Trabajar con datos simulados en los informes móviles de Reporting Services
Cuando se coloca un elemento de galería en la superficie de diseño, el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] genera de inmediato datos simulados para ese elemento. Estos datos sirven para una serie de propósitos útiles al crear informes móviles.   
  
![SS_MRP_SimDataTreeMapProps](../../reporting-services/mobile-reports/media/ss-mrp-simdatatreemapprops.png)  
  
Los datos simulados son de ayuda cuando se toma un enfoque basado en el diseño para crear informes móviles. La acción de llenar inicialmente los elementos con datos simulados permite crear rápidamente prototipos de informes móviles sin necesidad de cumplir requisitos de datos específicos. Estos informes móviles se pueden evaluar después para comprobar su estética y eficacia en general.  
  
## <a name="create-an-excel-file-with-simulated-data-as-a-template"></a>Crear un archivo de Excel con datos simulados como plantilla  
  
Los datos simulados también proporcionan una plantilla que representa con precisión los requisitos de datos de un diseño determinado de informes móviles.   
  
-  Haga clic en **Exportar todos los datos** en la esquina superior derecha de la vista de datos.   
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] genera un documento de Excel que contiene los datos simulados, lo que permite una rápida sustitución de los datos reales, que están listos para la importación.   
  
## <a name="how-simulated-data-behaves"></a>Comportamiento de los datos simulados  
  
Los datos simulados generados están diseñados específicamente para el informe móvil que se va a crear. A medida que coloca más elementos en la superficie de diseño, los datos simulados asociados aumentan y cambian para proporcionar la mejor experiencia posible sin datos reales. Esta evolución garantiza que los campos adicionales y las posibilidades de filtro estén disponibles en caso de que se agregue una serie adicional a las visualizaciones de gráficos o se amplíe el ámbito de uno o más elementos del informe móvil de otra forma.  
  
Como se ha mencionado anteriormente, puede exportar los datos simulados a un archivo de Excel y, de este modo, crear una plantilla de datos ideal para el informe móvil asociado. Puede incluir sus propios datos reales en el archivo de Excel y volver a importarlo al [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].   
  
Después de que todos los controles se enlacen a datos reales, las tablas simuladas que ya no se usen se quitarán automáticamente del informe móvil. No se pueden quitar tablas simuladas a las que todavía hagan referencia los elementos de la superficie de diseño.  
  
>**Nota**: Los datos simulados no se agregan a la superficie general del informe móvil porque no están serializados con el informe móvil, sino que se generan sobre la marcha en tiempo de ejecución.  
  
### <a name="see-also"></a>Vea también  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPad](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Ver [informes móviles y KPI de SQL Server en la aplicación de iPhone](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
  
  
  
  
  

