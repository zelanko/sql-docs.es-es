---
title: "Método getBytes (SQLServerBlob) | Documentos de Microsoft"
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
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f1139f0deb886265da6c7c56e682372155a0e3b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-sqlserverblob"></a>Método getBytes (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtiene los datos Blob como una matriz de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public byte[] getBytes(long pos,  
                       int length)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *punto de venta*  
  
 Posición inicial; comienza en 1 (no en 0).  
  
 *length*  
  
 Longitud de los datos que se van a obtener.  
  
## <a name="return-value"></a>Valor devuelto  
 A **bytes** matriz que contiene los datos solicitados.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBytes es especificado por el método getBytes en la interfaz java.sql.Blob.  
  
 Si tiene un valor null o tiene longitud cero BLOB e intentan obtener cero bytes exactamente en la posición 1, vacío **bytes** se devuelve la matriz (matriz de bytes de longitud 0).  
  
 Si el valor del objeto BLOB es NULL o tiene longitud cero y se intenta obtener una longitud de bytes determinada en una posición que no sea 1, se producirá una excepción relativa a la posición.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

