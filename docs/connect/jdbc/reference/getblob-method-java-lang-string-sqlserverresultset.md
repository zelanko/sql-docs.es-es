---
title: "Método getBlob (java.lang.String) (SQLServerResultSet) | Documentos de Microsoft"
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
- SQLServerResultSet.getBlob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9f730d45-b54a-4961-950e-f4447f7225e1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56b49a9516497f629f538421c7af495e057f870f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getblob-method-javalangstring-sqlserverresultset"></a>Método getBlob (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto Blob en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Blob getBlob(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *colName*  
  
 A **cadena** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Blob.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBlob se especifica por getBlob (método) en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Método getBlob &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

