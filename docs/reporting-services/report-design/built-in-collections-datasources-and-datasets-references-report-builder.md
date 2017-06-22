---
title: "Orígenes de datos y las referencias de colección de conjuntos de datos (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a1e556a8c6ac712d61d262c4d96993a9ab3ecf11
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="built-in-collections---datasources-and-datasets-references-report-builder"></a>Colecciones integradas: orígenes de datos y las referencias de los conjuntos de datos (generador de informes)
  La colección **DataSources** representa todos los orígenes de datos usados en un informe. De igual forma, la colección **DataSets** representa todos los conjuntos de datos de todos los orígenes de datos existentes en un informe. Use el panel **Datos de informe** para obtener acceso a una vista jerárquica en la que aparezcan los conjuntos de datos de informe organizados debajo del origen de datos al que hacen referencia. Si incluye referencias a estas colecciones, no verá los valores cuando obtenga acceso a una vista previa del informe. Estas colecciones solo están disponibles una vez publicado el informe en un servidor de informes.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 La colección **DataSources** representa los orígenes de datos a los que se hace referencia en una definición de informe publicado. Puede decidir incluir esta información en el informe para documentar el origen de los datos de informe. Esta colección no está disponible en el modo **Vista previa** . En la siguiente tabla, se describen las variables de la colección **DataSources** .  
  
|**Variable**|**Tipo**|**Description**|  
|------------------|--------------|---------------------|  
|**DataSourceReference**|**String**|Ruta de acceso completa de la definición de origen de datos en el servidor de informes. Por ejemplo, puede incluir una lista de todos los orígenes de datos que usó un informe como parte de un historial de informes. En el ejemplo siguiente se muestra la ruta de acceso completa del origen de datos denominado AdventureWorks2012:<br /><br /> `/DataSources/AdventureWorks2012`.|  
|**Tipo**|**String**|Tipo de proveedor de datos para el origen de datos. Por ejemplo, `SQL`.|  
  
## <a name="datasets"></a>DataSets  
 La colección **DataSets** representa los conjuntos de datos a los que se hace referencia en una definición de informe. Puede decidir incluir la consulta en el informe en un cuadro de texto, de modo que un usuario que esté interesado en saber exactamente qué datos están en el informe pueda ver el texto del comando original. Esta colección no está disponible en el modo **Vista previa** . En la siguiente tabla, se describen los miembros de la colección **DataSets** .  
  
|**Miembro**|**Tipo**|**Description**|  
|----------------|--------------|---------------------|  
|**CommandText**|**String**|Para los orígenes de datos de base de datos, ésta es la consulta que se utiliza para recuperar datos del origen de datos. Si la consulta es una expresión, ésta es la expresión evaluada.|  
|**RewrittenCommandText**|**String**|El valor CommandText expandido del proveedor de datos. Se utiliza normalmente en informes con parámetros de consulta que se asignan a parámetros de informe. El proveedor de datos establece esta propiedad al expandir las referencias de los parámetros de texto de comando a los valores constantes seleccionados para los parámetros de informe asignados.|  
  
### <a name="using-query-expressions"></a>Usar expresiones de consulta  
 Puede usar expresiones de consulta para definir la consulta contenida en un conjunto de datos. Puede usar esta característica para diseñar informes cuyas consultas cambien en función de la información facilitada por el usuario, de los datos de otros conjuntos de datos o de otras variables. Para más información sobre consultas, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
