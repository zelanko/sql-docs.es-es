---
title: Método Relative (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b8907a5e2eb2ead5202e8aec9fd5320a6047a5f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797708"
---
# <a name="relative-method-sqlserverresultset"></a>Método relative (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Mueve el cursor tantas filas como se hayan indicado, con respecto a la fila actual, tanto en una posición positiva como en una negativa.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *nRows*  
  
 Un valor**int** que indica el número de filas que se van a mover.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si el cursor está en una fila. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método relativo especificado por el método relativo en la interfaz java.sql.ResultSet.  
  
 Al intentar desplazarse más allá de la primera o última fila del conjunto de resultados, el cursor se posiciona antes o después de esta primera o última fila. Llamar a `relative(0)` es válido, pero no cambia la posición del cursor.  
  
 Llamar al método `relative(1)` es igual que llamar al método [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md). Llamar al método `relative(-1)` es igual que llamar al método [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
