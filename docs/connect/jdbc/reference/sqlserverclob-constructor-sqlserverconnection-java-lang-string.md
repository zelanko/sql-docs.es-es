---
title: Método Sqlserverclob (SQLServerConnection, java.lang.String) | Documentos de Microsoft
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
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b6c7982dd0bf12ee7314e6903e455f2bec3e090
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>Método SQLServerClob (SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) clase cuando se especifica un [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto y una cadena de datos.  
  
> [!NOTE]  
>  Este método se ha dejado de utilizar en la versión 2.0 del controlador JDBC. En su lugar, use la [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) método de la [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) clase.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *conexión*  
  
 Un objeto SQLServerConnection.  
  
 *data*  
  
 Los datos CLOB.  
  
## <a name="see-also"></a>Vea también  
 [Constructores SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [Miembros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
