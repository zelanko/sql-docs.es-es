---
title: "Método setCharacterStream (int, java.io.Reader, long) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cb6ac7f5-81ae-4cb7-87c8-cbee40d278c5
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a8aba37053a3f671feb1b512b1a8e583664c093
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setcharacterstream-method-int-javaioreader-long"></a>Método setCharacterStream (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto java.io.Reader, que es el número especificado de caracteres de longitud.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setCharacterStream(int parameterIndex,  
                                    java.io.Reader reader,  
                                    long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterIndex*  
  
 Un **int** que indica el número de parámetro.  
  
 *lector*  
  
 El objeto java.io.Reader que contiene los datos Unicode.  
  
 *length*  
  
 A **largo** que indica el número de caracteres de la secuencia.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setCharacterStream especificado por el método setCharacterStream en la interfaz java.sql.PreparedStatement.  
  
 Si la longitud de la secuencia es diferente de lo especificado en el *longitud* parámetro, el controlador JDBC produce una excepción cuando se actualiza o inserta la fila.  
  
 Si la longitud de la secuencia es desconocida, el *longitud* parámetro puede establecerse en -1 para indicar que el controlador debería aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, recomendamos que utilice el método de JDBC 4.0 [setCharacterStream método &#40; int, java.io.Reader &#41;](../../../connect/jdbc/reference/setcharacterstream-method-int-java-io-reader.md) cuando la aplicación desee actualizar la columna de un flujo cuya longitud se desconozca.  
  
## <a name="see-also"></a>Vea también  
 [Método setCharacterStream &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)   
 [Miembros SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

