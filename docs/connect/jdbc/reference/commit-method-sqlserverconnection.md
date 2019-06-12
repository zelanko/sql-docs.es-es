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
manager: jroth
ms.openlocfilehash: dafb8b3c5016d0be191e06eefb5b5ca80b9ec0de
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777392"
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
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
