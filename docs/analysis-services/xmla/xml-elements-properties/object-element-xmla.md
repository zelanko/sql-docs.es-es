---
title: Objeto de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9ef2f645895e567d69d06e4e1383e0c477b6ed1
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575917"
---
# <a name="object-element-xmla"></a>Elemento Object (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una referencia de objeto usada por el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Alter> <!-- or any of the parent elements in the Element relationships table -->  
...  
   <Object>  
      <!-- One or more object identifiers, depending on the parent element -->  
   </Object>  
...  
</Alter>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Cardinalidad|  
|------------------------|-----------------|  
|[ALTER](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
|Todos las demás|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[ALTER](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md), [eliminar](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [proceso](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [suscribirse](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|Elementos secundarios|Elementos requeridos de Analysis Services Scripting Language (ASSL). Especifica enumerando los elementos de Id. del objeto y sus antecesores (excepto la **Server** objeto.) Por ejemplo, la siguiente **objeto** elemento identifica una partición:<br /><br /> `<Object>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</Object>`|  
  
## <a name="remarks"></a>Notas  
 El orden en el que los identificadores aparecen no es importante.  
  
 Para **Alter** elementos, la instancia de Analysis Services se utiliza como el objeto predeterminado si el **objeto** no se especifica el elemento.  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
