---
title: "Método (SQLServerStatement) getMaxRows | Documentos de Microsoft"
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
apiname: SQLServerStatement.getMaxRows
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8211894887356f993067bc214e101f171f1d490e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows (método) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de filas que un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto puede contener.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el número máximo de filas, o 0 si no hay ningún límite.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getMaxRows especificado por el método getMaxRows en la interfaz java.sql.Statement.  
  
 Este método getMaxRows siempre devuelve 0 para los cursores desplazables dinámicos.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
