---
title: Elemento RootMemberIf (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- RootMemberIf Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c5a3a75efa13710bcc00a94ed55cee407dbbbc8d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="rootmemberif-element-assl"></a>Elemento RootMemberIf (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina cómo se identifican el miembro raíz o los miembros de un atributo primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <RootMemberIf>...</RootMemberIf>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*ParentIsBlankSelfOrMissing*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la **RootMemberIf** elemento se utiliza únicamente por los atributos primarios (en otras palabras, el valor de la [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento de la **DimensionAttribute** es el elemento primario establecido en *primario*) para determinar los miembros raíz (superiores) de una jerarquía de elementos primarios y secundarios.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|Solo los miembros que cumplen una o varias de las condiciones descritas para *ParentIsBlank*, *ParentIsSelf*, o *ParentIsMissing* se tratan como miembros raíz.|  
|*ParentIsBlank*|Solo los miembros con un valor null, cero o una cadena vacía en las columnas de clave representadas por la [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) colección de **DimensionAttribute** se tratan como miembros raíz.|  
|*ParentIsSelf*|Únicamente los miembros que son elementos primarios se tratan como miembros raíz.|  
|*ParentIsMissing*|Únicamente los miembros cuyos elementos primarios no se pueden encontrar se tratan como miembros raíz.|  
  
 La enumeración que corresponde a los valores permitidos para **RootMemberIf** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.RootIfValue>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
