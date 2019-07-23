---
title: Método supportsExtendedSQLGrammar (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsExtendedSQLGrammar
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8deb1987-c4e3-4599-8e37-0a04ec20b480
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f006c4343c1a89fcb6387bc437a3415607ca094
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969412"
---
# <a name="supportsextendedsqlgrammar-method-sqlserverdatabasemetadata"></a>Método supportsExtendedSQLGrammar (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite la gramática extendida de SQL de ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsExtendedSQLGrammar()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método supportsExtendedSQLGrammer se especifica mediante el método supportsExtendedSQLGrammer en la interfaz java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
