---
title: getFetchDirection (método) (SQLServerResultSet) | Documentos de Microsoft
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
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 594d59adc33decf67118fd680d6aeaa32a38ebe7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834620"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la dirección de la captura para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica la dirección de la captura actual.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getFetchDirection especificado por el método getFetchDirection en la interfaz java.sql.ResultSet.  
  
 Este método devuelve FETCH_FORWARD para los cursores de solo avance, el último valor realizado por una llamada a la [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) método para otros tipos de cursor, devolverá fetch_unknown para estos tipos de cursor si el método setFetchDirection nunca se ha llamado.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
