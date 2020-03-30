---
title: La base de datos omite la instrucción de definición de datos dentro de la transacción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.dataDefinitionIgnoredInTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1674fb46-43a7-46d0-9f05-cf993d3bc032
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d1538cc4aaf3e62086f57602b29ce0e61bceb6a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67955207"
---
# <a name="datadefinitionignoredintransactions-method-sqlserverdatabasemetadata"></a>Método dataDefinitionIgnoredInTransactions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos omite una instrucción de definición de datos dentro de una transacción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean dataDefinitionIgnoredInTransactions()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si las instrucciones DDL se omiten en las transacciones. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método dataDefinitionIgnoredInTransactions especifica este método dataDefinitionIgnoredInTransactions en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
