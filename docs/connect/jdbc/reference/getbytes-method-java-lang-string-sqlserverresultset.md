---
title: "Método getBytes (java.lang.String) (SQLServerResultSet) | Documentos de Microsoft"
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
apiname: SQLServerResultSet.getBytes (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ff617165-47f8-41c1-9c51-37ffc7714923
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66111708e248c2bc744492050d3c68847fbd9b50
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getbytes-method-javalangstring-sqlserverresultset"></a>Método getBytes (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **bytes** matriz en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public byte[] getBytes(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Una matriz de **bytes** valores.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBytes es especificado por el método getBytes en la interfaz java.sql.ResultSet.  
  
 Este método admite la recuperación de todas las columnas como una lectura de bytes sin formato desde el servidor. Devuelve una matriz de bytes directamente desde el servidor, en el formato que está almacenado en el servidor.  
  
 En una versión anterior de la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], podía utilizar SQLServerResultSet.getBytes para convertir valores entre las matrices de bytes y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de datos **fecha**, **tiempo**,  **datetime2**, o **datetimeoffset**. Ahora, al usar este método con esos tipos de datos, se producirá una excepción que indica que no se admite la conversión.  
  
## <a name="see-also"></a>Vea también  
 [Método getBytes &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
