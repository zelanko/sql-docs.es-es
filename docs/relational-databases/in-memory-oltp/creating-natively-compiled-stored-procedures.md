---
title: Creación de procedimientos almacenados compilados de forma nativa | Microsoft Docs
description: Obtenga información sobre las características de Transact-SQL admitidas solo para los procedimientos almacenados compilados de forma nativa. Vea cómo crear procedimientos almacenados compilados de forma nativa en SQL Server.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fd6c808ecc53838feb9466283c83919231ce67ad
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537596"
---
# <a name="creating-natively-compiled-stored-procedures"></a>Crear procedimientos almacenados compilados de forma nativa
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Los procedimientos almacenados compilados de forma nativa no implementan el área expuesta completa de programación y consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Hay ciertas construcciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que no se pueden usar en los procedimientos almacenados compilados de forma nativa. Para obtener más información, vea [Características admitidas en los módulos T-SQL compilados de forma nativa](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
Las siguientes características [!INCLUDE[tsql](../../includes/tsql-md.md)] solo se admiten en procedimientos almacenados compilados de forma nativa:  
  
-   Bloques atomic. Para obtener más información, consulte [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
-   Restricciones `NOT NULL` en parámetros y variables. No se pueden asignar valores **NULL** a los parámetros o variables declarados como **NOT NULL**. Para obtener más información, vea [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
    -   `CREATE PROCEDURE dbo.myproc (@myVarchar VARCHAR(32) NOT NULL) AS (...)`  
  
    -   `DECLARE @myVarchar VARCHAR(32) NOT NULL = "Hello"; -- Must initialize to a value.`  
  
    -   `SET @myVarchar = NULL; -- Compiles, but fails during run time.`  
  
-   Enlace de esquema de los procedimientos almacenados compilados de forma nativa.  
  
Los procedimientos almacenados compilados de forma nativa se crean por medio de [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md). En el ejemplo siguiente se muestra una tabla optimizada para memoria y un procedimiento almacenado compilado de nativa que se usa para insertar filas en la tabla.  
  
```sql  
CREATE TABLE [dbo].[T2] (  
  [c1] [int] NOT NULL, 
  [c2] [datetime] NOT NULL,
  [c3] nvarchar(5) NOT NULL, 
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_2] (@c1 int, @c3 nvarchar(5)) 
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
  DECLARE @c2 datetime = GETDATE();  
  INSERT INTO [dbo].[T2] (c1, c2, c3) values (@c1, @c2, @c3);  
END  
GO  
```  
 
En el ejemplo de código, **NATIVE_COMPILATION** indica que este procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] es un procedimiento almacenado compilado de forma nativa. Se requieren las siguientes opciones:  
  
|Opción|Descripción|  
|------------|-----------------|  
|**SCHEMABINDING**|Un procedimiento almacenado compilado de forma nativa se debe enlazar al esquema de objetos al que hace referencia. Esto significa que no se puede anular las tablas a las que hace referencia el procedimiento. Las tablas a las que se hace referencia en el procedimiento deben incluir el nombre de esquema y no se admiten caracteres comodín (\*) en las consultas (es decir, sin `SELECT * from...`). **SCHEMABINDING** solo se admite para los procedimientos almacenados compilados de forma nativa en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**BEGIN ATOMIC**|El cuerpo de un procedimiento almacenado compilado de forma nativa debe constar exactamente de un solo bloque atomic. Los bloques atomic garantizan la ejecución atómica del procedimiento almacenado. Si se invoca el procedimiento fuera del contexto de una transacción activa, iniciará una nueva transacción, que se confirma al final del bloque atomic. Los bloques atomic de los procedimientos almacenados compilados de forma nativa tienen dos opciones obligatorias:<br /><br /> **TRANSACTION ISOLATION LEVEL**. Vea [Transaction Isolation Levels for Memory-Optimized Tables](https://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) (Niveles de aislamiento de transacción para tablas con optimización para memoria) para conocer los niveles de aislamiento admitidos.<br /><br /> **LANGUAGE**. El lenguaje del procedimiento almacenado se debe establecer en uno de los lenguajes o de alias de lenguaje disponibles.|  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
