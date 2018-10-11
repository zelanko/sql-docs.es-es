---
title: Método Commit (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6350dc135971f2f7d37154d4728c5d4922954047
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819423"
---
# <a name="commit-method-sqlserverconnection"></a>Método commit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Realiza todos los cambios efectuados desde la confirmación anterior o realiza una reversión permanente y libera los bloqueos de la base de datos que incorpore este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) en esos momentos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método commit especifica este método commit en la interfaz java.sql.Connection.  
  
 Este método se debería utilizar solamente cuando el modo de confirmación automática esté deshabilitado.  
  
 Observe que este método no se ejecutará correctamente y producirá una excepción si el cliente inicia una transacción manual y, a continuación, por algún motivo, SQL Server revierte la transacción manual. Por ejemplo, se produce una excepción si el cliente llama a un procedimiento almacenado que llame explícitamente a ROLLBACK TRANSACTION y, a continuación, el cliente llama al método commit. Además, si SQL Server muestra un error con una gravedad suficiente (16 o más) para revertir la transacción manual que inició el cliente, una llamada ulterior al método commit producirá una excepción.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
