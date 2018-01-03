---
title: Partitioning, elemento (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57f49195654c7a83d8297eae1941a7d2202a115c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="partitioning-element-dta"></a>Partitioning (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Contiene el esquema de partición que le gustaría Database Engine Tuning Advisor para usar durante el análisis.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, sin longitud máxima.|  
|**Valores permitidos**|**NONE**<br /> Ninguna partición.<br /><br /> **FULL**<br /> Partición total. (Mejora el rendimiento).<br /><br /> **ALIGNED**<br /> Únicamente partición alineada. (Mejora la administración).<br /><br /> Utilice solo uno de estos valores con este elemento.<br /><br /> **ALIGNED** significa que, en la recomendación generada por el Asistente para la optimización de motor de base de datos, cada índice propuesto se divide exactamente igual que la tabla subyacente para la que se ha definido el índice. Los índices no clúster de una vista indizada se alinean con la vista indizada.|  
|**Valor predeterminado**|**NONE**|  
|**Repetición**|Una obligatoria para el elemento **TuningOptions** , a menos que se utilice el elemento **DropOnlyMode** . Si se utiliza **DropOnlyMode** , no es posible utilizar **Partitioning**. Estos elementos son mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
