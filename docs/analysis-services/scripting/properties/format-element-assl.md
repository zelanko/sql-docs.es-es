---
title: Dar formato a elementos (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Format Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Format
helpviewer_keywords: Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 01d1202f5868d5d81318d18e4f43856f3a790077
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="format-element-assl"></a>Elemento Format (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contiene el formato requerido de la [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Elemento de datos](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Los valores permitidos para el elemento **Format** son los formatos de Microsoft Office Excel, así como las cadenas *TrimRight*, *TrimLeft*, *TrimAll*y *TrimNone*. *TrimRight* es el valor predeterminado para el proceso de recorte.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Cualquier cadena de formato de Excel|Se da formato a los datos de acuerdo con la cadena de formato con nombre o personalizada que se haya especificado. Es posible especificar cualquier cadena de formato que admita Excel.|  
|*TrimAll*|Los datos se recortan por la izquierda y por la derecha.|  
|*TrimLeft*|Los datos se recortan por la izquierda.|  
|*TrimNone*|No se recortan los datos.|  
|*TrimRight*|Los datos se recortan por la derecha.|  
  
 El elemento que corresponde al elemento primario de **formato** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
