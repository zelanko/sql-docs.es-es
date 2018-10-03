---
title: DatabaseToConnect (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b458e0707f36bde18f6128ae302c7e5826fb5680
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078595"
---
# <a name="databasetoconnect-element-dta"></a>DatabaseToConnect (DTA, elemento)
  Especifica la primera base de datos a la que se conecta el Asistente para la optimización de motor de base de datos al optimizar una carga de trabajo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Puede utilizar una vez por cada `TuningOptions` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions, elemento &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos secundarios**|None|  
  
## <a name="remarks"></a>Comentarios  
 Use `DatabaseToConnect` para especificar el nombre de la primera base de datos al que desee Database Engine Tuning Advisor para conectarse cuando se inicia la sesión de optimización. Con este elemento, solo es posible especificar una base de datos. Si se especifican varias bases de datos, el Asistente para la optimización de motor de base de datos devuelve un error.  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso, vea [Ejemplo de archivo de entrada XML con carga de trabajo insertada &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
