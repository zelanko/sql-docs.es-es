---
title: Método getMaxColumnsInGroupBy (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInGroupBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a59cfe98-c0f4-46ad-9243-62aa56855f1a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d745712e5a8c4b59ea85c1a9b19c2e247c166be3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982303"
---
# <a name="getmaxcolumnsingroupby-method-sqlserverdatabasemetadata"></a>Método getMaxColumnsInGroupBy (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de columnas que esta base de datos permite en una cláusula GROUP BY.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMaxColumnsInGroupBy()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el número máximo permitido de columnas.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getMaxColumnsInGroupBy se especifica mediante el método getMaxColumnsInGroupBy en la interfaz java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
