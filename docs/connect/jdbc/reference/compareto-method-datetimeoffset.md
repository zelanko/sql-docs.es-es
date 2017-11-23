---
title: "Método compareTo (DateTimeOffset) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ecd77b1080f1a5c49059f65e857d56c8d582b1b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="compareto-method-datetimeoffset"></a>Método compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Compara este **DateTimeOffset** objeto a otro **DateTimeOffset** objeto basándose en la hora en GMT.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parámetros  
 A [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor que se va a comparar con la instancia actual.  
  
## <a name="return-value"></a>Valor devuelto  
 La tabla siguiente describe los valores devueltos de este método:  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0|Ambos **DateTimeOffset** objetos representan el mismo punto en el tiempo.|  
|número negativo|Esto **DateTimeOffset** objeto representa un punto en el tiempo que se encuentra antes *otros*.|  
|número positivo|Esto **DateTimeOffset** objeto representa un punto en el tiempo que se encuentra después *otros*.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando dos **DateTimeOffset** objetos tienen la misma hora en GMT, no hay ninguna ordenación adicional de los objetos según el desplazamiento.  
  
## <a name="see-also"></a>Vea también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
