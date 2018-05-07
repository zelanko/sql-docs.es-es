---
title: Método setCharacterStream (java.lang.String, java.io.Reader, long) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 54fb2f13-f8d8-47b5-bec1-4a5af3e86a84
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4253de4038b1505a3befdbbf80f47c9f210735ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-javalangstring-javaioreader-long"></a>Método setCharacterStream (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto java.io.Reader especificado, que es el número especificado de caracteres de longitud.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *lector*  
  
 Un objeto de lector que contiene los datos Unicode.  
  
 *length*  
  
 A **largo** que indica el número de caracteres de la secuencia.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setCharacterStream especificado por el método setCharacterStream en la interfaz java.sql.CallableStatement.  
  
 Si la longitud de la secuencia es diferente de lo especificado en el *longitud* parámetro, el controlador JDBC produce una excepción cuando se actualiza o inserta la fila.  
  
 Si la longitud de la secuencia es desconocida, el *longitud* parámetro puede establecerse en -1 para indicar que el controlador debería aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, recomendamos que utilice el método de JDBC 4.0 [método setCharacterStream (java.lang.String, java.io.Reader)](../../../connect/jdbc/reference/setcharacterstream-method-java-lang-string-java-io-reader.md) cuando la aplicación desee actualizar la columna de un flujo cuya longitud se desconozca.  
  
## <a name="see-also"></a>Vea también  
 [Método setCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
