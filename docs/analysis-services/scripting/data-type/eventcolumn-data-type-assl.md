---
title: Tipo de datos EventColumn (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe9daba9906a3bc65bfd33e87f07ef55615734cb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="eventcolumn-data-type-assl"></a>Tipo de datos EventColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo que representa una columna de información que se va a capturar para un elemento [Event](../../../analysis-services/scripting/objects/event-element-assl.md) como parte de un elemento [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|  
|Elementos derivados|[Columna](../../../analysis-services/scripting/objects/column-element-assl.md) ([columnas](../../../analysis-services/scripting/collections/columns-element-assl.md) colección de [seguimiento](../../../analysis-services/scripting/objects/trace-element-assl.md))|  
  
## <a name="see-also"></a>Vea también  
 [Elemento Events &#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
