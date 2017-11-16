---
title: "Creación de procedimientos almacenados compilados de forma nativa | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c358b4c12f78b7d56444d0a4bd0e8e6910c174aa
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="creating-natively-compiled-stored-procedures"></a>Crear procedimientos almacenados compilados de forma nativa
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Los procedimientos almacenados compilados de forma nativa no implementan el área expuesta completa de programación y consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Hay ciertas construcciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que no se pueden usar en los procedimientos almacenados compilados de forma nativa. Para obtener más información, vea [Características admitidas en los módulos T-SQL compilados de forma nativa](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 Sin embargo, hay varias características de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se admiten solo para los procedimientos almacenados compilados de forma nativa:  
  
-   Bloques atomic. Para obtener más información, consulte [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
-   Restricciones **NOT NULL** en parámetros y variables. No se pueden asignar valores **NULL** a los parámetros o variables declarados como **NOT NULL**. Para obtener más información, vea [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **not null**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **not null = "Hello"**; -- *(debe inicializarse en un valor)*.  
  
    -   SET @myVarchar **= null**; -- *(compila, pero se produce un error durante el tiempo de ejecución)*.  
  
-   Enlace de esquema de los procedimientos almacenados compilados de forma nativa.  
  
 Los procedimientos almacenados compilados de forma nativa se crean por medio de [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md). En el ejemplo siguiente se muestra una tabla optimizada para memoria y un procedimiento almacenado compilado de nativa que se usa para insertar filas en la tabla.  
  
```tsql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 En el ejemplo de código, **NATIVE_COMPILATION** indica que este procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] es un procedimiento almacenado compilado de forma nativa. Se requieren las siguientes opciones:  
  
|Opción|Descripción|  
|------------|-----------------|  
|**SCHEMABINDING**|Un procedimiento almacenado compilado de forma nativa se debe enlazar al esquema de objetos al que hace referencia. Esto significa que no se puede anular las tablas a las que hace referencia el procedimiento. Las tablas a las que se hace referencia en el procedimiento deben incluir el nombre de esquema y no se admiten caracteres comodín (\*) en las consultas (es decir, sin `SELECT * from...`). **SCHEMABINDING** solo se admite para los procedimientos almacenados compilados de forma nativa en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**BEGIN ATOMIC**|El cuerpo de un procedimiento almacenado compilado de forma nativa debe constar exactamente de un solo bloque atomic. Los bloques atomic garantizan la ejecución atómica del procedimiento almacenado. Si se invoca el procedimiento fuera del contexto de una transacción activa, iniciará una nueva transacción, que se confirma al final del bloque atomic. Los bloques atomic de los procedimientos almacenados compilados de forma nativa tienen dos opciones obligatorias:<br /><br /> **TRANSACTION ISOLATION LEVEL**. Vea [Transaction Isolation Levels for Memory-Optimized Tables](http://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) (Niveles de aislamiento de transacción para tablas con optimización para memoria) para conocer los niveles de aislamiento admitidos.<br /><br /> **LANGUAGE**. El lenguaje del procedimiento almacenado se debe establecer en uno de los lenguajes o de alias de lenguaje disponibles.|  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
