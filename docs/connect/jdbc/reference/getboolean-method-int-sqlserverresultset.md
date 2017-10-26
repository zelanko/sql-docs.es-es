---
title: "Método getBoolean (int) (SQLServerResultSet) | Documentos de Microsoft"
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
- SQLServerResultSet.getBoolean (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 50fcc0c3-36a1-47b2-b18c-7aa2ac9b27d3
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ca9e68e4feaea59103a494f696a87658d4077f1a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getboolean-method-int-sqlserverresultset"></a>Método getBoolean (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del índice de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **booleano** en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getBoolean(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Un **int** que indica el índice de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 A **booleano** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBoolean es especificado por el método getBoolean en la interfaz java.sql.ResultSet.  
  
 Este método se admite únicamente en los tipos de datos numéricos y de caracteres. Convierte valores "1", 1, y "**true**" a **true**y los valores "0", 0, y "**false**" a **false**. Para el resto de los valores no se ha definido el comportamiento.  
  
## <a name="see-also"></a>Vea también  
 [Método getBoolean &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

