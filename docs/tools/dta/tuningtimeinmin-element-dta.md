---
title: Elemento TuningTimeInMin (DTA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
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
- TuningTimeInMin element
ms.assetid: 4973d9ac-20fd-4ac3-bc9f-5d60e39fdb7d
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c43e9a34f482f48bc8a565cd9f39cecb8249bc26
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="tuningtimeinmin-element-dta"></a>TuningTimeInMin (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica la duración máxima de una sesión de optimización en minutos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <TuningTimeInMin>...</TuningTimeInMin>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**unsignedInt**, longitud ilimitada.|  
|**Valor predeterminado**|480 minutos (8 horas).|  
|**Repetición**|Obligatoria a menos que se haya especificado un valor para el elemento **NumberOfEvents** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|None|  
  
## <a name="example"></a>Ejemplo  
  
## <a name="description"></a>Description  
 En el siguiente ejemplo de código se muestra cómo establecer un tiempo de optimización máximo de 12 horas:  
  
## <a name="code"></a>código  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <TuningTimeInMin>720</TuningTimeInMin>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>Ver también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
