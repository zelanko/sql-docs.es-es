---
title: "Método getAsciiStream (SQLServerClob) | Documentos de Microsoft"
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
- SQLServerClob.getAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 134abe5e-5add-4d27-b333-b4b0f4d94c31
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4025d8814415e0889168bba781254a736d504260
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getasciistream-method-sqlserverclob"></a>Método getAsciiStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Materializa el objeto CLOB como un flujo ASCII.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un flujo de entrada que contiene los datos del objeto CLOB.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getAsciiStream especificado por el método getAsciiStream en la interfaz java.sql.Clob.  
  
 Siempre devuelve un flujo de bytes y supone que los datos en el CLOB están en formato ASCII porque no tiene forma alguna de saber si están en Unicode o en cualquier otra página de códigos multibyte.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

