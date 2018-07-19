---
title: Elemento UnknownMemberName (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d744357078e4cfaa73fe3170dba8f1321313efad
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050583"
---
# <a name="unknownmembername-element-assl"></a>Elemento UnknownMemberName (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene el título, en el idioma predeterminado de la dimensión, del miembro desconocido de la dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMemberName>...</UnknownMemberName>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|*Unknown*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor del elemento **UnknownMemberName** proporciona el título que se utiliza para el miembro desconocido. El identificador de miembro del miembro desconocido es *Dimension*.UnknownMember, donde *Dimension* es el nombre único de la dimensión, y no se puede cambiar.  
  
 El elemento que se corresponde con el elemento primario de **UnknownMemberName** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
