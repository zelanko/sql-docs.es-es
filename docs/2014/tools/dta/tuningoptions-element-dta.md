---
title: TuningOptions (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1c58386630e3ee531e14af25306a1cc3b3ca3540
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007514"
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Si se utiliza, solo puede hacerse una vez para cada elemento `DTAInput`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)|  
|**Elementos secundarios**|Elemento `ReportSet`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento `TuningLogTable`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento `NumberOfEvents`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> [TuningTimeInMin &#40;DTA, elemento&#41;](tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB &#40;DTA, elemento&#41;](storageboundinmb-element-dta.md)<br /><br /> Elemento `MaxKeyColumnsInIndex`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento `MaxColumnsInIndex`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento `MinPercentageImprovement`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [TestServer &#40;DTA, elemento&#41;](server-element-dta.md)<br /><br /> [FeatureSet &#40;DTA, elemento&#41;](featureset-element-dta.md)<br /><br /> [Partitioning &#40;DTA, elemento&#41;](partitioning-element-dta.md)<br /><br /> [DropOnlyMode &#40;DTA, elemento&#41;](droponlymode-element-dta.md)<br /><br /> [KeepExisting &#40;DTA, elemento&#41;](keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation &#40;DTA, elemento&#41;](onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect &#40;DTA, elemento&#41;](databasetoconnect-element-dta.md)<br /><br /> Elemento `IgnoreConstantsInWorkload`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento `RetainShellDB`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="example"></a>Ejemplo  
 Para obtener ejemplos del `TuningOptions` elemento, vea los [ejemplos de archivos de entrada XML &#40;DTA&#41;](xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
