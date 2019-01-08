---
title: DatabaseToConnect (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fef2df598d96b33def41f27345f88226fd4c6b5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821929"
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
|**Repetición**|Opcional. Se puede utilizar una vez por cada elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[TuningOptions &#40;DTA, elemento&#41;](tuningoptions-element-dta.md)|  
|**Elementos secundarios**|None|  
  
## <a name="remarks"></a>Comentarios  
 Utilice `DatabaseToConnect` para especificar el nombre de la primera base de datos a la que desea que se conecte el Asistente para la optimización de motor de base de datos cuando inicie la sesión de optimización. Con este elemento, solo es posible especificar una base de datos. Si se especifican varias bases de datos, el Asistente para la optimización de motor de base de datos devuelve un error.  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso, vea [Ejemplo de archivo de entrada XML con carga de trabajo insertada &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
