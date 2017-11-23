---
title: "Método Truncate (SQLServerNClob) | Documentos de Microsoft"
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
ms.assetid: b7e8210d-a724-4bae-832a-ae4c63031c9c
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b09192763b6982db02a53f758b6aab1837612085
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="truncate-method-sqlservernclob"></a>Método truncate (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Trunca la **NCLOB** a la longitud especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Len*  
  
 La longitud, en caracteres, para que la **NCLOB** se debe truncar el valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método truncar es especificado por el método truncar en la interfaz java.sql.NClob.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Miembros de SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
