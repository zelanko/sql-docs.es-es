---
title: Método Relative (SQLServerResultSet) | Documentos de Microsoft
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
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e1c976ab8f89e18d6a86fb7d06a144a72dbe66
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="relative-method-sqlserverresultset"></a>Método Relative (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Mueve el cursor la cantidad dada de filas, con respecto a la fila actual, en la vista una dirección positiva o negativa.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *nRows*  
  
 Un **int** que indica el número de filas que se va a mover.  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el cursor está en una fila. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método relativa es especificado por el método relativo en la interfaz java.sql.ResultSet.  
  
 Al intentar desplazarse más allá de la primera o última fila del conjunto de resultados, el cursor se posiciona antes o después de esta primera o última fila. Una llamada a `relative(0)` es válido, pero no cambia la posición del cursor.  
  
 Llamar al método `relative(1)` equivale a llamar a la [siguiente](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) método. Llamar al método `relative(-1)` equivale a llamar a la [anterior](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
