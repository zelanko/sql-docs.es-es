---
title: "Método setTimestamp a valores timestamp y calendar | Documentos de Microsoft"
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
- SQLServerCallableStatement.setTimestamp (java.lang.String, java.sql.Timestamp, java.util.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 09dca1f9-225a-4acb-9857-9a947e0829be
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d6e4c2ce26ae2a057f1b184311e31fbdb907e9ba
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="settimestamp-method-javalangstring-javasqltimestamp-javautilcalendar"></a>Método setTimestamp (java.lang.String, java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para los valores timestamp y calendar especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setTimestamp(java.lang.String sCol,  
                         java.sql.Timestamp x,  
                         java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *x*  
  
 Un objeto de la marca de tiempo.  
  
 *c*  
  
 Un objeto de calendario.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setTimestamp especificado por el método setTimestamp en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método setTimestamp &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
