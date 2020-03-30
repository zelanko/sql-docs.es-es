---
title: Método getDefaultTransactionIsolation (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDefaultTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85b867ed-de5a-4879-b3f8-bce897879077
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e2349dbe193834385869f86f87fe4284a967284
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67983691"
---
# <a name="getdefaulttransactionisolation-method-sqlserverdatabasemetadata"></a>Método getDefaultTransactionIsolation (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el nivel de aislamiento de transacción predeterminado de esta base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getDefaultTransactionIsolation()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **int** que indica el nivel de aislamiento de transacción predeterminado.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Este método getDefaultTransactionIsolation se especifica mediante el método getDefaultTransactionIsolation en la interfaz java.sql.DatabaseMetaData.  
  
 Cuando se usa el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método devuelve un valor TRANSACTION_READ_COMMITTED o el valor **int** 2.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
