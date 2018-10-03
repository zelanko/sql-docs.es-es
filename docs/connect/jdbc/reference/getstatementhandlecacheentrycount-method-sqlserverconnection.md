---
title: Método getStatementHandleCacheEntryCount (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getStatementHandleCacheEntryCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10cee9ea43079ff31556452ffd5d63b7c16a7fcc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730453"
---
# <a name="getstatementhandlecacheentrycount-method-sqlserverconnection"></a>Método getStatementHandleCacheEntryCount (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Devuelve el número actual de identificadores de instrucción preparada agrupados.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getStatementHandleCacheEntryCount()  
```  

## <a name="return-value"></a>Valor devuelto
 Un **int** que contiene el número actual de identificadores de instrucción preparada agrupados.

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
