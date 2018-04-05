---
title: Tuningoptions, elemento (DTA) | Documentos de Microsoft
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
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f82d39a90f515d4f70d9e48bef7f20996ba60f78
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="tuningoptions-element-dta"></a>TuningOptions (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Contiene las opciones de optimización de una sesión de optimización concreta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Si se utiliza, solo puede hacerse una vez para cada elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAInput &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementos secundarios**|Elemento**ReportSet** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**TuningLogTable** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**NumberOfEvents** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> [Elemento TuningTimeInMin &#40; DTA &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB &#40;DTA, elemento&#41;](../../tools/dta/storageboundinmb-element-dta.md)<br /><br /> Elemento**MaxKeyColumnsInIndex** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**MaxColumnsInIndex** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**MinPercentageImprovement** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [Elemento TestServer &#40; DTA &#41;](../../tools/dta/testserver-element-dta.md)<br /><br /> [FeatureSet, elemento &#40; DTA &#41;](../../tools/dta/featureset-element-dta.md)<br /><br /> [Creación de particiones elemento &#40; DTA &#41;](../../tools/dta/partitioning-element-dta.md)<br /><br /> [Droponlymode, elemento &#40; DTA &#41;](../../tools/dta/droponlymode-element-dta.md)<br /><br /> [KeepExisting, elemento &#40; DTA &#41;](../../tools/dta/keepexisting-element-dta.md)<br /><br /> [Onlineindexoperation, elemento &#40; DTA &#41;](../../tools/dta/onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect &#40;DTA, elemento&#41;](../../tools/dta/databasetoconnect-element-dta.md)<br /><br /> Elemento**IgnoreConstantsInWorkload** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**RetainShellDB** . Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="example"></a>Ejemplo  
 Para ver ejemplos del elemento **TuningOptions**, vea [Ejemplos de archivos de entrada XML &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
