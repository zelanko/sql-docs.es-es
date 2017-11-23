---
title: "Método setAsciiStream (int, java.io.InputStream, int) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerPreparedStatement.setAsciiStream
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 9436c39f-f1a1-484a-a75b-776a72ca70f4
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 420ff08a23435b74150bd4503a13745508585618
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setasciistream-method-int-javaioinputstream-int"></a>Método setAsciiStream (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de parámetro designado para el objeto InputStream determinado con el número especificado de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setAsciiStream(int n,  
                                 java.io.InputStream x,  
                                 int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *n*  
  
 Un **int** que indica el número de parámetro.  
  
 *x*  
  
 Un objeto InputStream.  
  
 *length*  
  
 El número de bytes.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setAsciiStream especificado por el método setAsciiStream en la interfaz java.sql.PreparedStatement.  
  
 Si la longitud de la secuencia es diferente al especificado en el *longitud* parámetro, el controlador JDBC produce una excepción cuando se actualiza o inserta la fila.  
  
 Si la longitud de la secuencia es desconocida, el *longitud* parámetro puede establecerse en -1 para indicar que el controlador debería aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, recomendamos que utilice el método de JDBC 4.0 [setAsciiStream método &#40; int, java.io.InputStream &#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) cuando la aplicación desee actualizar la columna de un flujo cuya longitud se desconozca.  
  
## <a name="see-also"></a>Vea también  
 [Método setAsciiStream &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [Miembros SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
