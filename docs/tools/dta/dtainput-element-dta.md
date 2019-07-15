---
title: Elemento DTAInput (DTA) | Microsoft Docs
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
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5731b02656cea4b5456a7bc8051548e4b05d3a1a
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729478"
---
# <a name="dtainput-element-dta"></a>DTAInput (DTA, elemento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="remarks"></a>Notas  
 Este elemento es la raíz de la jerarquía del esquema de entrada del Asistente para la optimización de motor de base de datos. La entrada del Asistente para la optimización de motor de base de datos pueden ser argumentos que especifiquen los servidores cuyas bases de datos se desean optimizar, cargas de trabajo, opciones de optimización o una configuración especificada por el usuario.  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso del elemento **DTAInput**, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
