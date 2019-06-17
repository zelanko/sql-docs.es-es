---
title: Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c8458961cbd73f712b158d82c31c84372c00cde6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801598"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Especifica el comportamiento de una instancia de la conexión específica. Si el valor es false, la primera ejecución llamará a sp_executesql y no prepara una instrucción, una vez que la segunda ejecución ocurre lo llamará a sp_prepexec y configurar un identificador de instrucción preparada. Después de las ejecuciones llamará a sp_execute. Cerrar Esto evita la necesidad de sp_unprepare en la instrucción preparada si la instrucción solo se ejecuta una vez.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 El nuevo valor de la **enablePrepareOnFirstPreparedStatementCall** propiedad de conexión.  
 
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
