---
title: "Método valueOf (java.sql.Timestamp, int) | Documentos de Microsoft"
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
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c79a5f486377bc86264377a898a9f908bbc7153
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="valueof-method-javasqltimestamp-int"></a>Método valueOf (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un **DateTimeOffset** objeto que representa un punto en el tiempo en un desplazamiento en concreto de GMT según un valor java.sql.Timestamp y un valor que indica el desplazamiento en minutos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *timestamp*  
  
 Un valor java.sql.Timestamp.  
  
 *minutesOffset*  
  
 El desplazamiento en minutos.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un objeto DateTimeOffset que representa el punto cronológico según el objeto java.sql.Timestamp en el desplazamiento dado, minutos, respecto a GMT.  
  
## <a name="see-also"></a>Vea también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
