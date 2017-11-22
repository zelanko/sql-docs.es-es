---
title: Elemento DTAInput (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 01ce41754770e58ae35e5c1ca6c1d94dab4d5fb1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="dtainput-element-dta"></a>DTAInput (DTA, elemento)
  Contiene la definición de la entrada XML del Asistente para la optimización de motor de base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Características|Descripción|  
|---------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una opcional por elemento **DTAXML** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[DTAXML &#40;DTA, elemento&#41;](../../tools/dta/dtaxml-element-dta.md)|  
|**Elementos secundarios**|[Server &#40;DTA, elemento&#41;](../../tools/dta/server-element-dta.md)<br /><br /> [Workload &#40;DTA, elemento&#41;](../../tools/dta/workload-element-dta.md)<br /><br /> [Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)<br /><br /> [Configuration &#40;DTA, elemento&#41;](../../tools/dta/configuration-element-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento es la raíz de la jerarquía del esquema de entrada del Asistente para la optimización de motor de base de datos. La entrada del Asistente para la optimización de motor de base de datos pueden ser argumentos que especifiquen los servidores cuyas bases de datos se desean optimizar, cargas de trabajo, opciones de optimización o una configuración especificada por el usuario.  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso del elemento **DTAInput**, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
