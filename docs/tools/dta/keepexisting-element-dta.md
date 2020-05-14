---
title: KeepExisting (DTA, elemento)
description: En la utilidad DTA, el elemento KeepExisting especifica las estructuras de diseño físico que el Asistente para la optimización de motor de base de datos conserva cuando genera recomendaciones.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: d76ae0a45b08ff826deaac7750688d521746c077
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831509"
---
# <a name="keepexisting-element-dta"></a>KeepExisting (DTA, elemento)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
|**Tipo y longitud de los datos**|**string**, límite de longitud aplicado por el servidor.|  
|**Valores permitidos**|**NONE**<br /> Ninguna estructura existente.<br /><br /> **ALL**<br /> Todas las estructuras existentes.<br /><br /> **ALIGNED**<br /> Todas las estructuras alineadas de partición.<br /><br /> **CL_IDX**<br /> Todos los clúster de las tablas.<br /><br /> **IDX**<br /> Todos los índices clúster y no clúster de las tablas.<br /><br /> Utilice solo uno de estos valores con este elemento.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Se puede utilizar una sola vez por cada elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
