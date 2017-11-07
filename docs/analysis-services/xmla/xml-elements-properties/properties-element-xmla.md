---
title: Elemento Properties (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Properties Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Properties
- microsoft.xml.analysis.properties
- urn:schemas-microsoft-com:xml-analysis#Properties
- Properties
helpviewer_keywords:
- Properties element
ms.assetid: 0b5468e5-bf23-4d22-862f-72e27a9fff2f
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 77029875d3c2e84c1b48c4e1e5454f735f5a2752
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="properties-element-xmla"></a>Elemento Properties (XMLA)
  Contiene el XML de propiedades de Analysis (XMAL) utilizadas por la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) y [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) métodos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Discover> <!-- or Execute -->  
...  
   <Properties>  
      <PropertyList>...</PropertyList>  
   </Properties>  
...  
</Discover>  
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
|Elementos primarios|[Detectar](../../../analysis-services/xmla/xml-elements-methods-discover.md), [ejecutar](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|Elementos secundarios|[PropertyList](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **propiedades** elemento representa propiedades XMLA usadas para controlar aspectos de la **Discover** y **Execute** métodos, como definir la información necesaria para conectarse al origen de datos, especificando el formato de devolución del conjunto de resultados o especificando la configuración regional en la que se deben dar formato a los datos.  
  
 Las propiedades disponibles y sus valores se pueden obtener utilizando el tipo de solicitud DISCOVER_PROPERTIES con el método **Discover** .  
  
## <a name="example"></a>Ejemplo  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

