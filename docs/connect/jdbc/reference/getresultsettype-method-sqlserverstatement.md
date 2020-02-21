---
title: Método getResultSetType (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResultSetType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 260da35f-ddf6-4111-8519-69956ea3072e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7a0293a48a354bba911a11ecf91a17211a9f8a12
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980301"
---
# <a name="getresultsettype-method-sqlserverstatement"></a>Método getResultSetType (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el tipo del conjunto de resultados para los objetos [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que haya generado este objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getResultSetType()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el tipo de conjunto de resultados.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getResultSetType especifica este método getResultSetType en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
