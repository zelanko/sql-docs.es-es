---
title: SQLServerException Constructor (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean) | Documentos de Microsoft
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
ms.openlocfilehash: e2aa5485f6568d2a01655e273f57b07448c7590d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>SQLServerException Constructor (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) clase cuando se especifica un **objeto**, **cadena** objeto, un **cadena** (objeto), un  **StreamError** objeto y un **booleano**.

## <a name="syntax"></a>Sintaxis  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parámetros  
 *obj*  
  
 El búfer de E/S que generó la excepción.

 *errText*  
  
 Una cadena que contiene el texto del error.
  
 *sqlState*  
  
 Un objeto de enumeración que contiene el estado SQL.
 
 *streamError*  
  
 Un objeto StreamError que contiene detalles sobre el error.
 
 *bStack*  
  
 Un valor booleano que indica si se debe generar el seguimiento de pila.
  
## <a name="see-also"></a>Vea también  
 [Constructores de SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Miembros de SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Clase SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
