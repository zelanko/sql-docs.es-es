---
title: OnlineIndexOperation (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 81a1d1762c0d78bce2d16113cc2bd290c7735219
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330845"
---
# <a name="onlineindexoperation-element-dta"></a>OnlineIndexOperation (DTA, elemento)
  Especifica si los índices, las vistas indizadas o las particiones recomendados por el Asistente para la optimización de motor de base de datos se pueden crear en línea.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, sin longitud máxima.|  
|**Valores permitidos**|**OFF**<br /> No se pueden crear en línea las estructuras recomendadas de diseño físico.<br /><br /> **ON**<br /> Se pueden crear en línea todas las estructuras recomendadas de diseño físico.<br /><br /> **MIXED**<br /> Siempre que es posible, el Asistente para la optimización de motor de base de datos intenta recomendar las estructuras de diseño físico que se pueden crear en línea.<br /><br /> Utilice uno de estos valores con este elemento. Si los índices se crean en línea, se anexa la palabra clave **ONLINE = ON** a la definición del objeto.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Si usa, sólo puede utilizarse una vez para el `TuningOptions` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions, elemento &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
