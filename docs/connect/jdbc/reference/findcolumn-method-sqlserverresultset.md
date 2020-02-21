---
title: Método findColumn (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.findColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c29994a-0b53-420b-8a9b-82a9eef08587
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24aed500f5b345e2ba3762bdd7a888fc5f8f31ba
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954569"
---
# <a name="findcolumn-method-sqlserverresultset"></a>Método findColumn (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el índice de la primera columna coincidente con el nombre de la columna especificado en este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int findColumn(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Un objeto **String** que contiene el nombre del rol.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **int** que indica el índice de la columna.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método findColumn especifica este método findColumn en la interfaz java.sql.ResultSet.  
  
 Si hay varias columnas con el mismo nombre, el método findColumn devuelve la primera coincidencia con distinción entre mayúsculas y minúsculas. Si no hay coincidencias con distinción entre mayúsculas y minúsculas, este método devuelve la primera coincidencia con distinción entre mayúsculas y minúsculas.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
