---
title: Método createStatement (int, int, int) | Documentos de Microsoft
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
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a98b5be003546b2573a1ecb844d4c5a08c7f6913
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="createstatement-method-int-int-int"></a>Método createStatement (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que genera [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos con el tipo especificado, la simultaneidad y la capacidad de alojamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *resultSetType*  
  
 El **int** valor que representa el resultado de establece el tipo.  
  
 *nConcur*  
  
 El **int** valor que representa el resultado de establece el tipo de simultaneidad.  
  
 *nHold*  
  
 El **int** valor que representa la capacidad de alojamiento.  
  
## <a name="return-value"></a>Valor devuelto  
 El objeto de instrucción.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método createStatement especificado por el método createStatement de la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Vea también  
 [Método createStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
