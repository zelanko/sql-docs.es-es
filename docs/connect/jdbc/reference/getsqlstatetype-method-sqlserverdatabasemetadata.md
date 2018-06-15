---
title: Método getSQLStateType (SQLServerDatabaseMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d5778b2b42af466ced101633a38ac9d0db83791
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838260"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>Método getSQLStateType (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si SQLSTATE, que devolvió el método SQLException.getSQLState, es X/Open (ahora se denomina Open Group), SQL CLI, SQL99 (JDBC 3.0) o SQL:2003 (JDBC 4.0).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el tipo de SQLSTATE, que puede ser uno de los siguientes valores:  
  
-   Para la versión 5.0 de Java Runtime Environment: si la **xopenStates** propiedad de conexión se establece en **true**, este método devuelve DatabaseMetaData.sqlStateXOpen. En caso contrario, DatabaseMetaData.sqlStateSQL99.  
  
-   Para la versión 6.0 de Java Runtime Environment: si la **xopenStates** propiedad de conexión se establece en **true**, este método devuelve DatabaseMetaData.sqlStateXOpen. En caso contrario, DatabaseMetaData.sqlStateSQL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getSQLStateType especificado por el método getSQLStateType en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
