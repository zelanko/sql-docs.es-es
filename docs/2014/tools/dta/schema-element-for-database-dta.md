---
title: Elemento de esquema de base de datos (DTA) | Documentos de Microsoft
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
- Schema element
ms.assetid: d932e59c-953f-4ab4-934d-b6baf344835c
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4bcdcba472eb2a439d7786898f30b09d7e1dc50f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196847"
---
# <a name="schema-element-for-database-dta"></a>Schema (DTA, elemento de Database)
  Especifica el esquema de la base de datos que se desea optimizar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Database>  
...code removed here...  
    <Schema>...</Schema>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria para el elemento **Database** especificado en el elemento **Server** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento de la base de datos de servidor &#40;DTA&#41;](database-element-for-server-dta.md)|  
|**Elementos secundarios**|[El nombre de elemento de esquema &#40;DTA&#41;](name-element-for-schema-dta.md)<br /><br /> [Elemento de la tabla de esquema &#40;DTA&#41;](table-element-for-schema-dta.md)|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo del uso de este elemento, vea [Elemento Server &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  