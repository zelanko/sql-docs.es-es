---
title: Método setAutoCommit (SQLServerConnection)
description: Obtenga información sobre los detalles de la API pública para el método setAutoCommit de la clase SQLServerConnection del controlador JDBC para SQL Server.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117fa85e5ec6bdd7d0d37de9fc057dd8127cf42a
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435373"
---
# <a name="setautocommit-method-sqlserverconnection"></a>Método setAutoCommit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el modo de confirmación automática para este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) en el estado determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *value*  
  
 Es **true** cuando se habilita el modo de confirmación automática para la conexión; es **false** cuando se deshabilita.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setAutoCommit especifica este método setAutoCommit en la interfaz java.sql.Connection.  
  
 Si una conexión está en modo de confirmación automática, todas sus instrucciones SQL se ejecutan y confirman como transacciones individuales. De lo contrario, sus instrucciones SQL se agrupan en transacciones que finalizan con una llamada al método [commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) o al método [rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md). De forma predeterminada, las nuevas conexiones están en modo de confirmación automática.  
  
 La confirmación se produce cuando la instrucción se completa o se produce la siguiente ejecución, lo que antes ocurra. Cuando las instrucciones devuelven un objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md), la instrucción se completa cuando se haya recuperado la última fila del conjunto de resultados, o bien cuando se haya cerrado el conjunto de resultados. En casos avanzados, una instrucción única podría devolver varios resultados además de los valores de parámetros de salida. En estos casos, la confirmación se produce cuando se hayan recuperado todos los resultados y valores de parámetros de salida.  
  
 Cuando el modo de confirmación automática es **false**, el controlador JDBC iniciará implícitamente una nueva transacción después de cada confirmación.  
  
> [!NOTE]  
> Si se llama a este método durante una transacción, esta se confirma.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)  
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
