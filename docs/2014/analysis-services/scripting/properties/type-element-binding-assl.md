---
title: Tipo de elemento (Binding) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Type Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: b5f5c485-dc83-4d66-a8d2-e96e96d068f9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 407c8e53a842baca13671256a8125b696d7f1e91
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225231"
---
# <a name="type-element-binding-assl"></a>Elemento Type (Binding) (ASSL)
  Contiene el tipo del enlace de atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Type>...</Type>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AttributeBinding](../data-type/binding-data-type-assl.md), [CubeAttributeBinding](../data-type/cubeattributebinding-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Todos*|Todos los niveles|  
|*Key*|Claves de miembro|  
|*Nombre*|Nombre del miembro|  
|*Value*|Valor de miembro|  
|*traducción*|Traducciones de miembro|  
|*UnaryOperator*|Operadores unarios|  
|*SkippedLevels*|Niveles omitidos|  
|*CustomRollup*|Fórmulas de resumen personalizado|  
|*CustomRollupProperties*|Propiedades de resumen personalizado|  
  
 Los elementos que corresponden a los elementos primarios de `Type` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.AttributeBinding> y <xref:Microsoft.AnalysisServices.CubeAttributeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos Binding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
