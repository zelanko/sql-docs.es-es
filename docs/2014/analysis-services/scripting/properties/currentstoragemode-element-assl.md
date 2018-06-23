---
title: Elemento CurrentStorageMode (ASSL) | Documentos de Microsoft
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
- CurrentStorageMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CurrentStorageMode
helpviewer_keywords:
- CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cce7bfd399c0c986a79e919c6227ee604e9ff470
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111229"
---
# <a name="currentstoragemode-element-assl"></a>Elemento CurrentStorageMode (ASSL)
  Determina el modo de almacenamiento actual para el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*ROLAP*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una vez o nunca.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Dimensión](../objects/dimension-element-assl.md), [partición](../objects/partition-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento `CurrentStorageMode` indica el modo de almacenamiento actualmente en uso para los propósitos de almacenamiento en caché automático y se aplica a todos los atributos del elemento principal.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*MOLAP*|El elemento primario usa el almacenamiento OLAP multidimensional (MOLAP).|  
|*ROLAP*|El elemento primario usa el almacenamiento OLAP relacional (ROLAP).|  
|*HOLAP*|El elemento primario usa el almacenamiento OLAP híbrido (HOLAP). **Nota:** este valor solo es válido para [partición](../objects/partition-element-assl.md) elementos primarios.|  
  
 La enumeración que corresponde a los valores permitidos de `CurrentStorageMode` en el modelo de objetos de Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.StorageMode>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  