---
title: Elemento root (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 794e33d6270ef9540396fd7d2f38a08ccab4c8d2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34578137"
---
# <a name="root-element-xmla"></a>Elemento root (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene un resultado devuelto por la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método o un comando XML for Analysis (XMLA) ejecutado utilizando el [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Vea la tabla siguiente.|  
|Valor predeterminado|None|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
|Ancestor|Tipo de datos|  
|--------------|---------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[Conjunto de filas](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md), [conjunto de filas](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[resultados](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md), [devolver](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **raíz** elemento contiene la información devuelta en el [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) elemento devuelto por una sola **Discover** llamada al método, o en la [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) elemento devuelto por un comando XMLA único ejecutado por un único **Execute** llamada al método.  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
