---
title: Server (DTA, elemento de Configuration) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2bc763d621d15f982a2670483683d3862e678c98
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63283675"
---
# <a name="server-element-for-configuration-dta"></a>Server (DTA, elemento de Configuration)
  Contiene la información de identificación del servidor en el que desea que el Asistente para la optimización de motor de base de datos evalúe la configuración hipotética (especificada por el elemento `Configuration`).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Se requiere una vez por elemento `Configuration`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento Configuration &#40;DTA&#41;](configuration-element-dta.md)|  
|**Elementos secundarios**|[Name &#40;DTA, elemento de Server&#41;](name-element-for-server-dta.md)<br /><br /> [Database &#40;DTA, elemento de Configuration&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Observaciones  
 Solo puede especificar un `Server` elemento para el `Configuration` elemento. Este elemento tiene el nombre **ServerTypecomplexType** en el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100). No confunda este elemento `Server` con el elemento secundario de `DTAInput`. Para obtener más información, vea [Server &#40;DTA, elemento&#41;](server-element-dta.md).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
