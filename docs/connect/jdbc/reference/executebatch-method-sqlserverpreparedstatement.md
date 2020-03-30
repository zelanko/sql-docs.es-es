---
title: Método executeBatch (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 463106c14a63feddb68998affff8131933e81dfa
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954898"
---
# <a name="executebatch-method-sqlserverpreparedstatement"></a>Método executeBatch (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Envía un lote de comandos a la base de datos para que se ejecute. Si todos los comandos se ejecutan correctamente, devuelve una matriz de recuentos de actualizaciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Una matriz de ints que contiene los recuentos de la actualización.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Observaciones  
 El método executeBatch especifica este método executeBatch en la interfaz java.sql.Statement.  
    
 Este método invalida [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
