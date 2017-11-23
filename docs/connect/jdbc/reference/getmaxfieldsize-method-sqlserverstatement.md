---
title: "Método (SQLServerStatement) getMaxFieldSize | Documentos de Microsoft"
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
apiname: SQLServerStatement.getMaxFieldSize
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb2e2e6216631908efeed70e6cf5ac3a9b936abf
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize (método) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de bytes que se pueden devolver para los caracteres y valores de columna binaria en un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el número máximo de bytes que puede contener una columna, o bien 0 si no hay ningún límite.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getMaxFieldSize especificado por el método getMaxFieldSize en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
