---
title: Modificar módulos T-SQL compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 45a0609a605478f2d3c727a7318e5a245fb7fd20
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34327476"
---
# <a name="altering-natively-compiled-t-sql-modules"></a>Altering Natively Compiled T-SQL Modules
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], puede realizar operaciones `ALTER` en procedimientos almacenados compilados de forma nativa y otros módulos [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados de forma nativa, como UDF escalares y desencadenadores mediante la instrucción `ALTER`.  
  
Al ejecutar `ALTER` en un módulo [!INCLUDE[tsql](../../includes/tsql-md.md)] compilado de forma nativa, el módulo se vuelve a compilar con una nueva definición. Mientras la recompilación está en curso, la versión antigua del módulo sigue estando disponible para su ejecución. Una vez completada la compilación, se agotan las ejecuciones del módulo y se instala la nueva versión del módulo. Cuando se modifica un módulo [!INCLUDE[tsql](../../includes/tsql-md.md)] compilado de forma nativa, puede modificar las opciones siguientes.  
  
-   Parámetros  
-   EXECUTE AS  
-   NIVEL DE AISLAMIENTO DE TRANSACCIÓN  
-   LANGUAGE  
-   DATEFIRST  
-   DATEFORMAT  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
> No es posible convertir módulos [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados de forma nativa en módulos compilados de forma no nativa. No es posible convertir módulos T-SQL compilados de forma no nativa en módulos compilados de forma nativa.  
  
Para más información sobre la funcionalidad y la sintaxis de `ALTER PROCEDURE`, vea [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md).  
  
Si ejecuta [sp_recompile](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) en módulos [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados de forma nativa, hará que los módulos se vuelvan a compilar en la siguiente ejecución.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se crea una tabla optimizada para memoria (T1) y un procedimiento almacenado compilado de forma nativa (usp_1) que selecciona todas las columnas de T1. Después, se modifica usp_1 para quitar la cláusula `EXECUTE AS`, cambiar el valor de `LANGUAGE` y seleccionar una sola columna (C1) de T1.  
  
```sql  
CREATE TABLE [dbo].[T1] (  
  [c1] [int] NOT NULL,  
  [c2] [float] NOT NULL,  
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
   SELECT c1, c2 FROM dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
   SELECT c1 FROM dbo.T1  
END  
GO    
```   
  
## <a name="see-also"></a>Ver también  
 [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)    
