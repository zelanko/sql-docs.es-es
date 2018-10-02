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
manager: craigg
ms.openlocfilehash: b9030898e71ec13a75da9b91e41f9792d31cce82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798033"
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
 Este método isLast especificado por el método isLast en la interfaz java.sql.ResultSet.  
  
 Si este método se utiliza con cursores de avance y dinámicos, se producirá una excepción.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
