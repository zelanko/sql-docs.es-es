---
title: KeepExisting (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8691e57b9750447b1740c79337b75500febd9549
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070745"
---
# <a name="keepexisting-element-dta"></a>KeepExisting (DTA, elemento)
  Especifica las estructuras de diseño físico (índices, vistas indizadas o particiones) que el Asistente para la optimización de motor de base de datos debe conservar al generar su recomendación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, límite de longitud aplicado por el servidor.|  
|**Valores permitidos**|**NONE**<br /> Ninguna estructura existente.<br /><br /> **ALL**<br /> Todas las estructuras existentes.<br /><br /> **ALIGNED**<br /> Todas las estructuras alineadas de partición.<br /><br /> **CL_IDX**<br /> Todos los clúster de las tablas.<br /><br /> **IDX**<br /> Todos los índices clúster y no clúster de las tablas.<br /><br /> Utilice solo uno de estos valores con este elemento.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Puede utilizar una sola vez por cada `TuningOptions` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions, elemento &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
