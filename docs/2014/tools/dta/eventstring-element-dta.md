---
title: El elemento EventString (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db55d1d2451ab8febf984deb9e5bcb6d4718353f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291701"
---
# <a name="eventstring-element-dta"></a>EventString (DTA, elemento)
  Especifica una carga de trabajo de scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] directamente en el archivo de entrada XML.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|`Weight`|Opcional. Especifica el factor de peso de la consulta (un factor de importancia) del evento especificado. Use un `float` tipo de datos para especificar el peso. Por ejemplo, `Weight`="100,01". El valor mínimo que se puede especificar para `Weight` es "0".|  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, longitud es ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria si no se especifica ningún otro tipo de carga de trabajo. Debe especificar un `EventString`, un `File`, o un `Database` elemento secundario para el `Workload` primario, pero solo un tipo se puede usar. Por ejemplo, si especifica una carga de trabajo con el `EventString` elemento, y no se puede especificar una carga de trabajo con el `File` elemento en el mismo archivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento de la carga de trabajo &#40;DTA&#41;](workload-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con carga de trabajo insertada &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
