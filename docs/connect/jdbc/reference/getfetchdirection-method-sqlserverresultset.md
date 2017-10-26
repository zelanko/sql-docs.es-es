---
title: "getFetchDirection (método) (SQLServerResultSet) | Documentos de Microsoft"
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
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2667676b22af4c4f25b8adfb4bb0565dd2e6abf9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la dirección de la captura para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica la dirección de la captura actual.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getFetchDirection especificado por el método getFetchDirection en la interfaz java.sql.ResultSet.  
  
 Este método devuelve FETCH_FORWARD para los cursores de solo avance, el último valor realizado por una llamada a la [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) método para otros tipos de cursor, devolverá fetch_unknown para estos tipos de cursor si el método setFetchDirection nunca se ha llamado.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

