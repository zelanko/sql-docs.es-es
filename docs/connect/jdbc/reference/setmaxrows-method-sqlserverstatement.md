---
title: Método setMaxRows (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 223abdf54e5af3e92d0ab1c172ae1f5d1f5b9bf9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645593"
---
# <a name="setmaxrows-method-sqlserverstatement"></a>Método setMaxRows (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el límite del número máximo de filas que cualquier objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) puede contener para el número determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *max*  
  
 Valor **int** que indica el número máximo de filas o 0 si no hay ningún límite.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setMaxRows especificado por el método setMaxRows en la interfaz java.sql.Statement.  
  
 Este método setMaxRows no tiene ningún efecto en el caso de los cursores desplazables y dinámicos. La aplicación debería utilizar la sintaxis SELECT TOP N de SQL para limitar el número de filas que devuelven los conjuntos de resultados potencialmente de gran tamaño.  
  
 Cuando se llama al método setMaxRows, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ejecuta la instrucción SET ROWCOUNT SQL cuando ejecuta la consulta de la aplicación. Esto hace que el controlador JDBC limite el número máximo de filas que se verán afectadas por todas las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] ejecutadas por esa consulta, no simplemente el número de filas que devuelve esa consulta. Si la aplicación necesita establecer un límite solamente en el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de nivel superior, debería utilizar la sintaxis de SQL SELECT TOP N en la consulta, en vez del método setMaxRows.  
  
 Para más información sobre la instrucción SQL SET ROWCOUNT, vea el tema "[SET ROWCOUNT (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
