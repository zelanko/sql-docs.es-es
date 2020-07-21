---
title: Método updateAsciiStream (java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 143bff3e-2b5c-485d-9529-1c2387560094
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 889e7e6b14299a924c999bc2141d24dbfb88dfd7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926029"
---
# <a name="updateasciistream-method-int-javaioinputstream-long"></a>Método updateAsciiStream (int, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo ASCII, que tendrá el número especificado de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateAsciiStream(int columnIndex,  
                              java.io.InputStream x,  
                              long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
 *x*  
  
 Un objeto InputStream.  
  
 *length*  
  
 Longitud del flujo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateAsciiStream especifica este método updateAsciiStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa caracteres ASCII (bytes) desde un objeto InputStream a las columnas de caracteres convertibles, que son el rango ASCII [0x00 - 0x7F] de Unicode y las páginas de códigos 874, 932, 936, 949, 950 y desde la 1250 a la 1258. Este método realiza una conversión en la página de intercalación de destino. Si se intenta actualizar una columna de destino no convertible se producirá una excepción. Para las columnas binarias, se pasan bytes sin formato.  
  
 Si la longitud del flujo es distinta a la especificada en el parámetro *length*, el controlador JDBC produce una excepción cuando la fila se actualiza o se inserta.  
  
 Si se desconoce la longitud del flujo, el parámetro *length* puede establecerse en -1 para indicar que el controlador debe aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, se recomienda usar el [Método updateAsciiStream &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/updateasciistream-method-int-java-io-inputstream.md) de JDBC 4.0 si la aplicación quiere actualizar la columna a partir de un flujo cuya longitud se desconoce.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
