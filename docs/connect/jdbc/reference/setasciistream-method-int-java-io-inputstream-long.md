---
title: Método setAsciiStream (int, java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9dfa7781-d72f-407a-a8d4-1c78c9446d09
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3ef4131bb99ab2569e4e91436174a481ecdb63d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66765227"
---
# <a name="setasciistream-method-int-javaioinputstream-long"></a>Método setAsciiStream (int, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número del parámetro designado para el objeto java.io.InputStream especificado con el número indicado de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x,  
                                    long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterIndex*  
  
 Valor **int** que indica el número de parámetro.  
  
 *x*  
  
 Un objeto java.io.InputStream.  
  
 *length*  
  
 Un valor **long** que indica el número de bytes.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setAsciiStream especificado por el método setAsciiStream en la interfaz java.sql.PreparedStatement.  
  
 Si la longitud del flujo es distinta a la especificada en el parámetro *length*, el controlador JDBC produce una excepción cuando la fila se actualiza o se inserta.  
  
 Si se desconoce la longitud del flujo, el parámetro *length* puede establecerse en -1 para indicar que el controlador debe aceptar el flujo independientemente de su longitud. Con sqljdbc4.jar, se recomienda usar el [Método setAsciiStream &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) de JDBC 40 si la aplicación quiere actualizar la columna a partir de un flujo cuya longitud se desconoce.  
  
## <a name="see-also"></a>Consulte también  
 [Método setAsciiStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [Miembros SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
