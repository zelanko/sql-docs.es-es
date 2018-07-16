---
title: Type (elemento) (MiningStructureColumn) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (MiningStructureColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30ce9327fb28e9f452e643ded604f2a8dd72a084
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304245"
---
# <a name="type-element-miningstructurecolumn-assl"></a>Elemento Type (MiningStructureColumn) (ASSL)
  Contiene el tipo de la [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Long*|Entero de 64 bits con signo. Este tipo de datos se asigna a la `Int64` tipo de datos en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipo de .NET Framework y los datos DBTYPE_I8 en OLE DB.|  
|*Boolean*|Valor booleano. Este tipo de datos se asigna al tipo de datos `Boolean` en .NET Framework y al tipo de datos DBTYPE_BOOL en OLE DB.|  
|*Texto*|Flujo de caracteres Unicode terminado en NULL. Este tipo de datos se asigna al tipo de datos `String` en .NET Framework y al tipo de datos DBTYPE_WSTR en OLE DB.|  
|*Doble*|Número de punto flotante de precisión doble del intervalo -1.79E +308 a 1.79E +308. Este tipo de datos se asigna al tipo de datos `Double` en .NET Framework y al tipo de datos DBTYPE_R8 en OLE DB.|  
|*Date*|Fecha de los datos, almacenada como un número de punto flotante de precisión doble. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción del día. Este tipo de datos se asigna al tipo de datos `DateTime` en .NET Framework y al tipo de datos DBTYPE_DATE en OLE DB.|  
|*Table*|Tabla anidada. Este tipo de datos se asigna al tipo de datos de DBTYPE_HCHAPTER en OLE DB. **Nota:** columnas de tabla en .NET Framework no tienen un tipo de datos intrínseco equivalente, pero en su lugar, son compatibles con el `DataReader` clase.|  
  
 La enumeración que corresponde a los valores permitidos para `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>.  
  
 El elemento que se corresponde con el elemento primario de `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
