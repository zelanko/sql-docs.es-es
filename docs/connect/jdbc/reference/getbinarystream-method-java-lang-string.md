---
title: Método getBinaryStream (java.lang.String) | Documentos de Microsoft
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
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3054c8af398a2158b9fd779c668593ee7dc86fde
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getbinarystream-method-javalangstring"></a>Método getBinaryStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como una secuencia binaria de bytes no interpretados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBinaryStream especificado por el método getBinaryStream en la interfaz java.sql.ResultSet.  
  
 Este método puede utilizarse solo con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de datos de binary, varbinary, varbinary (max) e image. Si se intenta utilizar con cualquier otro tipo de datos, provocará una excepción.  
  
 Una vez que este método obtenga el valor como un flujo, el valor se puede leer en fragmentos desde el flujo. Este método es particularmente conveniente para recuperar valores LONGVARBINARY grandes.  
  
> [!NOTE]  
>  Todos los datos en el flujo devuelto se deben leer antes de obtener el valor de cualquier otra columna. La llamada siguiente a un método de captador cierra el flujo implícitamente. Además, una secuencia puede devolver 0 cuando se llama al método InputStream.available, si hay datos disponibles o no.  
  
## <a name="see-also"></a>Vea también  
 [Método getBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
