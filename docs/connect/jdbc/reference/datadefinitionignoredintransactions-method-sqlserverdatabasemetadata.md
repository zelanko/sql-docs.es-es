---
title: Base de datos hace caso omiso instrucción de definición de datos dentro de transacción | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: fda0e082d8f0f35995e622f7f3a47b0a075f9eee
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772834"
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
  
## <a name="remarks"></a>Notas  
 Este método dataDefinitionIgnoredInTransactions especificado por el método dataDefinitionIgnoredInTransactions en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
