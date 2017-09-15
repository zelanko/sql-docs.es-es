---
title: "Método getQueryTimeout (SQLServerStatement) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8dff954f-b458-4fa6-abe6-be62ff75e2b9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fff7b7d5310caf4ea57d929037c82aff1ae3f024
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getquerytimeout-method-sqlserverstatement"></a>Método getQueryTimeout (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número de segundos [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] esperará a que esto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que se va a ejecutar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getQueryTimeout()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el número de segundos que esperará el controlador JDBC o 0 si no hay ningún límite.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getQueryTimeout especificado por el método getQueryTimeout en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
