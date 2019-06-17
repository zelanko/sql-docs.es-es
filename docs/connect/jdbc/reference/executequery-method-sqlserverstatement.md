---
title: Método executeQuery (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeQuery
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 599cf463-e19f-4baa-bacb-513cad7c6cd8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8755695a805684338378efa4427c24c333c3da08
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796940"
---
# <a name="executequery-method-sqlserverstatement"></a>Método executeQuery (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL determinada y devuelve un objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) único.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sql*  
  
 Un valor **String** que contiene una instrucción SQL.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método executeQuery especificado por el método executeQuery de la interfaz java.sql.Statement.  
  
 Se produce la excepción [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) si la instrucción SQL especificada genera algo que no sea un único objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
 Si la ejecución de un procedimiento almacenado produce un recuento de actualización mayor que uno o que genera más de un conjunto de resultados, use el método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para ejecutar el procedimiento almacenado.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
