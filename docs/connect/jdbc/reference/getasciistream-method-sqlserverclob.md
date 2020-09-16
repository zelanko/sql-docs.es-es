---
description: Método getAsciiStream (SQLServerClob)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27a934e014b1b6045ead64e39759c665197f87bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437397"
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
  
  
