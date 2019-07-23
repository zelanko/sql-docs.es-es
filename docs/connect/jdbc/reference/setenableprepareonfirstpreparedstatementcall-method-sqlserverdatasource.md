---
title: Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26ac2cac075d08b8029ac0e85dacffd1674fb0da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974308"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Especifica el comportamiento de una instancia de conexión concreta. Si esta configuración es falsa, la primera ejecución de una instrucción preparada llamará a sp_executesql y no preparará una instrucción, una vez que se produzca la segunda ejecución, llamará a sp_prepexec y, en realidad, configurará un identificador de instrucción preparado. Las siguientes ejecuciones llamarán a sp_execute. Esto libera la necesidad de sp_unprepare en el cierre de la instrucción preparada si la instrucción solo se ejecuta una vez.  
## <a name="syntax"></a>Sintaxis  
  
```
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 Nuevo valor de la propiedad de conexión **enablePrepareOnFirstPreparedStatementCall** .  

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible en la versión 6,4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
