---
title: "Método executeUpdate (SQLServerStatement) | Documentos de Microsoft"
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
apiname: SQLServerStatement.executeUpdate
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c0c1f5238ece3adb72f108061742034b3df159f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="executeupdate-method-sqlserverstatement"></a>Método executeUpdate (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL determinada, que puede ser una instrucción INSERT, UPDATE o DELETE; o una instrucción SQL que no devuelve nada, como una instrucción DDL de SQL. A partir de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, executeUpdate devolverán el número correcto de filas actualizadas en una operación de combinación.  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nombre|Description|  
|----------|-----------------|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|Ejecuta la instrucción SQL determinada, que puede ser una instrucción INSERT, UPDATE, DELETE o MERGE; o una instrucción SQL que no devuelve nada, como una instrucción DDL de SQL.|  
|[executeUpdate (java.lang.String, int)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|Se ejecuta la instrucción SQL especificada y señala el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con la marca indicada sobre si las claves generadas automáticamente generan por esta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto debe estar disponible para la recuperación.|  
|[executeUpdate (java.lang.String, int &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|Ejecuta la instrucción SQL determinada e indica al controlador JDBC que las claves que se han generado automáticamente y están presentes en la matriz determinada deben estar disponibles para su recuperación.|  
|[executeUpdate (java.lang.String, java.lang.String &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|Ejecuta la instrucción SQL determinada e indica al controlador JDBC que las claves que se han generado automáticamente y están presentes en la matriz determinada deben estar disponibles para su recuperación.|  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
