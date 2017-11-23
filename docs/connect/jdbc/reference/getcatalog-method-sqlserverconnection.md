---
title: "Método (SQLServerConnection) getCatalog | Documentos de Microsoft"
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
apiname: SQLServerConnection.getCatalog
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba6dff246665d467ee77502f5bd27a2a9ed06dfa
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog (método) (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el nombre del catálogo actual de este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el nombre del catálogo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getCatalog especificado por el método getCatalog en la interfaz java.sql.Connection.  
  
 Devuelve la propiedad de catálogo actual del objeto SQLServerConnection, o null si no se establece. La propiedad de catálogo se establece explícitamente con la [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) método, o se actualiza implícitamente leyendo el cambio de entorno de TDS para el catálogo actual.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
