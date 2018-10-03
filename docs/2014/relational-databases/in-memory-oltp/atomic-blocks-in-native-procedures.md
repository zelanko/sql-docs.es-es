---
title: Bloques Atomic | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 40e0e749-260c-4cfc-a848-444d30c09d85
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4bad6da6de694d9b835a6d3fe23fbc68d8642f50
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124105"
---
# <a name="atomic-blocks"></a>Bloques atomic
  `BEGIN ATOMIC` es parte del estándar ANSI SQL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite los bloques atomic solo en el nivel superior de los procedimientos almacenados compilados de forma nativa.  
  
-   Cada procedimiento almacenado compilado de forma nativa contiene exactamente un bloque de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este es un bloque ATOMIC.  
  
-   Los procedimientos almacenados [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretados no nativos y los lotes ad hoc no admiten los bloques atomic.  
  
 Los bloques atomic se ejecutan (atómicamente) dentro de la transacción. Todas las instrucciones del bloque se ejecutan correctamente o el bloque completo se revertirá al punto de retorno que se creó al principio del bloque. Además, los parámetros de configuración de la sesión son fijos para el bloque atomic. La ejecución del mismo bloque atomic en sesiones con diferentes parámetros producirá el mismo comportamiento, independientemente de la configuración de la sesión actual.  
  
## <a name="transactions-and-error-handling"></a>Transacciones y control de errores  
 Si una transacción ya existe en una sesión (porque un lote ejecutó una instrucción `BEGIN TRANSACTION` y la transacción permanece activa), iniciar a continuación un bloque atomic creará un punto de retorno de la transacción. Si el bloque sale sin una excepción, se confirma el punto de retorno que se creó para el bloque, pero la transacción no se confirmará hasta que se confirme en el nivel de sesión. Si el bloque produce una excepción, los efectos del bloque se revierten pero la transacción en el nivel de sesión continuará, a menos que la excepción invalide la transacción. Por ejemplo, un conflicto de escritura invalida la transacción, mientras que un error de conversión no la invalida.  
  
 Si no hay ninguna transacción activa en una sesión, `BEGIN ATOMIC` iniciará una nueva transacción. Si no se inicia una excepción fuera del ámbito del bloque, la transacción se confirmará al final del bloque. Si el bloque produce una excepción (es decir, la excepción no se detecta ni se controla en el bloque), la transacción se revertirá. Para las transacciones que ocupan un único bloque atomic (un único procedimiento almacenado compilado nativamente), no tiene que escribir explícita `BEGIN TRANSACTION` y `COMMIT` o `ROLLBACK` instrucciones.  
  
 Compatibilidad con los procedimientos almacenados de forma nativa la `TRY`, `CATCH`, y `THROW` construcciones de control de errores. `RAISERROR` no se admite.  
  
 En el ejemplo siguiente se muestra el comportamiento de control de errores con bloques atomic y procedimientos almacenados compilados de forma nativa:  
  
```tsql  
-- sample table  
CREATE TABLE dbo.t1 (  
  c1 int not null primary key nonclustered  
)  
WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- sample proc that inserts 2 rows  
CREATE PROCEDURE dbo.usp_t1 @v1 bigint not null, @v2 bigint not null  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC  
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english', DELAYED_DURABILITY = ON)  
  
  INSERT dbo.t1 VALUES (@v1)  
  INSERT dbo.t1 VALUES (@v2)  
  
END  
GO  
  
-- insert two rows  
EXEC dbo.usp_t1 1, 2  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify the rows 1 and 2 were committed  
SELECT c1 FROM dbo.t1  
GO  
  
-- execute proc with arithmetic overflow  
EXEC dbo.usp_t1 3, 4444444444444  
GO  
-- expected error message:  
-- Msg 8115, Level 16, State 0, Procedure usp_t1  
-- Arithmetic overflow error converting bigint to data type int.  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 was not committed; usp_t1 has been rolled back  
SELECT c1 FROM dbo.t1  
GO  
  
-- start a new transaction  
BEGIN TRANSACTION  
  -- insert rows 3 and 4  
  EXEC dbo.usp_t1 3, 4  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify the rows 3 and 4 were inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
  -- catch the arithmetic overflow error  
  BEGIN TRY  
    EXEC dbo.usp_t1 5, 4444444444444  
  END TRY  
  BEGIN CATCH  
    PRINT N'Error occurred: ' + error_message()  
  END CATCH  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify rows 3 and 4 are still in the table, and row 5 has not been inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
COMMIT  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 and 4 has been committed  
SELECT c1 FROM dbo.t1  
ORDER BY c1  
GO  
```  
  
 Los mensajes de error siguientes específicos de las tablas optimizadas para memoria invalidan las transacciones. Si aparecen en el ámbito de un bloque atomic, causarán que se anulen las transacciones: 10772, 41301, 41302, 41305, 41325, 41332 y 41333.  
  
## <a name="session-settings"></a>Configuración de la sesión  
 Los parámetros de configuración de sesión de los bloques atomic son fijos cuando se compila el procedimiento almacenado. Se pueden especificar algunas opciones de configuración con `BEGIN ATOMIC` mientras que otros están fijos siempre en el mismo valor.  
  
 Se requieren las siguientes opciones con `BEGIN ATOMIC`:  
  
|Configuración necesaria|Descripción|  
|----------------------|-----------------|  
|`TRANSACTION ISOLATION LEVEL`|Los valores admitidos son `SNAPSHOT`, `REPEATABLEREAD`, y `SERIALIZABLE`.|  
|`LANGUAGE`|Determina los formatos de fecha y hora y los mensajes del sistema. Se admiten todos los lenguajes y alias de [sys.syslanguages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql).|  
  
 Los siguientes parámetros de configuración son opcionales:  
  
|Configuración opcional|Descripción|  
|----------------------|-----------------|  
|`DATEFORMAT`|Se admiten todos los formatos de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se especifica, `DATEFORMAT` reemplaza el formato de fecha predeterminado asociado con `LANGUAGE`.|  
|`DATEFIRST`|Cuando se especifica, `DATEFIRST` reemplaza el valor predeterminado asociado a `LANGUAGE`.|  
|`DELAYED_DURABILITY`|Los valores admitidos son `OFF` y `ON`.<br /><br /> Las confirmaciones de transacción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden ser totalmente durables (el valor predeterminado) o durables diferidas. Para más información, vea [Controlar la durabilidad de las transacciones](../logs/control-transaction-durability.md).|  
  
 Las opciones SET siguientes tienen el mismo valor predeterminado del sistema para todos los bloques atomic en todos los procedimientos almacenados compilados de forma nativa:  
  
|Opción SET|Valor predeterminado del sistema para los bloques atomic|  
|----------------|--------------------------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNING|ON|  
|ARITHABORT|ON|  
|ARITHIGNORE|OFF|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|IDENTITY_INSERT|OFF|  
|NOCOUNT|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
|ROWCOUNT|0|  
|TEXTSIZE|0|  
|XACT_ABORT|OFF<br /><br /> Las excepciones no detectadas hacen que se revierta el bloque atomic, pero no causan que la transacción se anule a menos que el error invalide la transacción.|  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  
