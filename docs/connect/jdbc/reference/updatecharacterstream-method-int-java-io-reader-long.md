---
title: "Método (java.io.Reader, long) updateCharacterStream | Documentos de Microsoft"
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
ms.assetid: c426b0e3-2f9d-425a-b7da-1d0325e292d1
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a7e5d785e80cbeaf9cf257bf74678b9de7b83c8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="updatecharacterstream-method-int-javaioreader-long"></a>Método updateCharacterStream (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo de caracteres, que tendrá el número de caracteres especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x,  
                                  long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Un **int** que indica el índice de columna.  
  
 *x*  
  
 Un objeto de lector.  
  
 *length*  
  
 Longitud del flujo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateCharacterStream especificado por el método updateCharacterStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa los caracteres Unicode de un objeto de lector al texto seleccionado y las columnas binarias. Esto incluye todas las columnas de texto y binarias como, varbinary, varbinary(max), image y XML, pero no las UDT.  
  
 Si la longitud de la secuencia es diferente de lo especificado en el *longitud* parámetro, el controlador JDBC produce una excepción cuando se actualiza o inserta la fila.  
  
 Si la longitud de la secuencia es desconocida, el *longitud* parámetro puede establecerse en -1 para indicar que el controlador debería aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, recomendamos que utilice el método de JDBC 4.0 [updateCharacterStream método &#40; int, java.io.Reader &#41;](../../../connect/jdbc/reference/updatecharacterstream-method-int-java-io-reader.md) cuando la aplicación desee actualizar la columna de un flujo cuya longitud se desconozca.  
  
## <a name="see-also"></a>Vea también  
 [Método updateCharacterStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
