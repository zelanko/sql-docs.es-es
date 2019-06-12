---
title: Método supportsMultipleResultSets (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMultipleResultSets
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb4d0b91-db1d-4a6f-a87c-8ea125215afc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c6abf07e5ff18fba6fd68e8c109388f82bc5eae4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764142"
---
# <a name="supportsmultipleresultsets-method-sqlserverdatabasemetadata"></a>Método supportsMultipleResultSets (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite recibir varios objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) a partir de una llamada única al método [execute](../../../connect/jdbc/reference/execute-method.md) de la clase [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsMultipleResultSets()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método supportsMultipleResultSets especificado por el método supportsMultipleResultSets en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
