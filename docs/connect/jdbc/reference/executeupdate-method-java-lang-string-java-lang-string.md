---
title: Método executeUpdate (java.lang.String, java.lang.String) | Documentos de Microsoft
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
- SQLServerStatement.executeUpdate (java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f44a689-65c8-4c94-9574-e9c08ea7918e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08504da732634c16a6d2176f1430587046893ed1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 *sql*  
  
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
 [Método executeUpdate &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
