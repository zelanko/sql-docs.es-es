---
title: "Método getTimestamp (int, java.util.Calendar) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getTimestamp (int, java.util.Calendar)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 161c559a-8651-44ba-a914-15eb6a612417
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce7ad759d6901ccdc641d693f836180a1152fe84
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="gettimestamp-method-int-javautilcalendar"></a>Método getTimestamp (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Timestamp en el lenguaje de programación según el índice del parámetro, utilizando un objeto de calendario de Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Timestamp getTimestamp(int index,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Un **int** que indica el índice del parámetro.  
  
 *CAL*  
  
 Un objeto de calendario.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de la marca de tiempo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getTimestamp es especificado por el método getTimestamp en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve valores solo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** y **smalldatetime** columnas.  
  
## <a name="see-also"></a>Vea también  
 [Método getTimestamp &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
