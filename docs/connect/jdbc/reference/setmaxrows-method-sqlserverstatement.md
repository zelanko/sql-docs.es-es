---
title: "Método setMaxRows (SQLServerStatement) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.setMaxRows
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b35a8295c8dda7c56ed20d38f47e5b5740ef0fe
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setmaxrows-method-sqlserverstatement"></a>Método setMaxRows (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el límite para el número máximo de filas que cualquier [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto puede contener el número determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *max*  
  
 Un **int** que indica el número máximo de filas, o 0 si no hay ningún límite.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setMaxRows especificado por el método setMaxRows en la interfaz java.sql.Statement.  
  
 Este método setMaxRows no tiene ningún efecto para los cursores desplazables dinámicos. La aplicación debería utilizar la sintaxis SELECT TOP N de SQL para limitar el número de filas que devuelven los conjuntos de resultados potencialmente de gran tamaño.  
  
 Cuando se llama al método setMaxRows, la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ejecuta la instrucción SQL SET ROWCOUNT cuando ejecuta consultas de la aplicación. Esto hace que el controlador JDBC limitar el número máximo de filas afectadas por todos los [!INCLUDE[tsql](../../../includes/tsql_md.md)] instrucciones ejecutadas por esa consulta, no solo el número de filas devueltas por la consulta. Si la aplicación debe establecer un límite en el nivel superior [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto, deben usar la sintaxis SELECT TOP N SQL en la consulta en lugar del método setMaxRows.  
  
 Para obtener más información acerca de la instrucción SQL SET ROWCOUNT, vea el "[SET ROWCOUNT (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)" tema en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
