---
title: Método commit (SQLServerConnection) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50afbfa25052e0f602c486d011ce666a599372e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923588"
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
  
## <a name="remarks"></a>Observaciones  
 El método commit especifica este método commit en la interfaz java.sql.Connection.  
  
 Este método se debería utilizar solamente cuando el modo de confirmación automática esté deshabilitado.  
  
 Observe que este método no se ejecutará correctamente y producirá una excepción si el cliente inicia una transacción manual y, a continuación, por algún motivo, SQL Server revierte la transacción manual. Por ejemplo, se produce una excepción si el cliente llama a un procedimiento almacenado que llame explícitamente a ROLLBACK TRANSACTION y, a continuación, el cliente llama al método commit. Además, si SQL Server muestra un error con una gravedad suficiente (16 o más) para revertir la transacción manual que inició el cliente, una llamada ulterior al método commit producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
