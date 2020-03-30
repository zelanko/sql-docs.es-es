---
title: Método supportsOpenCursorsAcrossCommit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOpenCursorsAcrossCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b7eed108-64cc-4be6-b297-8af6c1e3dc72
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 264f61c744be0ffc614ca3f45e5268715c680ed8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67969100"
---
# <a name="supportsopencursorsacrosscommit-method-sqlserverdatabasemetadata"></a>Método supportsOpenCursorsAcrossCommit (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos permite mantener cursores abiertos en las confirmaciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsOpenCursorsAcrossCommit()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsOpenCursorsAcrossCommit especifica este método supportsOpenCursorsAcrossCommit en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
