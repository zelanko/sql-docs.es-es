---
title: Método getShort (java.lang.String) (SQLServerResultSet) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getShort (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 183af414-b0a3-4ca7-b160-d199bcf469b0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab32e81f265e36286a878c9e2376adcb55ced6d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getshort-method-javalangstring-sqlserverresultset"></a>Método getShort (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **breve** en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public short getShort(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 A **corto** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getShort especificado por el método getShort en la interfaz java.sql.ResultSet.  
  
 Este método solo se admite en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de datos que pueden devolver un valor entero como smallint, tinyint y bit de forma segura. Si se utiliza este método en cualquier otro tipo de datos, provocará una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Método getShort &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
