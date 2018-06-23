---
title: Tipo de elemento (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 38b4442afe95f06d9a6f437e906c01b7386d91ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111638"
---
# <a name="type-element-xmla"></a>Elemento Type (XMLA)
  Determina el tipo de procesamiento que debe realizar la [proceso](../xml-elements-commands/process-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Procesar](../xml-elements-commands/process-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información acerca del procesamiento de las opciones disponibles en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [procesamiento del objeto de modelo multidimensionales](../../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 El valor del elemento `Type` se limita a las cadenas listadas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*ProcessFull*|Quita todos los datos del objeto afectado y después lo procesa.|  
|*ProcessAdd*|Agrega nuevos datos al objeto afectado.|  
|*ProcessUpdate*|Actualiza los datos el objeto afectado.|  
|*ProcessIndexes*|Crea o vuelve a generar índices y agregaciones en el objeto afectado.|  
|*ProcessScriptCache*|Si se procesa el cubo, el servidor volverá a generar la caché de script de MDX. Si no, se producirá un error.<br /><br /> **Tenga en cuenta** se aplica solo al cubo.|  
|*ProcessData*|Procesa los datos sólo en el objeto afectado.|  
|*ProcessDefault*|Detecta el estado del objeto afectado y después ejecuta la opción de procesamiento adecuada en el objeto afectado para optimizarlo y volver a dejarlo en un estado totalmente procesado.|  
|*ProcessClear*|Quita los datos del objeto afectado y todos los objetos relacionados.|  
|*ProcessStructure*|Únicamente procesa los datos del objeto afectado.|  
|*ProcessClearStructureOnly*|Borra los datos únicamente del objeto afectado.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  