---
title: "Método (SQLServerConnection) getCatalog | Documentos de Microsoft"
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
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac9650ac08ac3cae7169a2f746d050ccbed7d6f6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
  
