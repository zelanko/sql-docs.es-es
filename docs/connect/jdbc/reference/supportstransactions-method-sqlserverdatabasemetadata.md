---
title: Método supportsTransactions (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 57d28ee5-c2f6-4740-b42d-cead1aade809
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6ecfa9d1c43244967030284a5fd034d522583b0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842533"
---
# <a name="supportstransactions-method-sqlserverdatabasemetadata"></a>Método supportsTransactions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite transacciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsTransactions()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método supportsTransactions especificado por el método supportsTransactions en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
