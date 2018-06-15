---
title: deleteRow (método) (SQLServerResultSet) | Documentos de Microsoft
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
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd06dec2dccd3e124d702131aa4520a394ecd9fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32830110"
---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Elimina la fila actual de este[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto y de la base de datos subyacente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void deleteRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método deleteRow es especificado por el método deleteRow en la interfaz java.sql.ResultSet.  
  
 No se puede llamar a este método cuando el cursor está en la fila de inserción.  
  
 Al utilizar los cursores del conjunto de claves, este método deja un hueco en el conjunto de resultados. Puede probar este hueco mediante el [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) método. Los números de fila de las filas en el conjunto de resultados no se ven modificados.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
