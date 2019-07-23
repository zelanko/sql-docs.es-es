---
title: Método getConcurrency (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d0d59186e15dc07d1d4e91ac673c456ec592d01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952823"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>Método getConcurrency (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el modo de simultaneidad de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el tipo de simultaneidad, que puede ser uno de los siguientes valores:  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getConcurrency se especifica mediante el método getConcurrency de la interfaz java. SQL. ResultSet.  
  
 El objeto [SQLServerStatementque](../../../connect/jdbc/reference/sqlserverstatement-class.md) creó el conjunto de resultados determina simultaneidad que se utiliza.  
  
 Este método se puede utilizar para determinar la simultaneidad actual. Si la aplicación seleccionó CONCUR_READ_ONLY o CONCUR_UPDATABLE, estos se devolverán. Si la aplicación utilizó la simultaneidad predeterminada, se devolverá CONCUR_READ_ONLY.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
