---
title: "Método getAsciiStream (SQLServerClob) | Documentos de Microsoft"
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
apiname: SQLServerClob.getAsciiStream
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 134abe5e-5add-4d27-b333-b4b0f4d94c31
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6cbaa7a53b77cfaaaa1ebbe19a88da0c8576a553
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
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
  
  
