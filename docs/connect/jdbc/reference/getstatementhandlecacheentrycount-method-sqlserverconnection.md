---
title: getStatementHandleCacheEntryCount (método) (SQLServerConnection) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: ff9bdcca7a1d5c868c497d4be61a68a51ae37090
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32837518"
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
  
  
