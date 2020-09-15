---
description: Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource)
title: Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 838696d89354d857c86aae0f6191d1dd08fba820
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431917"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Especifica el comportamiento de una instancia de conexión específica. Si esta configuración es false, la primera ejecución de una instrucción preparada llamará a sp_executesql y no prepara una instrucción. Una vez que se produce la segunda ejecución, llamará a sp_prepexec y configura realmente un identificador de instrucción preparada. Las siguientes ejecuciones llamarán a sp_execute. Esto alivia la necesidad de sp_unprepare en la instrucción preparada CLOSE si la instrucción solo se ejecuta una vez.  
## <a name="syntax"></a>Sintaxis  
  
```
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 El nuevo valor de la propiedad de conexión **enablePrepareOnFirstPreparedStatementCall**.  

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Observaciones  
 Este método está disponible en la versión 6.4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
