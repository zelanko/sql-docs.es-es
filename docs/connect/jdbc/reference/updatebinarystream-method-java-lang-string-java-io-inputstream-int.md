---
title: "Método updateBinaryStream (java.io.InputStream, int) | Documentos de Microsoft"
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
- SQLServerResultSet.updateBinaryStream (java.lang.String, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9be246a7-85fa-49fc-ad79-aabe97f5b280
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e1199bdd667e4b24c39f987a37f48f841176ae05
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-int"></a>Método updateBinaryStream (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo binario, que tendrá el número especificado de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 AStringthat contiene la etiqueta de columna.  
  
 *x*  
  
 Un objeto InputStream.  
  
 *length*  
  
 Un **int** que indica la longitud de la secuencia.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateBinaryStream especificado por el método updateBinaryStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa bytes desde un objeto InputStream que seleccione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] columnas binarias como binary, varbinary, varbinary (max), image, xml y udt. Este método no admite la actualización de columnas de caracteres. Para actualizar las columnas de caracteres con un InputStream, use la [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) método.  
  
 Si la longitud de la secuencia es diferente al especificado en el *longitud* parámetro, el controlador JDBC produce una excepción cuando se actualiza o inserta la fila.  
  
 Si la longitud de la secuencia es desconocida, el *longitud* parámetro puede establecerse en -1 para indicar que el controlador debería aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, recomendamos que utilice el método de JDBC 4.0 [updateBinaryStream método &#40;java.lang.String, java.io.InputStream &#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md) cuando la aplicación desee actualizar la columna de un flujo cuya longitud es desconocido.  
  
## <a name="see-also"></a>Vea también  
 [Método updateBinaryStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
