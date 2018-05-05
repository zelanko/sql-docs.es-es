---
title: Método updateAsciiStream (java.io.InputStream, int) | Documentos de Microsoft
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
- SQLServerResultSet.updateAsciiStream (java.lang.String, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4e2997a0-c18e-4114-bce9-0ab4b2b9f92c
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74938db74f72b081e4e1256a1c4e94af43b8fc8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream-int"></a>Método updateAsciiStream (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza el nombre de la columna designada con un valor de flujo ASCII, que tendrá el número especificado de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateAsciiStream(java.lang.String columnName,  
                              java.io.InputStream x,  
                              int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de columna.  
  
 *x*  
  
 Un objeto InputStream.  
  
 *length*  
  
 Un **int** que indica la longitud de la secuencia.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateAsciiStream especificado por el método updateAsciiStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa caracteres ASCII (bytes) de un objeto InputStream a las columnas de caracteres convertibles, que son el rango ASCII [0 x 00 a 0x7F] de Unicode y 874, 932, 936, 949, 950 y desde la 1250 a las páginas de códigos 1258. Este método realiza una conversión en la página de intercalación de destino. Si se intenta actualizar una columna de destino no convertible se producirá una excepción. Para las columnas binarias, se pasan bytes sin formato.  
  
 Si la longitud de la secuencia es diferente al especificado en el *longitud* parámetro, el controlador JDBC produce una excepción cuando se actualiza o inserta la fila.  
  
 Si la longitud de la secuencia es desconocida, el *longitud* parámetro puede establecerse en -1 para indicar que el controlador debería aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, recomendamos que utilice el método de JDBC 4.0 [método updateAsciiStream &#40;java.lang.String, java.io.InputStream&#41; ](../../../connect/jdbc/reference/updateasciistream-method-java-lang-string-java-io-inputstream.md) cuando la aplicación desee actualizar la columna de un flujo cuya longitud es desconocido.  
  
## <a name="see-also"></a>Vea también  
 [Método updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
