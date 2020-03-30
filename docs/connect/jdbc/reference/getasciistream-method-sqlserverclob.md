---
title: Método getAsciiStream (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 134abe5e-5add-4d27-b333-b4b0f4d94c31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dfa7ed5314d75ba0bec0d2a000575e8d9ed4d3fc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954135"
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
  
## <a name="remarks"></a>Observaciones  
 El método getAsciiStream especifica este método getAsciiStream en la interfaz java.sql.Clob.  
  
 Siempre devuelve un flujo de bytes y supone que los datos en el CLOB están en formato ASCII porque no tiene forma alguna de saber si están en Unicode o en cualquier otra página de códigos multibyte.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
