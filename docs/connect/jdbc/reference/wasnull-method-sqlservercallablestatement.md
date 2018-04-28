---
title: Método wasNull (SQLServerCallableStatement) | Documentos de Microsoft
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
ms.topic: article
apiname:
- SQLServerCallableStatement.wasNull
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a27b2fe-ae12-46a9-9bca-2c5ca66b9eb3
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58802bc194081fbedbb94edd9cafae8a24122443
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="wasnull-method-sqlservercallablestatement"></a>Método wasNull (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si la última lectura del parámetro OUT incorporaba el valor de NULL de SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean wasNull()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el último parámetro lee era null. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método wasNull especificado por el método wasNull en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
