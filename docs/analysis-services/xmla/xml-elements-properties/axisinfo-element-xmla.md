---
title: Elemento AxisInfo (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AxisInfo Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AxisInfo
- microsoft.xml.analysis.axisinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#AxisInfo
helpviewer_keywords:
- AxisInfo element
ms.assetid: 060741db-b2ec-4174-9277-58d996440a88
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e28ea0859b689cec5d1ebeae987fdf55dc768205
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="axisinfo-element-xmla"></a>Elemento AxisInfo (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Representa los metadatos de un solo eje contenido por el elemento primario [AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AxesInfo>  
   ...  
   <AxisInfo name="string">  
      <HierarchyInfo>...</HierarchyInfo>  
   </AxisInfo>  
   ...  
</AxesInfo>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md)|  
|Elementos secundarios|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Description|  
|---------------|-----------------|  
|Nombre|Atributo **String** requerido. El nombre del eje.|  
  
## <a name="remarks"></a>Comentarios  
 En un **raíz** elemento que usa el **MDDataSet** objeto, un **AxisInfo** elemento contiene una colección de **HierarchyInfo** elementos que , combinado con el valor de la **nombre** atributo, representa la definición de un eje único devuelto en el conjunto de datos multidimensional.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
