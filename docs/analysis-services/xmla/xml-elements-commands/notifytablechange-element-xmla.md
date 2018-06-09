---
title: Elemento NotifyTableChange (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 049756318b4d0e14b0bd2fe858d7a2153673cfd5
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575007"
---
# <a name="notifytablechange-element-xmla"></a>Elemento NotifyTableChange (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Notifica a una instancia de Analysis Services que se ha producido un cambio en las tablas de un origen de datos especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <NotifyTableChange>  
      <Object>...</Object>  
      <TableNotifications>...</TableNotifications>  
   </NotifyTableChange>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El **NotifyTableChange** comando permite que una aplicación cliente notificar explícitamente a un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de instancia que una o varias tablas de un origen de datos que hayan cambiado. En el almacenamiento en caché automático, esta notificación indica que los objetos OLAP relacionales (ROLAP) basados en esas tablas se deben revisar y actualizar.  
  
 Este método de notificación está indicado para objetos ROLAP basados en vistas o consultas con nombre definidas en una vista del origen de datos cuyos cambios pueden ser difíciles detectar y controlar.  
  
 El **objeto** el elemento debe hacer referencia a un origen de datos en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos. Si el elemento **Object** hace referencia a un objeto que no es una base de datos, se produce un error.  
  
 Para más información sobre almacenamiento en caché automático, vea [Almacenamiento en caché automático &#40;Particiones&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="see-also"></a>Vea también
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
