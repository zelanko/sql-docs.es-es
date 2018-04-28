---
title: setFetchSize (método) (SQLServerResultSet) | Documentos de Microsoft
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
ms.topic: article
apiname:
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2344b1701a66621665a4ea1179e74b602141918d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="setfetchsize-method-sqlserverresultset"></a>setFetchSize (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ofrece el controlador JDBC una sugerencia sobre el número de filas que se debe capturar desde la base de datos cuando se necesitan más filas para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Filas*  
  
 Un **int** que indica el número de filas que se va a capturar.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setFetchSize especificado por el método setFetchSize en la interfaz java.sql.ResultSet.  
  
 Si el tamaño de la captura es cero, el controlador JDBC omite el valor y calcula el tamaño de captura apropiado. El valor predeterminado se establece mediante el [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que creó el conjunto de resultados. El tamaño de la captura puede cambiar en cualquier momento.  
  
 Este método cambia el tamaño de la captura del bloque para los cursores de servidor y surte efecto la próxima vez que el controlador JDBC necesite llamar a sp_cursorfetch. Al establecer el tamaño de la captura en cero, se restaura el tamaño predeterminado de la misma para el tipo de cursor que se esté utilizando en esos momentos.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
