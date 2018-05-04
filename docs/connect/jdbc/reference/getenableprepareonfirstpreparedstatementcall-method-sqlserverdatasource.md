---
title: getEnablePrepareOnFirstPreparedStatementCall (método) (SQLServerDataSource) | Documentos de Microsoft
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
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 970d17947e4472feaea0bb95e6596d49455db1cf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>getEnablePrepareOnFirstPreparedStatementCall (método) (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de **enablePrepareOnFirstPreparedStatementCall** propiedad de conexión. Si esta configuración devuelve false la primera ejecución de una instrucción preparada llamaremos sp_executesql y no prepara una instrucción, una vez que la segunda ejecución sucede lo llamaremos sp_prepexec y un identificador de instrucción preparada realmente de la instalación. Después de las ejecuciones llamará a sp_execute. Esto evita la necesidad de sp_unprepare en la instrucción preparada cierre si la instrucción solo se ejecuta una vez. 
  
## <a name="syntax"></a>Sintaxis  
  
```
public boolean getEnablePrepareOnFirstPreparedStatementCall();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve el **booleano** valor de la **enablePrepareOnFirstPreparedStatementCall** propiedad de conexión.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
