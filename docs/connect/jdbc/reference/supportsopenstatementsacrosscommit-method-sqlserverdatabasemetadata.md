---
title: Método supportsOpenStatementsAcrossCommit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOpenStatementsAcrossCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e733586c-9222-43cb-92ea-ba474f442a43
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dbc4dfe12daf675f16a632ed5caa8b7b3830ced0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67969084"
---
# <a name="supportsopenstatementsacrosscommit-method-sqlserverdatabasemetadata"></a>Método supportsOpenStatementsAcrossCommit (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos permite mantener instrucciones abiertas en las confirmaciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsOpenStatementsAcrossCommit()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsOpenStatementsAcrossCommit especifica este método supportsOpenStatementsAcrossCommit en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
