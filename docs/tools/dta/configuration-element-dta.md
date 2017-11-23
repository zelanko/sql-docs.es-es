---
title: "Elemento de configuración (DTA) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20e3d53c5e7825af7a018d0a42b2361f1fe2e5d1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
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
|**SpecificationMode**|Opcional. Especifica si el Asistente para la optimización de motor de base de datos debe analizar la configuración especificada con respecto a la configuración actual existente o como una independiente totalmente nueva. Utilice un tipo de datos **string** para especificar este atributo mediante uno de los siguientes valores permitidos:<br /><br /> **Relative**:<br />                  Evalúa la configuración especificada con respecto a la configuración actual existente de las estructuras de diseño físico (índices, vistas indizadas, particiones) de la base de datos que se está optimizando. Por ejemplo:<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  Evalúa la configuración especificada como una configuración independiente. Cuando se especifica Absolute, el Asistente para la optimización de motor de base de datos no tiene en cuenta la configuración existente. Por ejemplo:<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Se puede utilizar una vez por cada elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementos secundarios**|[Elemento Server de Configuration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
