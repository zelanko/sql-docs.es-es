---
title: Elemento Isolation (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Isolation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Isolation element
ms.assetid: 28c98c6f-668e-4547-8d25-127cc3995a7d
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a21593d360342dc703e1da45d50b4ddff74241a7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257231"
---
# <a name="isolation-element-assl"></a>Elemento Isolation (ASSL)
  Indica el nivel de aislamiento para un elemento que se deriva el [DataSource](../data-type/datasource-data-type-assl.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataSource>  
   ...  
   <Isolation>...</Isolation>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*ReadCommitted*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Origen de datos](../data-type/datasource-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*ReadCommitted*|Especifica que las instrucciones no pueden leer datos que hayan sido modificados, pero no confirmados, por otras transacciones. Esto evita las lecturas de datos sucios. Otras transacciones pueden cambiar los datos entre instrucciones individuales dentro de la transacción actual. Esto puede dar como resultado lecturas que no se pueden repetir o datos fantasma. Es el valor predeterminado para el elemento `Isolation`.|  
|*Snapshot*|Especifica que los datos leídos por cualquier instrucción de una transacción sean la versión coherente, desde el punto de vista transaccional, de los datos existentes al comienzo de la transacción. La transacción únicamente puede ver las modificaciones de datos confirmadas antes del comienzo de la misma. Las modificaciones de datos realizadas por otras transacciones después del inicio de la transacción actual no estarán visibles para las instrucciones que se estén ejecutando en la transacción actual. El efecto es el mismo que se obtendría si las instrucciones de una transacción obtuviesen una instantánea de los datos confirmados tal como se encontraban al comienzo de la transacción.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
