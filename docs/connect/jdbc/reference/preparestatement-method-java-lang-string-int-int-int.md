---
title: Método prepareStatement (java.lang.String, int, int, int) | Documentos de Microsoft
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
- SQLServerConnection.prepareStatement (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b78d2192-f315-4c45-9051-c77059e2c3f4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b5bb32a78809ae6abac9af2decfff9002c9c3f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="preparestatement-method-javalangstring-int-int-int"></a>Método prepareStatement (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) objeto que genera [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos con el tipo especificado, la simultaneidad y la capacidad de alojamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int nType,  
                                                   int nConcur,  
                                                   int nHold)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sql*  
  
 A **cadena** que contiene una instrucción SQL.  
  
 *nLas*  
  
 Un **int** que indica el tipo de conjunto de lo resultados.  
  
 *nConcur*  
  
 Un **int** que indica el tipo de simultaneidad del conjunto de lo resultados.  
  
 *nHold*  
  
 Un **int** que indica el conjunto de resultados capacidad de alojamiento.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de instrucción PreparedStatement.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método prepareStatement especificado por el método prepareStatement en la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Vea también  
 [Método prepareStatement &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
