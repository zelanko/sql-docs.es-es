---
title: Name (DTA, elemento de Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: e871c4fa-3b57-46cf-b4f8-e3be86f92dc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f0f192dbf931d5ad80c594b376973ee2db3f31
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63297507"
---
# <a name="name-element-for-database-dta"></a>Name (DTA, elemento de Database)
  Especifica el nombre de la base de datos que se desea optimizar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Server>  
    <Database>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|
  `string`, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Se requiere una vez por elemento `Database`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento Database para servidor &#40;DTA&#41;](database-element-for-server-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo del uso de este elemento, vea [Elemento Server &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
