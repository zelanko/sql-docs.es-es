---
title: "Método executeQuery (java.lang.String) | Documentos de Microsoft"
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
apiname: SQLServerPreparedStatement.executeQuery (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 610205c2-6bcd-426c-ad6f-9682551efdec
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d848338f8f4599e07c7c71b0b723150499ec6054
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="executequery-method-javalangstring"></a>Método executeQuery (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL especificada y devuelve una sola [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *SQL*  
  
 A **cadena** que contiene una instrucción SQL.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método executeQuery es especificado por el método executeQuery en la interfaz java.sql.Statement.  
  
 Este método invalida el [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método que se encuentra en la [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) clase.  
  
 Llamar a este método producirá una excepción porque la instrucción SQL para el objeto SQLServerPreparedStatement no se especifica cuando se crea el objeto.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) se produce si la instrucción SQL especificada genera algo distinto de una sola [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="see-also"></a>Vea también  
 [Método executeQuery &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
