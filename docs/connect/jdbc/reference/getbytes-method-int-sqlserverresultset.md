---
title: "Método getBytes (int) (SQLServerResultSet) | Documentos de Microsoft"
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
- SQLServerResultSet.getBytes (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1385d7d4-9288-4cbd-8606-4b919e9b07b2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7b9185349b2ce7332c1a5f9478db0a01253dc136
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-int-sqlserverresultset"></a>Método getBytes (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del índice de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **bytes** matriz en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public byte[] getBytes(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Un **int** que indica el índice de columna.  
  
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
  
  

