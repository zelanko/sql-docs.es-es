---
title: "Método Absolute (SQLServerResultSet) | Documentos de Microsoft"
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
apiname: SQLServerResultSet.absolute
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b38ee28be85be9f91e334f58c51a21e17931a5ac
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="absolute-method-sqlserverresultset"></a>Método Absolute (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Mueve el cursor a la fila especificada en este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *fila*  
  
 Un **int** que indica el número de fila para mover a. Puede ser positivo, negativo o 0.  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el cursor se mueve a la posición especificada. **false** si es antes de la primera fila o después de la última fila.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método absoluta se especifica mediante el método absoluto en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
