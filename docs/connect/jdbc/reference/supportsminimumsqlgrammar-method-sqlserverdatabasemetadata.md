---
description: Método supportsMinimumSQLGrammar (SQLServerDatabaseMetaData)
title: Método supportsMinimumSQLGrammar (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMinimumSQLGrammar
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 40f5d727-1ce7-414d-867d-589ead7b2a29
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c663d4a6104cf503901640e9e019bf06c1d5d37c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467017"
---
# <a name="supportsminimumsqlgrammar-method-sqlserverdatabasemetadata"></a>Método supportsMinimumSQLGrammar (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite la gramática mínima de SQL de ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsMinimumSQLGrammar()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsMinimumSQLGrammer especifica este método supportsMinimumSQLGrammer en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
