---
title: Elemento de la base de datos de configuración (DTA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
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
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02fc044ef6ce1e015743ee503ed77ea843b0e182
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="database-element-for-configuration-dta"></a>Database (DTA, elemento de Configuration)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Especifica la base de datos que se usará Database Engine Tuning Advisor para evaluar la configuración hipotética (especificada por el **configuración** elemento).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Obligatoria una o más veces por elemento **Server** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento de servidor de configuración &#40; DTA &#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
|**Elementos secundarios**|[Elemento de nombre de base de datos &#40; DTA &#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Elemento de esquema de base de datos &#40; DTA &#41;](../../tools/dta/schema-element-for-database-dta.md)<br /><br /> [Elemento Recommendation &#40; DTA &#41;](../../tools/dta/recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento tiene el nombre **DatabaseTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento **Database** con el que tiene al elemento **Server** como raíz primaria, que se encuentra en la parte superior del archivo de entrada XML. Para obtener más información, vea [Elemento Database para servidor &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento **Database**, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
