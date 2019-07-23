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
ms.openlocfilehash: ac1cf4dbd8c8c14b5c97dbfecbe81d397c1598ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983446"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Método getEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Devuelve el valor de la propiedad de conexión **enablePrepareOnFirstPreparedStatementCall** . Si es false, la primera ejecución llamará a sp_executesql y no se preparará una instrucción, una vez que se produzca la segunda ejecución, llamará a sp_prepexec y, en realidad, configurará un identificador de instrucción preparado. Las siguientes ejecuciones llamarán a sp_execute. Esto libera la necesidad de sp_unprepare en el cierre de la instrucción preparada si la instrucción solo se ejecuta una vez. El valor predeterminado de esta opción se puede cambiar mediante una llamada a setDefaultEnablePrepareOnFirstPreparedStatementCall ().

## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Valor devuelto
 Valor **booleano** que contiene el valor de la propiedad de conexión **enablePrepareOnFirstPreparedStatementCall** .

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible en la versión 6,4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
