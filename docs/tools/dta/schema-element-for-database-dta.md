---
title: Elemento de esquema de base de datos (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Schema element
ms.assetid: d932e59c-953f-4ab4-934d-b6baf344835c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f36d625afa75e1bab4108e4a6cb9cadb60eedbf7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661444"
---
# <a name="schema-element-for-database-dta"></a>Schema (DTA, elemento de Database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica el esquema de la base de datos que se desea optimizar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Database>  
...code removed here...  
    <Schema>...</Schema>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria para el elemento **Database** especificado en el elemento **Server** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento Database para servidor &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)|  
|**Elementos secundarios**|[Name &#40;DTA, elemento de Schema&#41;](../../tools/dta/name-element-for-schema-dta.md)<br /><br /> [Table &#40;DTA, elemento de Schema&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo del uso de este elemento, vea [Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Ver también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
