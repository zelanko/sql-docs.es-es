---
title: Método updateBlob (java.lang.String, java.io.InputStream, long) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 40f75549-5d5a-4de3-a271-4b8f0dd7b124
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d2c40def2946bac84b59f7e6c96682fa0d04d8a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="updateblob-method-javalangstring-javaioinputstream-long"></a>Método updateBlob (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada mediante el flujo de entrada especificado, que tendrá el número especificado de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
                                              long length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 A **cadena** que contiene la etiqueta de columna.  
  
 *inputStream*  
  
 Un objeto InputStream.  
  
 *length*  
  
 A **largo** que indica la longitud de la secuencia.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateBlob especificado por el método updateBlob en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Método updateBlob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
