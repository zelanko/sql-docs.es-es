---
title: Elemento de configuración (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 934acda419b734f577de4c8127184d3dd18ea650
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150149"
---
# <a name="configuration-element-dta"></a>Configuration (DTA, elemento)
  Establece una configuración especificada por el usuario compuesta por estructuras de diseño físico existentes e hipotéticas para que el Asistente para la optimización de motor de base de datos la analice al optimizar una carga de trabajo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Atributo Configuration|Descripción|  
|-----------------------------|-----------------|  
|`SpecificationMode`|Opcional. Especifica si el Asistente para la optimización de motor de base de datos debe analizar la configuración especificada con respecto a la configuración actual existente o como una independiente totalmente nueva. Utilice un tipo de datos **string** para especificar este atributo mediante uno de los siguientes valores permitidos:<br /><br /> `Relative`: <br />                  Evalúa la configuración especificada con respecto a la configuración actual existente de las estructuras de diseño físico (índices, vistas indizadas, particiones) de la base de datos que se está optimizando. Por ejemplo: <br />`<Configuration SpecificationMode="Relative">`<br /><br /> `Absolute`: <br />                  Evalúa la configuración especificada como una configuración independiente. Cuando se especifica Absolute, el Asistente para la optimización de motor de base de datos no tiene en cuenta la configuración existente. Por ejemplo:<br />`<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Se puede utilizar una vez por cada elemento `DTAInput`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)|  
|**Elementos secundarios**|[Elemento Server de Configuration &#40;DTA&#41;](server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
