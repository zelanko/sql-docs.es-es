---
title: Elemento NotifyTableChange (XMLA) | Documentos de Microsoft
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
- NotifyTableChange Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 64779ceab6d83365755ed212a93685ee3f31837f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198982"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../xml-elements-properties/object-element-xmla.md), [TableNotifications](../xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El comando `NotifyTableChange` permite a una aplicación cliente notificar explícitamente a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que una o varias tablas de un origen de datos se han cambiado. En el almacenamiento en caché automático, esta notificación indica que los objetos OLAP relacionales (ROLAP) basados en esas tablas se deben revisar y actualizar.  
  
 Este método de notificación está indicado para objetos ROLAP basados en vistas o consultas con nombre definidas en una vista del origen de datos cuyos cambios pueden ser difíciles detectar y controlar.  
  
 El elemento `Object` debe hacer referencia a un origen de datos de la base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Si el elemento `Object` hace referencia a un objeto que no es una base de datos, se produce un error.  
  
 Para más información sobre almacenamiento en caché automático, vea [Almacenamiento en caché automático &#40;Particiones&#41;](../../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  