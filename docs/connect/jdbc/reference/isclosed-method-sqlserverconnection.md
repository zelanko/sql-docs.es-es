---
title: Método isClosed (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isClosed
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3560ab18-4350-4d02-9716-439f0c2f7142
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 508b3d1fe22ff58e91865204d6b74822ba6f5763
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647635"
---
# <a name="isclosed-method-sqlserverconnection"></a>Método isClosed (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si se ha cerrado este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isClosed()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si la conexión está cerrada, **false** si no lo está.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método isClosed especificado por el método isClosed en la interfaz java.sql.Connection.  
  
 Comprueba el estado del objeto SQLServerConnection llamado. Una conexión está cerrada si se ha llamado en ella al método [close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md) o si se han producido ciertos errores irrecuperables. Este método devolverá el valor **true** solo cuando se ha llamado tras llamar al método close.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
