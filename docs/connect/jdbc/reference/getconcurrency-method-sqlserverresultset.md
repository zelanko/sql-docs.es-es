---
description: Método getConcurrency (SQLServerResultSet)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8cb92a019c9c65e867be023fab9bc299a7a8bc8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436557"
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
  
## <a name="remarks"></a>Observaciones  
 El método getConcurrency especifica este método getConcurrency en la interfaz java.sql.ResultSet.  
  
 El objeto [SQLServerStatementque](../../../connect/jdbc/reference/sqlserverstatement-class.md) creó el conjunto de resultados determina simultaneidad que se utiliza.  
  
 Este método se puede utilizar para determinar la simultaneidad actual. Si la aplicación seleccionó CONCUR_READ_ONLY o CONCUR_UPDATABLE, estos se devolverán. Si la aplicación utilizó la simultaneidad predeterminada, se devolverá CONCUR_READ_ONLY.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
