---
title: Método valueOf (java.sql.Timestamp, java.util.Calendar) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e75ea9ae6b98041d2f79d2a8a0c515ed1b05b2a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>Método valueOf (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un **DateTimeOffset** objeto que representa un punto en el tiempo en un desplazamiento en concreto de GMT según un valor java.sql.Timestamp y un valor java.util.Calendar que indica el desplazamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *timestamp*  
  
 Un valor java.sql.Timestamp.  
  
 *Calendario*  
  
 Valor de desplazamiento.  Los componentes de fecha y hora de *calendario* establecidas de acuerdo con la *timestamp* valor.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un objeto DateTimeOffset que representa el punto en el tiempo determinado por el objeto java.sql.Timestamp en la zona horaria del objeto java.util.Calendar determinado.  
  
## <a name="remarks"></a>Comentarios  
 Este método también establece el objeto de java.util.Calendar hasta el punto en el tiempo especificado por el objeto java.sql.Timestamp.  
  
## <a name="see-also"></a>Vea también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
