---
title: Elemento DataSourceView (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSourceView Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceView
- microsoft.xml.analysis.datasourceview
- urn:schemas-microsoft-com:xml-analysis#DataSourceView
helpviewer_keywords:
- DataSourceView element
ms.assetid: c4a4360f-7342-484b-bac1-0a247e8f279d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 299c6cd4c9eab4b982c294cffc8e728d14e4b2cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150335"
---
# <a name="datasourceview-element-xmla"></a>Elemento DataSourceView (XMLA)
  Contiene una vista del origen de datos fuera de línea de enlace para el elemento primario [Batch](../xml-elements-commands/batch-element-xmla.md) o [proceso](../xml-elements-commands/process-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Batch> <!-- or Process>  
...  
   <DataSourceView>  
      <DatabaseID>...</DatabaseID>  
      <DataSourceViewID>...</DataSourceViewID>  
   </DataSourceView>  
...  
</Batch>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Batch](../xml-elements-commands/batch-element-xmla.md), [Process](../xml-elements-commands/process-element-xmla.md)|  
|Elementos secundarios|[DatabaseID](id-element-xmla.md), [DataSourceViewID](../../scripting/properties/id-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El `DataSourceView` elemento representa un enlace fuera de línea a una vista del origen de datos, utilizado por el `Batch` o `Process` command to tempoarily override la vista del origen de datos de enlace de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos procesa el comando.  
  
 Para obtener más información sobre los enlaces fuera de línea, consulte [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
