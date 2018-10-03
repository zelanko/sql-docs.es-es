---
title: Método closeUnreferencedPreparedStatementHandles (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.closeUnreferencedPreparedStatementHandles
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed4a01f47c16077ccb05e474c045e8edf2dbdeaa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811663"
---
# <a name="closeunreferencedpreparedstatementhandles-method-sqlserverconnection"></a>Método closeUnreferencedPreparedStatementHandles (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Fuerza la anulación-preparar las solicitudes para las instrucciones preparadas descartadas pendientes que se ejecutará.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public void closeUnreferencedPreparedStatementHandles()  
```  


## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  

## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
