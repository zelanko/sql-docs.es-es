---
title: Elemento de la base de datos de servidor (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b23e8d7f68cca0722691863a2c5c8d5e095c33c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62661837"
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
|Repetición|Obligatoria una o más veces por elemento `Server`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|Elemento primario|[Server &#40;DTA, elemento&#41;](server-element-dta.md)|  
|Elementos secundarios|[Name &#40;DTA, elemento de Database&#41;](name-element-for-database-dta.md)<br /><br /> [Schema &#40;DTA, elemento de Database&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento tiene el nombre **DatabaseDetailsTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento `Database` con el que tiene al elemento `Configuration` como raíz primaria. Para obtener más información, vea [Database &#40;DTA, elemento de Configuration&#41;](database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de la `Database` elemento, vea [elemento Server &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
