---
title: Método createStatement (int, int, int) | Documentos de Microsoft
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
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cabeeaf2759991bda02b3dd1f59e247c7037f15
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32830640"
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
  
  
