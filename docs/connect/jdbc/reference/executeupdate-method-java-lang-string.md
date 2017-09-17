---
title: "Método executeUpdate (java.lang.String, int[]) | Documentos de Microsoft"
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
- SQLServerStatement.executeUpdate (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b3d5b60-4285-4047-b13e-106754ca0d98
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 60e6995abe98bb45c682f251189a6a307334d87b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring-int"></a>Método executeUpdate (java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL especificada y señala [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] que las claves generadas automáticamente que se indican en la matriz especificada deben estar disponibles para la recuperación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *SQL*  
  
 A **cadena** que contiene una instrucción SQL.  
  
 *columnIndexes*  
  
 Una matriz de valores int que indica que los índices de columna de las claves que se generaron automáticamente deben estar disponibles.  
  
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
  
  
