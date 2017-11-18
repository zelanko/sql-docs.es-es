---
title: "Método getBinaryStream (int) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.getBinaryStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de22a6c4-1ba3-4ed0-91a2-bf235c2ceec3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1f822af6387e66df4ed6f9a2fba28835220a6156
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getbinarystream-method-int"></a>Método getBinaryStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del índice de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como una secuencia binaria de bytes no interpretados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Un **int** que indica el índice de columna.  
  
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
 [Método getBinaryStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

