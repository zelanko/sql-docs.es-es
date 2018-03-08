---
title: "setEnablePrepareOnFirstPreparedStatementCall (método) (SQLServerConnection) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea672e1cd3b5998ca6829fb0f4c9fae29773d9d2
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>setEnablePrepareOnFirstPreparedStatementCall (método) (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Especifica el comportamiento de una instancia de conexión específica. Si el valor es false, la primera ejecución llamará sp_executesql y no prepara una instrucción, una vez que la segunda ejecución produce se llame a sp_prepexec y configurar realmente un identificador de instrucción preparada. Después de las ejecuciones llamará a sp_execute. Esto evita la necesidad de sp_unprepare en la instrucción preparada cierre si la instrucción solo se ejecuta una vez.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 El nuevo valor de la **enablePrepareOnFirstPreparedStatementCall** propiedad de conexión.  
 
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
