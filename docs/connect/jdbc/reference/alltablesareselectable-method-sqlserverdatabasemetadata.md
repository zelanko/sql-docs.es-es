---
title: Método allTablesAreSelectable (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.allTablesAreSelectable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb340450-45a7-49c8-84bc-1b9dd5ee842f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2fa61d7239858cb3479e7eeaa730e4197bf6bc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955862"
---
# <a name="alltablesareselectable-method-sqlserverdatabasemetadata"></a>Método allTablesAreSelectable (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si el usuario actual tiene los permisos para utilizar todas las tablas que devuelve el método [getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) en una instrucción SELECT.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean allTablesAreSelectable()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si el usuario tiene los permisos para llamar a la utilización de todas las tablas. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método allTablesAreSelectable se especifica mediante el método allTablesAreSelectable en la interfaz java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
