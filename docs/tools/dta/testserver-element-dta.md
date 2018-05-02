---
title: Elemento TestServer (DTA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- TestServer element
ms.assetid: caa3547a-2cd5-47ad-ace2-a36752835cfe
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70efce8b1aede11f3892b6c20c06fa6d1c143a43
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="testserver-element-dta"></a>TestServer (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Especifica el servidor de prueba que se va a utilizar al optimizar un servidor de producción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<TuningOptions>  
  <TestServer>...</TestServer>  
   ...code removed here...  
</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Se puede utilizar una vez por cada elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Reducir la carga de optimización del servidor de producción](../../relational-databases/performance/reduce-the-production-server-tuning-load.md).  
  
## <a name="see-also"></a>Ver también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
