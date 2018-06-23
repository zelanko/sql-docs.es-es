---
title: Elemento de la base de datos de configuración (DTA) | Documentos de Microsoft
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
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6afd8b418cd00c2ec89430e4c82613ea1af285d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105726"
---
# <a name="database-element-for-configuration-dta"></a>Database (DTA, elemento de Configuration)
  Especifica la base de datos que se usará Database Engine Tuning Advisor para evaluar la configuración hipotética (especificada por el `Configuration` elemento).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Obligatoria una o más veces por `Server` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento de servidor para la configuración de &#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**Elementos secundarios**|[El nombre de elemento de base de datos &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento de esquema de base de datos &#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [Elemento Recommendation &#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Notas  
 Este elemento tiene el nombre **DatabaseTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento `Database` con el que tiene al elemento `Server` como raíz primaria, que se encuentra en la parte superior del archivo de entrada XML. Para obtener más información, vea [Elemento Database para servidor &#40;DTA&#41;](database-element-for-server-dta.md).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este `Database` elemento, vea la [ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  