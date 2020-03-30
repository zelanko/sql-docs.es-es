---
title: Método getUnicodeStream (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getUnicodeStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e8ea50a3-804a-4752-96e5-eb3d521f93c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be721dad48fae3f83aa720516d0979d9f8ff26df
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978410"
---
# <a name="getunicodestream-method-javalangstring"></a>Método getUnicodeStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de la columna que se ha designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo de caracteres Unicode.  
  
> [!NOTE]  
>  Este método se ha dejado de incluir en las especificaciones de JDBC y si se llama producirá una excepción de no implementación. En su lugar, debería utilizar el método [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.InputStream getUnicodeStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Valor **String** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getUnicodeString especifica este método getUnicodeString en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Método getUnicodeStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
