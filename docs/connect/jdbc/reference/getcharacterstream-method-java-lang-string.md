---
title: "Método getCharacterStream (java.lang.String) | Documentos de Microsoft"
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
- SQLServerResultSet.getCharacterStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cdddc572-05c1-480d-b3e5-28270001575c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a882e903e689f67db7adf9b8d71d34851affd5b4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-javalangstring"></a>Método getCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto java.io.Reader.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Reader getCharacterStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getCharacterStream especificado por el método getCharacterStream en la interfaz java.sql.ResultSet.  
  
 Este método leerá solo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de datos de caracteres Unicode como nchar, nvarchar, nvarchar (max) y ntext. El resto de tipos de datos, incluso los tipos de carácter ASCII, producirán una excepción. Para leer los tipos de datos ASCII, utilice la [getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Vea también  
 [Método getCharacterStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

