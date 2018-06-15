---
title: getEnablePrepareOnFirstPreparedStatementCall (método) (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a131964479c0e2f64afa1f316344d446d1df2214
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834546"
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
  
  
