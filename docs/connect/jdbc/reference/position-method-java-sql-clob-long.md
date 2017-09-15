---
title: "Método Position (java.sql.Clob, long) | Documentos de Microsoft"
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
- SQLServerClob.position (java.sql.Clob, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2fb34d5-1d34-4764-a795-712d9c6aa313
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dc0e364f962206b701fd00219f0f6eb7b46a849
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="position-method-javasqlclob-long"></a>Método position (java.sql.Clob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la posición de un carácter del objeto CLOB especificado en el CLOB según la posición de inicio determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public long position(java.sql.Clob searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *searchstr*  
  
 Subcadena para buscar.  
  
 *Inicio*  
  
 La posición donde se empieza la búsqueda. La primera posición es 1.  
  
## <a name="return-value"></a>Valor devuelto  
 La posición donde aparece la subcadena o -1 si no está presente. La primera posición es 1.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método de posición se especifica el método de posición en la interfaz java.sql.Clob.  
  
## <a name="see-also"></a>Vea también  
 [Coloque el método &#40; SQLServerClob &#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
