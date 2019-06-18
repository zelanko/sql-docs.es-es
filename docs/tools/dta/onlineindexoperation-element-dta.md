---
title: OnlineIndexOperation (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6832df1d7940f71770b8f691c9b26b911c435d50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62660008"
---
# <a name="onlineindexoperation-element-dta"></a>OnlineIndexOperation (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica si los índices, las vistas indizadas o las particiones recomendados por el Asistente para la optimización de motor de base de datos se pueden crear en línea.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, sin longitud máxima.|  
|**Valores permitidos**|**OFF**<br /> No se pueden crear en línea las estructuras recomendadas de diseño físico.<br /><br /> **ON**<br /> Se pueden crear en línea todas las estructuras recomendadas de diseño físico.<br /><br /> **MIXED**<br /> Siempre que es posible, el Asistente para la optimización de motor de base de datos intenta recomendar las estructuras de diseño físico que se pueden crear en línea.<br /><br /> Utilice uno de estos valores con este elemento. Si los índices se crean en línea, se anexa la palabra clave **ONLINE = ON** a la definición del objeto.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Si se utiliza, solo puede hacerse una vez para el elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
