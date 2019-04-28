---
title: Opciones de consulta de ejecución (página avanzada) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7c598ca2dc2e1fd79e221c0c3d3fc1a5c3592dcb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844176"
---
# <a name="query-options-execution-advanced-page"></a>Opciones de ejecución de consulta (página Avanzadas)
  Al utilizar la instrucción **SET** están disponibles una variedad de opciones. Utilice esta página para especificar una opción **set** para la ejecución de consultas de Microsoft SQL Server. Para obtener información detallada de cada una de estas opciones, vea los Libros en pantalla de SQL Server.  
  
 **SET NOCOUNT**  
 No devuelve el recuento del número de filas, como un mensaje con el conjunto de resultados. Esta opción está desactivada de forma predeterminada.  
  
 **SET NOEXEC**  
 No ejecuta la consulta. Esta opción está desactivada de forma predeterminada.  
  
 **SET PARSEONLY**  
 Comprueba la sintaxis de cada consulta, pero no las ejecuta. Esta opción está desactivada de forma predeterminada.  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 Cuando se activa esta casilla, las consultas que concatenan un valor existente con un `NULL`, devuelven siempre un valor `NULL` como resultado. Cuando se desactiva esta casilla, un valor existente concatenado con un valor `NULL`, devuelve el valor existente. Esta opción está activada de forma predeterminada.  
  
 **SET ARITHABORT**  
 Cuando se activa esta casilla, cuando una instrucción `INSERT`, `DELETE` o `UPDATE` encuentra un error aritmético (desbordamiento, división por cero o error de dominio) durante la evaluación de la expresión, se finaliza la consulta o lote. Cuando se desactiva esta casilla, se proporciona un valor `NULL` para ese valor si es posible, la consulta continúa y se incluye un mensaje con el resultado. Vea los Libros en pantalla para una descripción más detallada de este comportamiento. Esta opción está activada de forma predeterminada.  
  
 **SET SHOWPLAN_TEXT**  
 Cuando se activa esta casilla, el plan de consulta se devuelve en formato de texto con cada consulta. Esta opción está desactivada de forma predeterminada.  
  
 **SET STATISTICS TIME**  
 Cuando se activa esta casilla, las estadísticas de tiempo se devuelven con cada consulta. Esta opción está desactivada de forma predeterminada.  
  
 **SET STATISTICS IO**  
 Cuando se activa esta casilla, las estadísticas de tiempo se devuelven con cada consulta. Esta opción está desactivada de forma predeterminada.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 Se ha establecido de forma predeterminada el nivel de aislamiento de transacción READ COMMITTED. Para obtener más información, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). El nivel de aislamiento de transacción SNAPSHOT no está disponible. Para utilizar el aislamiento SNAPSHOT, agregue la instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] siguiente:  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **ESTABLECER LA PRIORIDAD DE INTERBLOQUEO**  
 El valor predeterminado de **Normal** permite que cada consulta tenga la misma prioridad cuando tiene lugar un interbloqueo. Seleccione la prioridad Baja en la lista desplegable si desea que esta consulta pierda los conflictos de interbloqueo y se seleccione cuando la consulta haya finalizado.  
  
 **ESTABLECER TIEMPO DE ESPERA DE BLOQUEO**  
 El valor predeterminado de -1 indica que los bloqueos se mantienen hasta que finalizan las transacciones. El valor de 0 significa no esperar en absoluto y devolver un mensaje en cuanto se encuentre un bloqueo. Proporcione un valor mayor que 0 milisegundos para finalizar una transacción si los bloqueos para transacción deben mantenerse durante un intervalo mayor.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 Utilice la opción **query governor cost limit** para especificar un límite superior al periodo de tiempo en que una consulta puede ejecutarse. El costo de la consulta se refiere al tiempo transcurrido estimado, en segundos, necesario para finalizar una consulta en una configuración específica de hardware. La configuración predeterminada de 0 indica que no hay límite para el periodo de tiempo en que se ejecutará una consulta.  
  
 **Suprimir encabezados de mensaje de proveedor**  
 Cuando se activa esta casilla, no se muestran los mensajes de estado del proveedor (como el proveedor OLE DB). Esta casilla está activada de forma predeterminada. Desactive esta casilla para ver los mensajes del proveedor cuando la solución de las consultas presente errores en el nivel del proveedor.  
  
 **Desconectar tras la ejecución de la consulta**  
 Cuando se activa esta casilla, la conexión a SQL Server finaliza una vez que termina la consulta. Esta opción está desactivada de forma predeterminada.  
  
 **Valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  
