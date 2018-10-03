---
title: Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e5a03b231b86be065ff19dd0f0a6818ba560bf5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47671744"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Devuelve el valor de **enablePrepareOnFirstPreparedStatementCall** propiedad de conexión. Si es false, la primera ejecución llamará a sp_executesql y no preparar una instrucción, una vez que produzca la segunda ejecución llamará a sp_prepexec y configurar un identificador de instrucción preparada. Después de las ejecuciones llamará a sp_execute. Cerrar Esto evita la necesidad de sp_unprepare en la instrucción preparada si la instrucción solo se ejecuta una vez. El valor predeterminado para esta opción se puede cambiar por setDefaultEnablePrepareOnFirstPreparedStatementCall() que realiza la llamada.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Valor devuelto
 Un **booleano** que contiene el valor de **enablePrepareOnFirstPreparedStatementCall** propiedad de conexión.

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
