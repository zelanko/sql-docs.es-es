---
title: "Método getMaxStatements (SQLServerDatabaseMetaData) | Documentos de Microsoft"
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
apiname: SQLServerDatabaseMetaData.getMaxStatements
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 71d58431-b671-49c5-939a-f581d1fef7cd
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 710be054840b51c6b22def89d73d62fc2a0d5df7
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getmaxstatements-method-sqlserverdatabasemetadata"></a>Método getMaxStatements (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de instrucciones activas que se pueden abrir para esta base de datos al mismo tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMaxStatements()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el número máximo de instrucciones activas permitidas.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getMaxStatements especificado por el método getMaxStatements en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
