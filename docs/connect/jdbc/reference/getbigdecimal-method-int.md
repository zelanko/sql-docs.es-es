---
title: "Método getBigDecimal (int) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getBigDecimal Method (int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f74030d8-3789-463b-b414-2eb01cef8a30
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2520d63ee6623cfca6c78d2b30582763198f6daa
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getbigdecimal-method-int"></a>Método getBigDecimal (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como java.math.BigDecimal con precisión completa según el índice de parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto BigDecimal.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBigDecimal especificado por el método getBigDecimal en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método getBigDecimal &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
