---
title: Tipo de elemento (MiningStructureColumn) (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (MiningStructureColumn)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1fbc9ce30cd9f436a3bce1d96e532d6264b08a2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-miningstructurecolumn-assl"></a>Elemento Type (MiningStructureColumn) (ASSL)
  Contiene el tipo de la [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Long*|Entero de 64 bits con signo. Este tipo de datos se asigna a la **Int64** tipo de datos en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipo de .NET Framework y los datos DBTYPE_I8 en OLE DB.|  
|*Boolean*|Valor booleano. Este tipo de datos se asigna a la **booleano** tipo de datos de .NET Framework y el tipo de datos DBTYPE_BOOL en OLE DB.|  
|*Texto*|Flujo de caracteres Unicode terminado en NULL. Este tipo de datos se asigna a la **cadena** tipo de datos de .NET Framework y el tipo de datos DBTYPE_WSTR en OLE DB.|  
|*Doble*|Número de punto flotante de precisión doble del intervalo -1.79E +308 a 1.79E +308. Este tipo de datos se asigna a la **doble** tipo de datos de .NET Framework y el tipo de datos DBTYPE_R8 en OLE DB.|  
|*Date*|Fecha de los datos, almacenada como un número de punto flotante de precisión doble. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción del día. Este tipo de datos se asigna a la **DateTime** tipo de datos de .NET Framework y el tipo de datos DBTYPE_DATE en OLE DB.|  
|*Table*|Tabla anidada. Este tipo de datos se asigna al tipo de datos de DBTYPE_HCHAPTER en OLE DB.<br /><br /> Nota: Las columnas de tabla en .NET Framework no tienen un tipo de datos intrínseco equivalente, pero en su lugar, son compatibles con el **DataReader** clase.|  
  
 La enumeración que corresponde a los valores permitidos para **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>.  
  
 El elemento que corresponde al elemento primario de **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

