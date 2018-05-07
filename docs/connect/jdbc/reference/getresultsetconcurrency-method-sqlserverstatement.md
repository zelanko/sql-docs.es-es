---
title: Método (SQLServerStatement) getResultSetConcurrency | Documentos de Microsoft
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
- SQLServerStatement.getResultSetConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 47ef6547-5ec7-4cf5-a4d4-e34cbeec72eb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06f0348d631bcfaad6fb712ac51c1ec6ac84f73e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getresultsetconcurrency-method-sqlserverstatement"></a>getResultSetConcurrency (método) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el conjunto de resultados de simultaneidad para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que haya generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getResultSetConcurrency()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el tipo de simultaneidad del conjunto de lo resultados.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getResultSetConcurrency especificado por el método getResultSetConcurrency en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
