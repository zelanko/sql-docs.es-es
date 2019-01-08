---
title: Creación de particiones de elemento (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: acf6d033595952186b411ef0e547858f8b59771b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769347"
---
# <a name="partitioning-element-dta"></a>Partitioning (DTA, elemento)
  Contiene el esquema de particiones que se desea que utilice el Asistente para la optimización de motor de base de datos durante el análisis.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, sin longitud máxima.|  
|**Valores permitidos**|**NONE**<br /> Ninguna partición.<br /><br /> **FULL**<br /> Partición total. (Mejora el rendimiento).<br /><br /> **ALIGNED**<br /> Únicamente partición alineada. (Mejora la administración).<br /><br /> Utilice solo uno de estos valores con este elemento.<br /><br /> **ALIGNED** significa que, en la recomendación generada por el Asistente para la optimización de motor de base de datos, cada índice propuesto se divide exactamente igual que la tabla subyacente para la que se ha definido el índice. Los índices no clúster de una vista indizada se alinean con la vista indizada.|  
|**Valor predeterminado**|**NONE**|  
|**Repetición**|Una obligatoria para el elemento `TuningOptions`, a menos que se utilice el elemento `DropOnlyMode`. Si se utiliza `DropOnlyMode`, no es posible utilizar `Partitioning`. Estos elementos son mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
