---
title: Datos de informes de Reporting Services móviles | Microsoft Docs
description: Después de importar los datos en el Publicador de informes móviles de Microsoft SQL Server, el proceso de creación y diseño de informes para dispositivos móviles es el mismo, con independencia de si los datos proceden de archivos de Excel o de conjuntos de datos compartidos.
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 91138ef8-ddb4-4ac5-a1e4-fa4cf1c58dcc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3c022631d0f21c4e23756e39e4824fe9f52ef3b5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "79447863"
---
# <a name="data-for-reporting-services-mobile-reports"></a>Datos de informes de Reporting Services móviles
El modelo de datos del [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] es sencillo. Los datos se importan en el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] como una colección de conjuntos de datos. No son necesarias relaciones formales entre conjuntos de datos. Las búsquedas de un conjunto de datos a otro funcionarán siempre que coincidan los valores de clave. Las agregaciones de fecha y hora las controla el tiempo de ejecución de informe móvil y coincidirán entre diferentes conjuntos de datos, incluso si la granularidad de datos de fecha y hora es distinta entre los conjuntos de datos.   
  
Puede importar datos desde dos tipos de orígenes:   
  
* **Archivos de Excel locales**: seleccione un documento de Excel y seleccione las hojas de cálculo para importar. Después de la importación, los datos se almacenan en la definición de informe móvil. Para actualizar los datos del archivo original de Excel, use el comando **Actualizar datos** en la esquina superior derecha de la pestaña **Datos** de [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]. Obtenga más información sobre cómo [preparar datos de Excel para informes móviles de SSRS](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md).  
  
* **Conjuntos de datos compartidos del Publicador de informes móviles de SQL Server**: examine la lista de conjuntos de datos publicados en el servidor y seleccione los que quiera agregar al informe móvil. Los informes móviles basados en datos de servidor están siempre conectados a los conjuntos de datos de servidor originales y reflejan el estado más reciente de los datos en el servidor. Vea una [lista de los orígenes de datos admitidos](../report-data/data-sources-supported-by-reporting-services-ssrs.md).   
  
  Obtenga más información sobre cómo [obtener datos de conjuntos de datos compartidos en el Publicador de informes móviles](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md).  
  
Después de importar los datos en el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)], el resto de la experiencia de diseño y creación de informes móviles es igual, independientemente de dónde provengan los datos.   
  
## <a name="connect-mobile-report-elements-to-data"></a>Conectar elementos del informe móvil con datos ##  
  
Cada elemento del Publicador de informes móviles de SQL Server contiene uno o más valores de datos. Por ejemplo, el elemento Medidor radial contiene dos configuraciones de datos: Valor principal y Valor de comparación. Cada una de estas configuraciones apunta a exactamente un campo (columna) en un conjunto de datos específico.   
  
El tiempo de ejecución de informes móviles proporciona valores agregados para el medidor, según las selecciones del usuario. Tenga en cuenta que el valor de comparación de la misma instancia del medidor radial se puede enlazar a un campo de un conjunto de datos diferente.   
  
### <a name="see-also"></a>Consulte también  
-  [Preparación de datos para informes móviles de Reporting Services](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
- [Obtención de datos de conjuntos de datos compartidos](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md)
- [Conservar el formato de fecha para Analysis Services en los informes móviles](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 
  
  

