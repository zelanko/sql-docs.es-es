---
title: Método isLast (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85d4451f-6392-470e-ab21-78a495b45792
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dab78e0f48f2bb7debcf5d993dfb128388a42506
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796514"
---
# <a name="islast-method-sqlserverresultset"></a>Método isLast (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si el cursor está en la última fila de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isLast()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el cursor está en la última fila. **false** si el cursor está en cualquier otra posición o si el conjunto de resultados no contiene ninguna fila.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método isLast se especifica en el método isLast en la interfaz java.sql.ResultSet.  
  
 Si este método se utiliza con cursores de avance y dinámicos, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
