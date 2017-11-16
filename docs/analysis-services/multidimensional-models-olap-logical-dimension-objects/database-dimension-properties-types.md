---
title: "Tipos de dimensión | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5fa77532b4c674c4b5035cf6b591b973008ae6e5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="database-dimension-properties---types"></a>Propiedades de dimensión de base de datos: tipos
  El **tipo** configuración de la propiedad proporciona información sobre el contenido de una dimensión a las aplicaciones cliente y servidor. En algunos casos, el **tipo** configuración solo se proporcionan instrucciones para las aplicaciones cliente y es opcional. En otros casos, como **cuentas** o **tiempo** dimensiones, el **tipo** la configuración de propiedad de la dimensión y sus atributos determina comportamientos específicos basados en servidor y puede ser necesario implementar ciertos comportamientos en el cubo. Por ejemplo, el **tipo** propiedad de una dimensión se puede establecer en **cuentas** para indicar a las aplicaciones cliente que la dimensión estándar contiene atributos de cuenta. Para obtener más información sobre el tiempo, cuenta y las dimensiones de moneda, vea [crear una dimensión de tipo de fecha](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [crear una cuenta financiera de dimensión de tipo de elementos primarios y secundarios](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), y [crear una divisa tipo de dimensión](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 La configuración predeterminada para el tipo de dimensión es **Regular**, que no hace suposiciones sobre el contenido de la dimensión. Esta es la configuración predeterminada para todas las dimensiones al definir inicialmente una dimensión a menos que especifique **tiempo** al definir la dimensión mediante el Asistente para dimensiones. También se debe dejar **Regular** como el tipo de dimensión si el Asistente para dimensiones no muestra un tipo adecuado para el tipo de dimensión.  
  
## <a name="available-dimension-types"></a>Tipos de dimensiones disponibles  
 La tabla siguiente describen los tipos de dimensiones disponibles en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Tipo de dimensión|Description|  
|--------------------|-----------------|  
|Regular|Dimensión cuyo tipo no se ha establecido en un tipo de dimensión especial.|  
|Time|Dimensión cuyos atributos representan periodos de tiempo, como años, semestres, trimestres, meses y días.|  
|Organización|Dimensión cuyos atributos representan información organizativa, como empleados o subsidiarias.|  
|Geografía|Dimensión cuyos atributos representan información geográfica, como ciudades o códigos postales.|  
|Lista de materiales|Dimensión cuyos atributos representan información de inventario o de fabricación, como listas de piezas para productos.|  
|Cuentas|Dimensión cuyos atributos representan un gráfico de cuentas para la elaboración de informes financieros.|  
|Clientes|Dimensión cuyos atributos representan información de clientes o de contacto.|  
|Productos|Dimensión cuyos atributos representan información de productos.|  
|Escenario|Dimensión cuyos atributos representan información de planeación o análisis estratégico.|  
|Cuantitativo|Dimensión cuyos atributos representan información cuantitativa.|  
|Utilidad|Dimensión cuyos atributos representan información diversa.|  
|Moneda|Este tipo de dimensión contiene datos de moneda y metadatos.|  
|Tarifas|Dimensión cuyos atributos representan información de tasa de cambio.|  
|Canal|Dimensión cuyos atributos representan información de canal.|  
|Promoción|Dimensión cuyos atributos representan información de promociones de marketing.|  
  
## <a name="see-also"></a>Vea también  
 [Crear una dimensión mediante el uso de una tabla existente](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  

