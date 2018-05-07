---
title: insertRow (método) (SQLServerResultSet) | Documentos de Microsoft
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
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 106743625ef17e733836ec9430f2f171af2b0d72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Agrega el contenido de la fila de inserción a este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto y a la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método insertRow es especificado por el método insertRow en la interfaz java.sql.ResultSet.  
  
 Cuando se llama a este método, el cursor debe estar en la fila de inserción. Una vez se llame a este método, el cursor permanece en la fila de inserción y el conjunto de resultados permanece en modo de inserción.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
