---
title: Elemento WritebackTableCreation (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- WritebackTableCreation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#WritebackTableCreation
- microsoft.xml.analysis.writebacktablecreation
- http://schemas.microsoft.com/analysisservices/2003/engine#WritebackTableCreation
helpviewer_keywords:
- WritebackTableCreation element
ms.assetid: e9579d63-e28c-4d4e-9f4a-21c5da24c276
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9908cf615ef5f767b72e639023b0444f02e71f7a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319215"
---
# <a name="writebacktablecreation-element-xmla"></a>Elemento WritebackTableCreation (XMLA)
  Determina si una tabla de reescritura se crea durante la [proceso](../xml-elements-commands/process-element-xmla.md) operación.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Procesar](../xml-elements-commands/process-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información acerca de las opciones de procesamiento disponibles para los objetos en una instancia de Analysis Services, consulte [procesamiento del objeto de modelo Multidimensional](../../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 El valor del elemento `WritebackTableCreation` se limita a las cadenas listadas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Crear*|Crear crea una nueva tabla de reescritura si no existe una. Se produce un error si la tabla de reescritura ya existe.|  
|*CreateAlways*|Cree una nueva tabla de reescritura, sobrescribiendo cualquier tabla de reescritura existente.|  
|*UseExisting*|Utilice la tabla de reescritura existente, si ya existe una. Si no existe una, se produce un error.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
