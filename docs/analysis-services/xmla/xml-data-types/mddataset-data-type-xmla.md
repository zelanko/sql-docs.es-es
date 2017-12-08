---
title: Tipo de datos MDDataSet Data (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDDataSet Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords: MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d6daeb5202c0f1078eabd1a5b820514b25de712c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="mddataset-data-type-xmla"></a>Tipo de datos MDDataSet Data (XMLA)
  Define un tipo de datos derivado que representa datos multidimensionales devueltos por la [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
 **Namespace** urn: schemas-microsoft-com-analysis: mddataset  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <OlapInfo>...</OlapInfo>  
   <Axes>...</Axes>  
   <CellData>...</CellData>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Conjunto de resultados](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Ejes](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md), [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md), [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Elementos derivados|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **MDDataSet** tipo de datos proporciona el orientado conjunto de filas (o conjunto de datos) necesarios para representar los datos OLAP en XML. El contenido de este conjunto de filas puede variar según los valores de la **contenido** y **formato** las propiedades incluidas en el [propiedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) colección de la  **Ejecutar** método. Para obtener más información sobre la **contenido** y **formato** propiedades, consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 Para obtener información básica sobre OLE DB para las estructuras de conjunto de datos de OLAP, vea el tema acerca de la asignación del tipo de datos MDDataSet a OLE DB en la especificación XML for Analysis 1.1. Para obtener un ejemplo de lenguaje (XSD) de definición de esquemas XML completo de la **MDDataSet** tipo de datos, consulte "Apéndice D: ejemplo de MDDataSet" de la especificación de XML for Analysis 1.1.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
