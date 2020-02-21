---
title: Método setTimestamp (int, java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTimestamp (int, java.sql.Timestamp, java.util.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10c93cbf-f831-4e00-8e37-ea728bf34b1e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa968eaf8b34a1959f17474ae79f65f1a2fd0ebc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972440"
---
# <a name="settimestamp-method-int-javasqltimestamp-javautilcalendar"></a>Método setTimestamp (int, java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para los valores timestamp y calendar especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setTimestamp(int n,  
                               java.sql.Timestamp x,  
                               java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *n*  
  
 Valor **int** que indica el número de parámetro.  
  
 *x*  
  
 Un objeto Timestamp.  
  
 *cal*  
  
 Un objeto Calendar.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setTimestamp especifica este método setTimestamp en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [setTimestamp (método) &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
