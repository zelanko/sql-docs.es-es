---
title: "Método Position (java.sql.Blob, long) | Documentos de Microsoft"
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
- SQLServerBlob.position (java.sql.Blob.long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7c3f740409e7a8d7a5cbc8989ae8aa074703305
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="position-method-javasqlblob-long"></a>Método position (java.sql.Blob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la posición de un patrón especificado en el BLOB según el patrón determinado y el índice de inicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *patrón*  
  
 El modelo que se va a buscar.  
  
 *Inicio*  
  
 El índice inicial que se va a buscar.  
  
## <a name="return-value"></a>Valor devuelto  
 A **largo** valor de la posición donde se encuentra el patrón, o -1 si no se encontró.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método de posición se especifica el método de posición en la interfaz java.sql.Blob.  
  
## <a name="see-also"></a>Vea también  
 [Coloque el método &#40; SQLServerBlob &#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Miembros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

