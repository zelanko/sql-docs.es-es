---
title: Instrucciones para la lógica de reintento de transacciones en tablas optimizadas para memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f719470419940b130967b7c1360c4ae0c281eb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779219"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>Instrucciones para la lógica de reintento de transacciones en tablas con optimización para memoria
  Hay varias condiciones de error que aparecen con las transacciones que tienen acceso a tablas optimizadas para memoria.  
  
-   41302. La transacción actual intentó actualizar un registro que se ha actualizado desde que la transacción se inició.  
  
-   41305. La transacción actual no pudo confirmarse debido a un error repetible de validación de lectura.  
  
-   41325. La transacción actual no pudo confirmarse debido a un error serializable de validación.  
  
-   41301. Una transacción anterior a la transacción actual realizada en una dependencia se ha anulado y la transacción actual ya no puede confirmarse.  
  
 Una causa común de estos errores son las interferencias entre transacciones que se ejecutan simultáneamente. La acción correctora común es reintentar la transacción.  
  
 Para obtener más información sobre estas condiciones de error, vea la sección sobre detección de conflictos, validación y comprobaciones de dependencias de confirmación en [transacciones en tablas optimizadas para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Los interbloqueos (código de error 1205) no pueden aparecer en las tablas optimizadas para memoria. Los bloqueos no se utilizan en las tablas optimizadas para memoria. Sin embargo, si la aplicación ya contiene lógica de reintento para los interbloqueos, la lógica existente se puede ampliar para incluir los nuevos códigos de error.  
  
## <a name="considerations-for-retrying"></a>Consideraciones sobre el reintento  
 Las aplicaciones suelen encontrar conflictos entre las transacciones y tienen que implementar lógica de reintento para resolverlos. El número de conflictos encontrado depende de varios factores:  
  
-   Contención de filas individuales. La posibilidad de conflictos aumenta a medida que aumenta el número de transacciones que intentan actualizar la misma fila.  
  
-   Número de filas leídas por transacciones REPEATABLE READ. Cuantas más filas se lean, mayor es la probabilidad de que algunas de estas filas sean actualizadas por transacciones simultáneas. Esto causa errores de validación de lectura repetible.  
  
-   Tamaño de los intervalos de examen que utilizan las transacciones SERIALIZABLE. Cuanto mayores sean los intervalos de examen, mayor es la posibilidad de que las transacciones simultáneas presenten filas fantasma, ocasionando errores en la validación serializable.  
  
     Es difícil para una aplicación evitar estos conflictos, que requieren lógica de reintento.  
  
> [!IMPORTANT]  
>  Las transacciones de lectura/escritura que tienen acceso a tablas optimizadas para memoria requieren lógica de reintento.  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>Consideraciones para las transacciones de solo lectura y los procedimientos almacenados compilados de forma nativa  
 Las transacciones de solo lectura que abarcan la ejecución de un procedimiento almacenado compilado de forma nativa no requieren la validación de las transacciones REPEATABLE READ y SERIALIZABLE. No pueden producirse conflictos de escritura porque una transacción es de solo lectura.  
  
 Sin embargo, los errores de dependencia pueden seguir apareciendo. Los errores de dependencia son más extraños que los errores resultantes de conflictos. Por tanto, en muchos casos, no se requiere una lógica de reintento específica para las transacciones de solo lectura que abarcan ejecuciones únicas de procedimientos almacenados compilados de forma nativa.  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>Consideraciones para las transacciones de solo lectura y las transacciones entre contenedores  
 Las transacciones de solo lectura entre contenedores, que son las transacciones que se inician fuera del contexto de un procedimiento almacenado compilado de forma nativa, no realizan la validación si se tiene acceso a todas las tablas optimizadas para memoria bajo aislamiento SNAPSHOT. Sin embargo, cuando se tiene acceso a tablas optimizadas para memoria con el aislamiento REPEATABLE READ o SERIALIZABLE, la validación se realiza en tiempo de confirmación. En este caso, puede ser necesaria lógica de reintento.  
  
 Para obtener más información, vea la sección sobre transacciones entre contenedores en [los niveles de aislamiento de transacción](../../2014/database-engine/transaction-isolation-levels.md).  
  
## <a name="implementing-retry-logic"></a>Implementar lógica de reintento  
 Como ocurre con todas las transacciones que tienen acceso a tablas optimizadas para memoria, se debe considerar el uso de lógica de reintentos para controlar los posibles errores, como conflictos de escritura (código de error 41302) o errores de dependencia (código de error 41301). En la mayoría de las aplicaciones la tasa de error será baja, pero sigue siendo necesario controlar los errores reintentando la transacción. He aquí dos maneras sugeridas de implementar lógica de reintentos:  
  
-   Reintentos del lado cliente. Los intentos del lado cliente son la mejor manera de implementar lógica de reintentos en el caso general. La aplicación cliente detecta el error producido por la transacción y reintenta la transacción. Si una aplicación cliente existente tiene lógica de reintentos para controlar los interbloqueos, puede ampliar la aplicación para controlar los nuevos códigos de error.  
  
-   Mediante un procedimiento almacenado contenedor. El cliente llama a un procedimiento almacenado de [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado que llama al procedimiento almacenado compilado de forma nativa o ejecuta la transacción. Después, el procedimiento contenedor usa lógica try/catch para detectar el error y reintentar la llamada al procedimiento si es necesario. Es posible que se devuelvan resultados al cliente antes del error y que el cliente no sepa cómo descartarlos. Por tanto, para estar seguros, es mejor usar este método solo con procedimientos almacenados compilados de forma nativa que no devuelven ningún conjunto de resultados al cliente.  
  
 La lógica de reintento se puede implementar en [!INCLUDE[tsql](../includes/tsql-md.md)] o en el código de aplicación en el nivel medio.  
  
 Dos posibles razones para considerar la lógica de reintento son:  
  
-   La aplicación cliente tiene lógica de reintento para otros códigos de error, como 1205, que puede ampliar.  
  
-   Los conflictos son raros y es importante reducir la latencia de un extremo a otro mediante la ejecución preparada. Para obtener más información sobre la ejecución directa de procedimientos almacenados compilados de forma nativa, vea [procedimientos almacenados compilados](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)de forma nativa.  
  
 En el siguiente ejemplo se muestra la lógica de reintento de un procedimiento almacenado de [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado que contiene una llamada a un procedimiento almacenado compilado de forma nativa o a una transacción entre contenedores.  
  
```sql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries - tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   ...  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>Consulte también  
 [Descripción de las transacciones en tablas optimizadas para memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Transacciones en tablas con optimización para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Instrucciones para los niveles de aislamiento de transacciones con tablas con optimización para memoria](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
