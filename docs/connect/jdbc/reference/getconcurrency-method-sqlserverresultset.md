---
title: getConcurrency (método) (SQLServerResultSet) | Documentos de Microsoft
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
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38a9bf912c0a967a29c8a6ff3543418d1c29b957
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el modo de simultaneidad de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el tipo de simultaneidad, que puede ser uno de los siguientes valores:  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getConcurrency especificado por el método getConcurrency en la interfaz java.sql.ResultSet.  
  
 La simultaneidad empleado viene determinado por la [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que creó el conjunto de resultados.  
  
 Este método se puede utilizar para determinar la simultaneidad actual. Si la aplicación seleccionó CONCUR_READ_ONLY o CONCUR_UPDATABLE, estos se devolverán. Si la aplicación utilizó la simultaneidad predeterminada, se devolverá CONCUR_READ_ONLY.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
