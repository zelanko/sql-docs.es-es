---
title: DTAInput (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 46af27730ab2bb7a0c1bfaa4f4e9dc625ed0eb0b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048439"
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
|**Elemento primario**|[Elemento DTAXML &#40;DTA&#41;](dtaxml-element-dta.md)|  
|**Elementos secundarios**|[Server &#40;DTA, elemento&#41;](server-element-dta.md)<br /><br /> [Workload &#40;DTA, elemento&#41;](workload-element-dta.md)<br /><br /> [TuningOptions &#40;DTA, elemento&#41;](tuningoptions-element-dta.md)<br /><br /> [Elemento Configuration &#40;DTA&#41;](configuration-element-dta.md)|  
  
## <a name="remarks"></a>Observaciones  
 Este elemento es la raíz de la jerarquía del esquema de entrada del Asistente para la optimización de motor de base de datos. La entrada del Asistente para la optimización de motor de base de datos pueden ser argumentos que especifiquen los servidores cuyas bases de datos se desean optimizar, cargas de trabajo, opciones de optimización o una configuración especificada por el usuario.  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso del elemento **DTAInput**, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
