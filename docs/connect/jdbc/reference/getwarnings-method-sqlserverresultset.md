---
title: "Método getWarnings (SQLServerResultSet) | Documentos de Microsoft"
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
apiname: SQLServerResultSet.getWarnings
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: eb4339b0-383b-4337-a935-e8ec3f0d4123
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3df9fc832fdcdb1e5e2eb6c9393f397b8308e002
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getwarnings-method-sqlserverresultset"></a>Método getWarnings (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la primera advertencia que notifican las llamadas en el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
> [!NOTE]  
>  Este método no es compatible actualmente con la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Si se llama este método, siempre devolverá un valor NULL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.SQLWarning getWarnings()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto objeto SQLWarning.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getWarnings es especificado por el método getWarnings en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
