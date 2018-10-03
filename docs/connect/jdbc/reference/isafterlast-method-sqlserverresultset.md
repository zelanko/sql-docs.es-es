---
title: Método isAfterLast (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isAfterLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19f9d124-3184-4985-8b97-503a8ab8b4f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 874677b8e82ef9129615daed2170757e908f9455
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809873"
---
# <a name="isafterlast-method-sqlserverresultset"></a>Método isAfterLast (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si el cursor está tras la última fila en este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el cursor está después de la última fila. **false** si el cursor está en cualquier otra posición o si el conjunto de resultados no contiene ninguna fila.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método isAfterLast especificado por el método isAfterLast en la interfaz java.sql.ResultSet.  
  
 Si este método se utiliza con cursores dinámicos, incluso los de solo avance y solo lectura, y la propiedad de conexión selectMethod se ha establecido para el "cursor", se producirá una excepción.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
