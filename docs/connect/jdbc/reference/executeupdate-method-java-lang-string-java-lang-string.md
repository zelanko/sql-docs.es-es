---
title: "Método executeUpdate (java.lang.String, java.lang.String) | Documentos de Microsoft"
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
- SQLServerStatement.executeUpdate (java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f44a689-65c8-4c94-9574-e9c08ea7918e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53682225a680d9913fd03e4e7a52beee729eecbc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring-javalangstring"></a>Método executeUpdate (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se ejecuta la instrucción SQL especificada y señales [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] que las claves generadas automáticamente indican en la matriz determinada debe estar disponible para la recuperación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *SQL*  
  
 A **cadena** que contiene una instrucción SQL.  
  
 *columnNames*  
  
 Una matriz de tipo **cadena** que indica que los nombres de columna de las claves generadas automáticamente deben estar disponibles.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el número de filas afectadas, 0 si se utiliza una instrucción DDL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método executeUpdate es especificado por el método executeUpdate en la interfaz java.sql.Statement.  
  
 Si ejecuta un procedimiento almacenado da como resultado un recuento de actualizaciones que es mayor que uno, o que genera más de un conjunto de resultados, use la [ejecutar](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método para ejecutar el procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Método executeUpdate &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
