---
title: Elemento de la base de datos de servidor (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1988ac62e5a19d235915a95f27e03562f00c31b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="database-element-for-server-dta"></a>Elemento Database para servidor (DTA)
  Especifica la base de datos que se desea optimizar en un servidor concreto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno.|  
|Valor predeterminado|Ninguno.|  
|Repetición|Obligatoria una o más veces por elemento **Server** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|Elemento primario|[Server &#40;DTA, elemento&#41;](../../tools/dta/server-element-dta.md)|  
|Elementos secundarios|[Name &#40;DTA, elemento de Database&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Elemento Schema de Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento tiene el nombre **DatabaseDetailsTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento **Database** con el que tiene al elemento **Configuration** como raíz primaria. Para obtener más información, vea [Database &#40;DTA, elemento de Configuration&#41;](../../tools/dta/database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo del uso del elemento **Database** , vea [Server &#40;DTA, elemento&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
