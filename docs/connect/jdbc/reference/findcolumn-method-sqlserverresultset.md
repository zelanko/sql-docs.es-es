---
title: "findColumn (método) (SQLServerResultSet) | Documentos de Microsoft"
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
- SQLServerResultSet.findColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c29994a-0b53-420b-8a9b-82a9eef08587
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e2ce20105ebb38f579cbc28b68cd83fd2010116
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="findcolumn-method-sqlserverresultset"></a>findColumn (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el índice de la primera columna de búsqueda de coincidencias para el nombre de columna especificado en este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int findColumn(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el índice de columna.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método findColumn especificado por el método findColumn en la interfaz java.sql.ResultSet.  
  
 Si hay varias columnas con el mismo nombre, el método findColumn devuelve a la primera coincidencia distingue mayúsculas de minúsculas. Si no hay coincidencias con distinción entre mayúsculas y minúsculas, este método devuelve la primera coincidencia con distinción entre mayúsculas y minúsculas.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
