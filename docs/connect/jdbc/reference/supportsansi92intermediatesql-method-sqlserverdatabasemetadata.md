---
title: Método supportsANSI92IntermediateSQL (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsANSI92IntermediateSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d6e8301-0633-4565-91c6-a80910954461
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fab9580485a4eab7ebb4967b4f8461c7dbc098e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969795"
---
# <a name="supportsansi92intermediatesql-method-sqlserverdatabasemetadata"></a>Método supportsANSI92IntermediateSQL (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite la gramática de SQL intermedia de ANSI92.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsANSI92IntermediateSQL()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método supportsANSI92IntermediateSQL se especifica mediante el método supportsANSI92IntermediateSQL en la interfaz java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
