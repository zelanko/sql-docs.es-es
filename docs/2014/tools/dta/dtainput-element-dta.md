---
title: Elemento DTAInput (DTA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7b414d14cf69815086973849d5e0f6b3badb6b3b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111929"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Características|Descripción|  
|---------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una opcional por elemento **DTAXML** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAXML &#40;DTA&#41;](dtaxml-element-dta.md)|  
|**Elementos secundarios**|[Elemento Server &#40;DTA&#41;](server-element-dta.md)<br /><br /> [Workload, elemento &#40;DTA&#41;](workload-element-dta.md)<br /><br /> [Tuningoptions, elemento &#40;DTA&#41;](tuningoptions-element-dta.md)<br /><br /> [Elemento de configuración &#40;DTA&#41;](configuration-element-dta.md)|  
  
## <a name="remarks"></a>Notas  
 Este elemento es la raíz de la jerarquía del esquema de entrada del Asistente para la optimización de motor de base de datos. La entrada del Asistente para la optimización de motor de base de datos pueden ser argumentos que especifiquen los servidores cuyas bases de datos se desean optimizar, cargas de trabajo, opciones de optimización o una configuración especificada por el usuario.  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso del elemento **DTAInput**, vea [Ejemplo de archivo de entrada XML simple &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  