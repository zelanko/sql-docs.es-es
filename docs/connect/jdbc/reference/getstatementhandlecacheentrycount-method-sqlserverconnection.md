---
title: getStatementHandleCacheEntryCount (método) (SQLServerConnection) | Documentos de Microsoft
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
ms.topic: conceptual
apiname:
- SQLServerConnection.getStatementHandleCacheEntryCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f29ad007c4f3b60694963c9f3f7b71763c7b9fa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getstatementhandlecacheentrycount-method-sqlserverconnection"></a>getStatementHandleCacheEntryCount (método) (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Devuelve el número actual de identificadores de instrucciones preparadas agrupados.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getStatementHandleCacheEntryCount()  
```  

## <a name="return-value"></a>Valor devuelto
 Un **int** que contiene el número actual de identificadores de instrucciones preparadas agrupados.

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
