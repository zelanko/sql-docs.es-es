---
title: Elemento RequestType (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63c1a838d74745b5ef51f73b51e34c95e08a81ff
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994797"
---
# <a name="requesttype-element-xmla"></a>Elemento RequestType (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Determina el tipo de metadatos devueltos por la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Discover>  
   ...  
   <RequestType>...</RequestType>  
   ...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Detectar](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **RequestType** elemento determina el conjunto de filas de esquema desde el que el **Discover** método devuelve los datos. Esta enumeración se limita a los nombres de los conjuntos de filas de esquema admitidas por Analysis Services. Para obtener más información acerca de los conjuntos de filas de esquema, vea [conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md).  
  
> [!NOTE]  
>  El **RequestType** elemento enumera solo los nombres de conjunto de filas de esquema. Si se utiliza el GUID de conjunto de filas de esquema, se produce un error.  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
