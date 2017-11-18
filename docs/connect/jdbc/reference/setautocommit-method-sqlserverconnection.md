---
title: "setAutoCommit (método) (SQLServerConnection) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1549693ac6b4e558c2fc86b29dc6aaa6122c235
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setautocommit-method-sqlserverconnection"></a>setAutoCommit (método) (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el modo de confirmación automática para este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto en el estado determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *value*  
  
 **True** para habilitar el modo de confirmación automática para la conexión, **false** para deshabilitarlo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setAutoCommit especificado por el método setAutoCommit en la interfaz java.sql.Connection.  
  
 Si una conexión está en modo de confirmación automática, todas sus instrucciones SQL se ejecutan y confirman como transacciones individuales. De lo contrario, sus instrucciones SQL se agrupan en transacciones que finalizan con una llamada a la [confirmación](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) método o la [reversión](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md) método. De forma predeterminada, las nuevas conexiones están en modo de confirmación automática.  
  
 La confirmación se produce cuando la instrucción se completa o se produce la siguiente ejecución, lo que antes ocurra. En el caso de instrucciones que devuelvan un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto, la instrucción se completa cuando se ha recuperado la última fila del conjunto de resultados, o cuando se ha cerrado el conjunto de resultados. En casos avanzados, una instrucción única podría devolver varios resultados además de los valores de parámetros de salida. En estos casos, la confirmación se produce cuando se hayan recuperado todos los resultados y valores de parámetros de salida.  
  
 Cuando el modo de confirmación automática es **false**, el controlador JDBC iniciará implícitamente una nueva transacción después de cada confirmación.  
  
> [!NOTE]  
>  Si se llama a este método durante una transacción, esta se confirma.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

