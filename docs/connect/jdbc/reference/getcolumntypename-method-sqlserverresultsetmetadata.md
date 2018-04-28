---
title: Método getColumnTypeName (SQLServerResultSetMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSetMetaData.getColumnTypeName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a444da82-c1af-40a5-9774-02476416c92c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af2724c99dede909ce59aac8bf42938574995cb0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="getcolumntypename-method-sqlserverresultsetmetadata"></a>Método getColumnTypeName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el nombre de tipo específico de la base de datos para la columna designada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getColumnTypeName(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Un **int** que indica el índice de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el nombre del servidor para la columna.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getColumnTypeName especificado por el método getColumnTypeName en la interfaz java.sql.ResultSetMetaData.  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Controlador JDBC 3.0 de incorpora cambios de comportamiento en la columna TYPE_NAME. Vea [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
