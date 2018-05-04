---
title: Elemento HierarchyInfo (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- HierarchyInfo Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#HierarchyInfo
- microsoft.xml.analysis.hierarchyinfo
- urn:schemas-microsoft-com:xml-analysis#HierarchyInfo
helpviewer_keywords:
- HierarchyInfo element
ms.assetid: b4472251-1f1d-4233-a8e6-407397862ab4
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1732502650534b655eb48236c8a96857fc265748
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchyinfo-element-xmla"></a>Elemento HierarchyInfo (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Representa una jerarquía única que se encuentra en un elemento [AxisInfo](../../../analysis-services/xmla/xml-elements-properties/axisinfo-element-xmla.md) primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AxisInfo>  
   ...  
   <HierarchyInfo name="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </HierarchyInfo>  
   ...  
</AxisInfo>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AxisInfo](../../../analysis-services/xmla/xml-elements-properties/axisinfo-element-xmla.md)|  
|Elementos secundarios|[Caption](../../../analysis-services/xmla/xml-elements-properties/caption-element-xmla.md), [DisplayInfo](../../../analysis-services/xmla/xml-elements-properties/displayinfo-element-xmla.md), [LName](../../../analysis-services/xmla/xml-elements-properties/lname-element-xmla.md), [LNum](../../../analysis-services/xmla/xml-elements-properties/lnum-element-xmla.md), [UName](../../../analysis-services/xmla/xml-elements-properties/uname-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Description|  
|---------------|-----------------|  
|Nombre|Atributo **String** requerido. Es el nombre de la jerarquía.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
