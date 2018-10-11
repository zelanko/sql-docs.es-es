---
title: Método getFetchDirection (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd40f1a3bc218093f8a34215d15291bd152310be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726123"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>Método getFetchDirection (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la dirección de la captura para este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica la dirección de la captura actual.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getFetchDirection especificado por el método getFetchDirection en la interfaz java.sql.ResultSet.  
  
 Este método devuelve FETCH_FORWARD para los cursores de avance y el último valor obtenido a través de una llamada al método [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) para otros tipos de cursor; por otra parte devolverá FETCH_UNKNOWN para estos tipos de cursor si nunca se ha llamado al método setFetchDirection.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
