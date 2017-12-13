---
title: Objeto de elemento (Dimension) (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Object Element (Dimension)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Object
- urn:schemas-microsoft-com:xml-analysis#Object
- microsoft.xml.analysis.object
helpviewer_keywords: Object element
ms.assetid: db7feb39-7cc1-4b54-8979-77ce402ef71f
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3f4e836439433d9e3bf17f55f70b637f6f80d649
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="object-element-dimension-xmla"></a>Elemento Object (Dimension) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene una referencia de objeto para la dimensión en la que el elemento primario [insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), o [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) se ejecuta el comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Insert> <!-- or any of the parent elements in the Element Relationships table -->  
...  
   <Object>  
      <Database>...</Database>  
      <Cube>...</Cube>  
      <Dimension>...</Dimension>  
   </Object>  
...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Quitar](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|Elementos secundarios|[Cubo](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md), [base de datos](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md), [dimensión](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
