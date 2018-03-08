---
title: "getDisableStatementPooling (método) (SQLServerConnection) | Documentos de Microsoft"
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
- SQLServerConnection.getDisableStatementPooling
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4b682c858c72c8560013a578513a7661bb1c570
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="getdisablestatementpooling-method-sqlserverconnection"></a>getDisableStatementPooling (método) (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Devuelve el valor de **disableStatementPooling** propiedad de conexión. Esta configuración controla si la agrupación de instrucción está habilitada o no para esta conexión.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getDisableStatementPooling()  
```  

## <a name="return-value"></a>Valor devuelto
 A **booleano** que contiene el valor de **disableStatementPooling** propiedad de conexión.

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
