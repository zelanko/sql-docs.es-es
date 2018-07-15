---
title: DropOnlyMode (DTA, elemento) | Microsoft Docs
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
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bb4fae568cb1301d1407a2694f6a2e527b0b4243
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247795"
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode (DTA, elemento)
  Especifica que el Asistente para la optimización de motor de base de datos solo debe quitar índices, vistas indizadas o particiones ya existentes durante la sesión de optimización. Cuando se especifica esta opción de optimización, no se consideran nuevas estructuras de diseño físico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Puede utilizar una sola vez por cada `TuningOptions` elemento. No se puede usar si se especifican los siguientes elementos en el `TuningOptions` elemento:<br /><br /> [FeatureSet, elemento &#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Creación de particiones elemento &#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [KeepExisting &#40;DTA, elemento&#41;](keepexisting-element-dta.md) se establece en **ALL**|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions, elemento &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente se muestra el `TuningOptions` sección de un archivo de entrada XML del Asesor de optimización de motor de base de datos donde el `DropOnlyMode` se especifica. En este ejemplo, la hora de optimización se limita a 24 horas (1440 minutos) y se considerará la eliminación de todos los clúster y no clúster existentes:  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
