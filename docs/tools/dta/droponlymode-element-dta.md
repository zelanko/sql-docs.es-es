---
title: Droponlymode, elemento (DTA) | Documentos de Microsoft
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
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c30ec1f3a06e0bb2142dd889852ddb071b68d96
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Especifica que el Asistente para la optimización de motor de base de datos solo debe quitar índices, vistas indizadas o particiones ya existentes durante la sesión de optimización. Cuando se especifica esta opción de optimización, no se consideran nuevas estructuras de diseño físico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
 **Tipo y longitud de los datos**  
  
 **Valor predeterminado**  
  
 **Repetición**: opcional. Se puede utilizar una sola vez por cada elemento **TuningOptions** . No se puede utilizar si se especifican los siguientes elementos en el elemento **TuningOptions** :  
  
-   [FeatureSet &#40;DTA, elemento&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning &#40;DTA, elemento&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [KeepExisting &#40;DTA, elemento&#41;](../../tools/dta/keepexisting-element-dta.md) se establece en **ALL**  
  
## <a name="element-relationships"></a>Relaciones del elemento  
 **Elemento primario**: [TuningOptions &#40;DTA, elemento&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
 **Elementos secundarios**  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra la sección **TuningOptions** de un archivo de entrada XML del Asistente para la optimización de motor de base de datos donde se especifica **DropOnlyMode** . En este ejemplo, la hora de optimización se limita a 24 horas (1440 minutos) y se considerará la eliminación de todos los clúster y no clúster existentes:  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>Ver también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
