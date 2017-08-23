---
title: Elemento DatabaseToConnect (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 94746d3007587223ba1b2ae6a3868ce3a013bafd
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# DatabaseToConnect (DTA, elemento)
  Especifica la primera base de datos a la que se conecta el Asistente para la optimización de motor de base de datos al optimizar una carga de trabajo.  
  
## Sintaxis  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Se puede utilizar una vez por cada elemento **TuningOptions** .|  
  
## Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Tuningoptions, elemento &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos secundarios**|Ninguno|  
  
## Comentarios  
 Utilice **DatabaseToConnect** para especificar el nombre de la primera base de datos a la que desea que se conecte el Asistente para la optimización de motor de base de datos cuando inicie la sesión de optimización. Con este elemento, solo es posible especificar una base de datos. Si se especifican varias bases de datos, el Asistente para la optimización de motor de base de datos devuelve un error.  
  
## Ejemplo  
 Para obtener un ejemplo de uso, vea [Ejemplo de archivo de entrada XML con carga de trabajo insertada &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
