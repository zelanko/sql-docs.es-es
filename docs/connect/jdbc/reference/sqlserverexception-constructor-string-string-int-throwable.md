---
title: SQLServerException Constructor (java.lang.String, java.lang.String, int, java.lang.Throwable) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c724877b07371eb4200492f93c1f7aa22b67c84
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException Constructor (java.lang.String, java.lang.String, int, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) clase cuando se especifica un **cadena** objeto, un **cadena** objeto, un **int**y un **puede producir** objeto.

## <a name="syntax"></a>Sintaxis  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parámetros  
 *errText*  
  
 Una cadena que contiene el texto del error.
  
 *errState*  
  
 Una cadena que contiene el estado del error.
 
 *errNum*  
  
 Un valor int que contiene el código de error para la excepción.
 
 *Causa*  
  
 Un objeto puede producir que contiene la causa de la excepción.
  
## <a name="see-also"></a>Vea también  
 [Constructores de SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Miembros de SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Clase SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
