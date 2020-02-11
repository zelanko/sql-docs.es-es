---
title: Tipos de dimensión | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbe1c8932c082ce537cd5dc3f2b12d98c05c3811
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62728561"
---
# <a name="dimension-types"></a>Tipos de dimensiones
  El valor de la propiedad `Type` proporciona información acerca del contenido de una dimensión al servidor y a las aplicaciones cliente. En algunos casos, el valor de `Type` solo constituye una guía para las aplicaciones cliente y es opcional. En otros casos, como en las dimensiones `Accounts` o `Time`, la configuración de la propiedad `Type` para la dimensión y sus atributos determina comportamientos específicos basados en el servidor y puede que sea necesario implementar ciertos comportamientos en el cubo. Por ejemplo, la propiedad `Type` de una dimensión se puede establecer en `Accounts` para indicar a las aplicaciones cliente que la dimensión estándar contiene atributos de cuenta. Para obtener más información sobre las dimensiones de tiempo, cuenta y moneda, vea [crear una dimensión de tipo de fecha](../multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [crear una cuenta de Finanzas de una dimensión de tipo primario-secundario](../multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)y [crear una dimensión de tipo moneda](../multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 El valor predeterminado para el tipo de dimensión es `Regular`, que no realiza suposiciones acerca del contenido de la dimensión. Se trata del valor predeterminado para todas las dimensiones al definir inicialmente una dimensión, a menos que se especifique `Time` al definir la dimensión mediante el Asistente para Dimensiones. También se debe dejar `Regular` como tipo de dimensión si el Asistente para dimensiones no muestra un tipo adecuado para el tipo de dimensión.  
  
## <a name="available-dimension-types"></a>Tipos de dimensiones disponibles  
 En la tabla siguiente se describen los tipos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]dimensiones disponibles en.  
  
|Tipo de dimensión|Descripción|  
|--------------------|-----------------|  
|Regular |Dimensión cuyo tipo no se ha establecido en un tipo de dimensión especial.|  
|Time|Dimensión cuyos atributos representan periodos de tiempo, como años, semestres, trimestres, meses y días.|  
|Organización|Dimensión cuyos atributos representan información organizativa, como empleados o subsidiarias.|  
|Geography|Dimensión cuyos atributos representan información geográfica, como ciudades o códigos postales.|  
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
  
## <a name="see-also"></a>Consulte también  
 [Crear una dimensión usando una tabla existente](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensiones &#40;Analysis Services de datos multidimensionales&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
