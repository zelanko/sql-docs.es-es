---
title: Método (SQLServerStatement) getMaxFieldSize | Documentos de Microsoft
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
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d98c7ec1ba9b814f17e3c401eb9a55aa53f9ed46
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize (método) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de bytes que se pueden devolver para los caracteres y valores de columna binaria en un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica el número máximo de bytes que puede contener una columna, o bien 0 si no hay ningún límite.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getMaxFieldSize especificado por el método getMaxFieldSize en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
