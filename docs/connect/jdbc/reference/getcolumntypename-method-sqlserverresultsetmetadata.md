---
title: Método getColumnTypeName (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnTypeName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a444da82-c1af-40a5-9774-02476416c92c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 72d51d7830cdcdb14208550974fe432a48a67b1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66763266"
---
# <a name="getcolumntypename-method-sqlserverresultsetmetadata"></a>Método getColumnTypeName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el nombre del tipo específico de base de datos de la columna designada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getColumnTypeName(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto **String** que contiene el nombre de servidor de la columna.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getColumnTypeName especificado por el método getColumnTypeName en la interfaz java.sql.ResultSetMetaData.  
  
 El controlador JDBC 3.0 de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene cambios de comportamiento en la columna TYPE_NAME. Vea [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md) para más información.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
