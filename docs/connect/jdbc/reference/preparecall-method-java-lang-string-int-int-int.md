---
title: "Método prepareCall (java.lang.String, int, int, int) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 81104fd5-75b0-4540-9f48-c3dbf59a8564
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac3d0d3c239c76d187954e6a4568a140aba73ade
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="preparecall-method-javalangstring-int-int-int"></a>Método prepareCall (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) objeto que genera [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos con el tipo especificado, la simultaneidad y la capacidad de alojamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int nType,  
                                              int nConcur,  
                                              int nHold)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *SQL*  
  
 A **cadena** que contiene una instrucción SQL.  
  
 *nLas*  
  
 Un **int** que indica el tipo de conjunto de lo resultados.  
  
 *nConcur*  
  
 Un **int** que indica el tipo de simultaneidad del conjunto de lo resultados.  
  
 *nHold*  
  
 Un **int** que indica el conjunto de resultados capacidad de alojamiento.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto CallableStatement.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método prepareCall especificado por el método prepareCall de la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Vea también  
 [Método prepareCall &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
