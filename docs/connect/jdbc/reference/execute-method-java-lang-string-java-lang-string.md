---
title: "Método Execute (java.lang.String, java.lang.String) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dc327a107a8a164e00f2f34f21515c96766e21d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring-javalangstring"></a>Método Execute (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL determinada, que puede devolver varios resultados e indica [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] que las claves generadas automáticamente que se indican en la matriz especificada deben estar disponibles para la recuperación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *SQL*  
  
 A **cadena** que contiene una instrucción SQL.  
  
 *columnNames*  
  
 Una matriz de cadenas que indica que los nombres de columna de las claves que se generaron automáticamente deben estar disponibles.  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el primer resultado es un conjunto de resultados. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método de ejecución especificado por el método execute en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar método &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

