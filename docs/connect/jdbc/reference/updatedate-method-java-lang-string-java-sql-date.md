---
title: "Método updateDate (java.lang.String, java.sql.Date) | Documentos de Microsoft"
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
- SQLServerResultSet.updateDate (java.lang.String, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fbe9123-7365-4a8f-bbd5-dc2b16f1b231
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56d2e77c1f8dccc4cbe73aa258495ffa41efbf19
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updatedate-method-javalangstring-javasqldate"></a>Método updateDate (java.lang.String, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de fecha según el nombre de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateDate(java.lang.String columnName,  
                       java.sql.Date x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de columna.  
  
 *x*  
  
 Un valor de fecha.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateDate es especificado por el método updateDate en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Método updateDate &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
