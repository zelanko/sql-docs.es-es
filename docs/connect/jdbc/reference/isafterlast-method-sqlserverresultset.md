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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8542c6a2dc87e1f0d52049b27446acf2c1f909de
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909861"
---
# <a name="isafterlast-method-sqlserverresultset"></a>Método isAfterLast (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si el cursor está tras la última fila en este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si el cursor está después de la última fila. **false** si el cursor está en cualquier otra posición o si el conjunto de resultados no contiene filas.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método isAfterLast especifica este método isAfterLast en la interfaz java.sql.ResultSet.  
  
 Si este método se utiliza con cursores dinámicos, incluso los de solo avance y solo lectura, y la propiedad de conexión selectMethod se ha establecido para el "cursor", se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
