---
title: setDisableStatementPooling (método) (SQLServerConnection) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
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
- SQLServerConnection.setDisableStatementPooling
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb24fbcd9557b1ba7f0b0e93d21f6429a795eb48
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="setdisablestatementpooling-method-sqlserverconnection"></a>setDisableStatementPooling (método) (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Establece la agrupación de instrucciones en true o false. Si es false, permite la declaración de agrupación para usarse de acoplamiento con statementPoolingCacheSize valor > 0.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setDisableStatementPooling(boolean disableStatementPooling)  
```  

#### <a name="parameters"></a>Parámetros  
 *disableStatementPooling*  
  
 El nuevo valor de la **disableStatementPooling** propiedad de conexión.  
 
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
