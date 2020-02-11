---
title: 'Opciones (ejecución de la consulta: SQL Server: Página avanzadas) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAdvanced
ms.assetid: 3ec788c7-22c3-4216-9ad0-81a168d17074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5323054b77ed26a3ada816f44c1bf6764ded931d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089372"
---
# <a name="options-query-executionsql-serveradvanced-page"></a>Opciones (Ejecución de la consulta/SQL Server/página Avanzadas)
  Hay varias opciones disponibles cuando se utiliza el comando SET. Utilice esta página para especificar una opción **set** para ejecutar consultas de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el Editor de consultas de SQL Server. No tendrán efecto en otros editores de código. Los cambios que se realicen en estas opciones solo se aplicarán a las nuevas consultas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para cambiar las opciones de las consultas actuales, haga clic en **Opciones de consulta** en el menú **Consulta** o en el menú contextual de la ventana Consulta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . En **Ejecución**, haga clic en **Avanzadas**. Para obtener más información sobre cada una estas opciones, consulte los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **ESTABLECER NOCOUNT**  
 No devuelve el recuento del número de filas, como un mensaje con el conjunto de resultados. Esta casilla está desactivada de forma predeterminada.  
  
 **ESTABLECER NOEXEC**  
 No ejecuta la consulta. Esta casilla está desactivada de forma predeterminada.  
  
 **ESTABLECER PARSEONLY**  
 Comprueba la sintaxis de cada consulta, pero no las ejecuta. Esta casilla está desactivada de forma predeterminada.  
  
 **ESTABLECER CONCAT_NULL_YIELDS_NULL**  
 Cuando esta casilla está activada, las consultas que concatenan un valor existente con un valor NULL devuelven siempre un valor NULL como resultado. Cuando esta casilla está desactivada, un valor existente concatenado con un valor NULL devolverá el valor existente. Esta casilla está activada de forma predeterminada.  
  
 **ESTABLECER ARITHABORT**  
 Cuando esta casilla está activada, el hecho de que una instrucción INSERT, DELETE o UPDATE encuentre un error aritmético (desbordamiento, división por cero o error de dominio) al evaluar una expresión, hará que la consulta o proceso por lotes finalicen. Cuando esta casilla está desactivada, se proporciona si es posible un valor NULL para dicho valor, la consulta continúa y se incluye un mensaje con el resultado. Para obtener más información, vea [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql). Esta casilla está activada de forma predeterminada.  
  
 **ESTABLECER SHOWPLAN_TEXT**  
 Cuando esta casilla está activada, el plan de consulta se devuelve en formato de texto con cada consulta. Esta casilla está desactivada de forma predeterminada.  
  
 **ESTABLECER HORA DE ESTADÍSTICAS**  
 Cuando se activa esta casilla, las estadísticas de tiempo se devuelven con cada consulta. Esta casilla está desactivada de forma predeterminada.  
  
 **ESTABLECER E/S DE ESTADÍSTICAS**  
 Cuando esta casilla está activada, las estadísticas de entrada y salida se devuelven con cada consulta. Esta casilla está desactivada de forma predeterminada.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 Se ha establecido de forma predeterminada el nivel de aislamiento de transacción READ COMMITTED. Para obtener más información, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). El nivel de aislamiento de transacción SNAPSHOT no está disponible. Para utilizar el aislamiento SNAPSHOT, agregue la instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] siguiente:  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **SET DEADLOCK PRIORITY**  
 El valor predeterminado Normal permite que cada consulta tenga la misma prioridad cuando se produce un interbloqueo. Seleccione una prioridad baja si desea que esta consulta pierda conflictos de interbloqueo y quede seleccionada como la consulta que debe finalizar.  
  
 **SET LOCK TIMEOUT**  
 El valor predeterminado de -1 indica que los bloqueos se mantienen hasta que finalizan las transacciones. El valor de 0 significa no esperar en absoluto y devolver un mensaje en cuanto se encuentre un bloqueo. Proporcione un valor mayor que 0 milisegundos para finalizar una transacción si los bloqueos para transacción deben mantenerse durante un intervalo mayor.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 Utilice la opción **QUERY_GOVERNOR_COST_LIMIT** para especificar un límite superior para el tiempo en el que se puede ejecutar una consulta. El costo de la consulta se refiere al tiempo transcurrido estimado, en segundos, necesario para finalizar una consulta en una configuración específica de hardware. El valor predeterminado 0 indica que no hay ningún límite de tiempo para la ejecución de una consulta.  
  
 **Suprimir encabezados de mensaje de proveedor**  
 Cuando esta casilla está activada, no se muestran los mensajes de estado del proveedor (como el proveedor SQLClient). Esta casilla está activada de forma predeterminada. Desactive esta casilla para ver los mensajes del proveedor cuando la solución de las consultas presente errores en el nivel del proveedor.  
  
 **Desconectar tras la ejecución de la consulta**  
 Cuando esta casilla está activada, la conexión a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] finaliza después de completarse la consulta. Esta casilla está desactivada de forma predeterminada.  
  
 **Restablecer valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  
