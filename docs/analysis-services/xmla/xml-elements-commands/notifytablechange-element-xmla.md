---
title: Elemento NotifyTableChange (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- NotifyTableChange Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 45e156076d7d97164fcb43674e3975daf6944e1e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="notifytablechange-element-xmla"></a>Elemento NotifyTableChange (XMLA)
  Notifica a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que se ha producido un cambio en las tablas de un origen de datos especificado.  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **NotifyTableChange** comando permite que una aplicación cliente notificar explícitamente a un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de instancia que una o varias tablas de un origen de datos que hayan cambiado. En el almacenamiento en caché automático, esta notificación indica que los objetos OLAP relacionales (ROLAP) basados en esas tablas se deben revisar y actualizar.  
  
 Este método de notificación está indicado para objetos ROLAP basados en vistas o consultas con nombre definidas en una vista del origen de datos cuyos cambios pueden ser difíciles detectar y controlar.  
  
 El **objeto** el elemento debe hacer referencia a un origen de datos en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos. Si el elemento **Object** hace referencia a un objeto que no es una base de datos, se produce un error.  
  
 Para más información sobre almacenamiento en caché automático, vea [Almacenamiento en caché automático &#40;Particiones&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
