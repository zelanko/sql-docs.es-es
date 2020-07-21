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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73a507e48b4ecc7f1ead7e33fe6936f5ed73f424
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924836"
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
  
## <a name="remarks"></a>Observaciones  
 El método getFetchDirection especifica este método getFetchDirection en la interfaz java.sql.ResultSet.  
  
 Este método devuelve FETCH_FORWARD para los cursores de avance y el último valor obtenido a través de una llamada al método [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) para otros tipos de cursor; por otra parte devolverá FETCH_UNKNOWN para estos tipos de cursor si nunca se ha llamado al método setFetchDirection.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
