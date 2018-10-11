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
manager: craigg
ms.openlocfilehash: 6daf6d4d9f4c0d9ec018a9a1ff135760d64b63e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795733"
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
 Este método getConcurrency especificado por el método getConcurrency en la interfaz java.sql.ResultSet.  
  
 El objeto [SQLServerStatementque](../../../connect/jdbc/reference/sqlserverstatement-class.md) creó el conjunto de resultados determina simultaneidad que se utiliza.  
  
 Este método se puede utilizar para determinar la simultaneidad actual. Si la aplicación seleccionó CONCUR_READ_ONLY o CONCUR_UPDATABLE, estos se devolverán. Si la aplicación utilizó la simultaneidad predeterminada, se devolverá CONCUR_READ_ONLY.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
