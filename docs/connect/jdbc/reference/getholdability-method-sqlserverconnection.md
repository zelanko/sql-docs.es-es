---
title: Método getHoldability (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b1644791-c36a-4837-86c4-9299537ee1c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f7dfc9609443febe545bd3b6ac7a6cdf75e1756
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982931"
---
# <a name="getholdability-method-sqlserverconnection"></a>Método getHoldability (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la capacidad de alojamiento actual de los objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que se crean mediante el uso del objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que contiene uno de los siguientes niveles capacidad de alojamiento:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setHoldability especifica este método setHoldability en la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
