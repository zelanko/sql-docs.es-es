---
title: Tuningoptions, elemento (DTA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b816f81d12c7a05fb2be4c38dcd4b5bf1a867c10
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105031"
---
# <a name="tuningoptions-element-dta"></a>TuningOptions (DTA, elemento)
  Contiene las opciones de optimización de una sesión de optimización concreta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Si usa, sólo puede utilizarse una vez para cada `DTAInput` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)|  
|**Elementos secundarios**|`ReportSet` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `TuningLogTable` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `NumberOfEvents` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> [Elemento TuningTimeInMin &#40;DTA&#41;](tuningtimeinmin-element-dta.md)<br /><br /> [Elemento StorageBoundInMB &#40;DTA&#41;](storageboundinmb-element-dta.md)<br /><br /> `MaxKeyColumnsInIndex` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `MaxColumnsInIndex` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `MinPercentageImprovement` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [Elemento TestServer &#40;DTA&#41;](server-element-dta.md)<br /><br /> [FeatureSet, elemento &#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Partitioning, elemento &#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [Droponlymode, elemento &#40;DTA&#41;](droponlymode-element-dta.md)<br /><br /> [KeepExisting, elemento &#40;DTA&#41;](keepexisting-element-dta.md)<br /><br /> [Onlineindexoperation, elemento &#40;DTA&#41;](onlineindexoperation-element-dta.md)<br /><br /> [Elemento DatabaseToConnect &#40;DTA&#41;](databasetoconnect-element-dta.md)<br /><br /> `IgnoreConstantsInWorkload` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `RetainShellDB` Elemento. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="example"></a>Ejemplo  
 Para obtener ejemplos de la `TuningOptions` elemento, vea la [ejemplos de archivos de entrada XML &#40;DTA&#41;](xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  