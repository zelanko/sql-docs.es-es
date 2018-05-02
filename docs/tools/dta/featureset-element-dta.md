---
title: FeatureSet, elemento (DTA) | Documentos de Microsoft
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
- FeatureSet element
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73bfa6884ff978c962215924287be551e29ec07e
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="featureset-element-dta"></a>FeatureSet (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Contiene las estructuras de diseño físico (índices o vistas indizadas) que quiere que utilice el Asistente para la optimización de motor de base de datos durante el análisis.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, sin longitud máxima.|  
|**Valores permitidos**|**IDX_IV**<br /> Índices y vistas indizadas.<br /><br /> **IDX**<br /> Solo índices.<br /><br /> **IV**<br /> Solo vistas indizadas.<br /><br /> **NCL_IDX**<br /> Solo índices no clúster.<br /><br /> Utilice uno de estos valores con este elemento.|  
|**Valor predeterminado**|**IDX**|  
|**Repetición**|Una obligatoria para cada elemento **TuningOptions** , a menos que se utilice el elemento **DropOnlyMode** . Si se utiliza **DropOnlyMode** , no es posible utilizar **FeatureSet**. Estos elementos son mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Ver también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
