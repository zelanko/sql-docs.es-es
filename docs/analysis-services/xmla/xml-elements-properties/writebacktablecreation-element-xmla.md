---
title: Elemento WritebackTableCreation (XMLA) | Documentos de Microsoft
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
apiname: WritebackTableCreation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#WritebackTableCreation
- microsoft.xml.analysis.writebacktablecreation
- http://schemas.microsoft.com/analysisservices/2003/engine#WritebackTableCreation
helpviewer_keywords: WritebackTableCreation element
ms.assetid: e9579d63-e28c-4d4e-9f4a-21c5da24c276
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cc68c8d4d4a3cf02995a2effb8d523fc7b3ce722
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="writebacktablecreation-element-xmla"></a>Elemento WritebackTableCreation (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Determina si una tabla de reescritura se crea durante la [proceso](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) operación.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Procesar](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de las opciones de procesamiento disponibles para los objetos en una instancia de Analysis Services, consulte [procesar un modelo multidimensional &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 El valor del elemento **WritebackTableCreation** se limita a las cadenas listadas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Crear*|Crear crea una nueva tabla de reescritura si no existe una. Se produce un error si la tabla de reescritura ya existe.|  
|*CreateAlways*|Cree una nueva tabla de reescritura, sobrescribiendo cualquier tabla de reescritura existente.|  
|*UseExisting*|Utilice la tabla de reescritura existente, si ya existe una. Si no existe una, se produce un error.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
