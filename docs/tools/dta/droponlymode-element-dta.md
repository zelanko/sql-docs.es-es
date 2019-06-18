---
title: DropOnlyMode (DTA, elemento) | Microsoft Docs
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
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f75d3a4c293ebcb2f91c39df4cb1c008601dcde2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62857091"
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica que el Asistente para la optimización de motor de base de datos solo debe quitar índices, vistas indizadas o particiones ya existentes durante la sesión de optimización. Cuando se especifica esta opción de optimización, no se consideran nuevas estructuras de diseño físico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
