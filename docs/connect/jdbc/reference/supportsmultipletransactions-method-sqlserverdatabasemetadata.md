---
description: Método supportsMultipleTransactions (SQLServerDatabaseMetaData)
title: Método supportsMultipleTransactions (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMultipleTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 34ff8dcb-5487-46d1-a4c1-25e33eb3eee4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e71f854e7eebcb600515314d427dacce0e57f33c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450327"
---
# <a name="supportsmultipletransactions-method-sqlserverdatabasemetadata"></a>Método supportsMultipleTransactions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos permite tener varias transacciones abiertas a la vez en conexiones diferentes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsMultipleTransactions()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsMultipleTransactions especifica este método supportsMultipleTransactions en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
