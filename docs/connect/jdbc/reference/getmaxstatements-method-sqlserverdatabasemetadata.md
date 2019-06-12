---
title: Método getMaxStatements (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxStatements
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 71d58431-b671-49c5-939a-f581d1fef7cd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 171ed64402b2d7b1dabd565086f8602afec948f6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792417"
---
# <a name="getmaxstatements-method-sqlserverdatabasemetadata"></a>Método getMaxStatements (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de instrucciones activas que se pueden abrir para esta base de datos al mismo tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMaxStatements()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el número máximo de instrucciones activas permitidas.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getMaxStatements especificado por el método getMaxStatements en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
