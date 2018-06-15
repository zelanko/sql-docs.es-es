---
title: Elemento Isolation (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b8233ce2fc5d987dac6511fee978e45b213601a2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030916"
---
# <a name="isolation-element-assl"></a>Elemento Isolation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Indica el nivel de aislamiento para un elemento que se deriva de la [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*ReadCommitted*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Origen de datos](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Value|Description|  
|-----------|-----------------|  
|*ReadCommitted*|Especifica que las instrucciones no pueden leer datos que hayan sido modificados, pero no confirmados, por otras transacciones. Esto evita las lecturas de datos sucios. Otras transacciones pueden cambiar los datos entre instrucciones individuales dentro de la transacción actual. Esto puede dar como resultado lecturas que no se pueden repetir o datos fantasma. Es el valor predeterminado para el elemento **Isolation** .|  
|*Snapshot*|Especifica que los datos leídos por cualquier instrucción de una transacción sean la versión coherente, desde el punto de vista transaccional, de los datos existentes al comienzo de la transacción. La transacción únicamente puede ver las modificaciones de datos confirmadas antes del comienzo de la misma. Las modificaciones de datos realizadas por otras transacciones después del inicio de la transacción actual no estarán visibles para las instrucciones que se estén ejecutando en la transacción actual. El efecto es el mismo que se obtendría si las instrucciones de una transacción obtuviesen una instantánea de los datos confirmados tal como se encontraban al comienzo de la transacción.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
