---
title: "Método executeUpdate (java.lang.String) (SQLServerStatement) | Documentos de Microsoft"
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
- SQLServerStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85e7c3a2-f2da-49bf-9d90-5fd246fd60e1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b5727ab7d6198e4b075b0e985e638345f095cef
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring-sqlserverstatement"></a>Método executeUpdate (java.lang.String) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL determinada, que puede ser una instrucción INSERT, UPDATE o DELETE; o una instrucción SQL que no devuelve nada, como una instrucción DDL de SQL. A partir de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, executeUpdate devolverán el número correcto de filas actualizadas en una operación de combinación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int executeUpdate(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *SQL*  
  
 A **cadena** que contiene la instrucción SQL.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el número de filas afectadas o 0 si se utiliza una instrucción DDL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método executeUpdate es especificado por el método executeUpdate en la interfaz java.sql.Statement.  
  
 Si ejecuta un procedimiento almacenado da como resultado un recuento de actualizaciones que es mayor que uno, o que genera más de un conjunto de resultados, use la [ejecutar](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método para ejecutar el procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Método executeUpdate &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

