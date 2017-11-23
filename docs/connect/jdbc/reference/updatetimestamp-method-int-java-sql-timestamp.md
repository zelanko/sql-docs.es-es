---
title: "Método updateTimestamp (int, java.sql.Timestamp) | Documentos de Microsoft"
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
apiname: SQLServerResultSet.updateTimestamp (int, java.sql.Timestamp)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: db83d9d7-137b-4a28-a2ca-d4782e0a256e
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: caad0346179f4af9548f840c0d0745e4df8b19d1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="updatetimestamp-method-int-javasqltimestamp"></a>Método updateTimestamp (int, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor timestamp según el índice de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateTimestamp(int index,  
                            java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Un **int** que indica el índice de columna.  
  
 *x*  
  
 Un valor timestamp.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateTimestamp es especificado por el método updateTimestamp en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Método updateTimestamp &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
