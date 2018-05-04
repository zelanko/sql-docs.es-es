---
title: Commit (método) (SQLServerConnection) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42cd2c1d8a189e353d4bfd6bbd2f67b3c14e0df1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="commit-method-sqlserverconnection"></a>Commit (método) (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Hace que todos los cambios realizados desde la anterior confirmación o reversión permanentes y libera los bloqueos de base de datos mantenidos actualmente por este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método de confirmación es especificado por el método commit en la interfaz java.sql.Connection.  
  
 Este método se debería utilizar solamente cuando el modo de confirmación automática esté deshabilitado.  
  
 Observe que este método no se ejecutará correctamente y producirá una excepción si el cliente inicia una transacción manual y, a continuación, por algún motivo, SQL Server revierte la transacción manual. Por ejemplo, se produce una excepción si el cliente llama a un procedimiento almacenado que llame explícitamente a ROLLBACK TRANSACTION y, a continuación, el cliente llama al método commit. Además, si SQL Server genera un error de una gravedad suficiente (16 o más) para revertir el cliente inicia una transacción manual; una llamada subsiguiente al método commit iniciará una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
