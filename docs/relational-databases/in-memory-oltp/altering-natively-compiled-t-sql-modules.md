---
title: "Modificar módulos T-SQL compilados de forma nativa | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4696039c56ebf5f1fd6ea440cd27da84721f35b9
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="altering-natively-compiled-t-sql-modules"></a>Altering Natively Compiled T-SQL Modules
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (y versiones posteriores) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)] puede realizar operaciones ALTER en procedimientos almacenados compilados de forma nativa y otros módulos T-SQL compilados de forma nativa como UDF escalares y desencadenadores mediante la instrucción ALTER.  
  
 Al ejecutar ALTER en un módulo T-SQL compilado de forma nativa, el módulo se vuelve a compilar con una nueva definición. Mientras la recompilación está en curso, la versión antigua del módulo sigue estando disponible para su ejecución. Una vez completada la compilación, se agotan las ejecuciones del módulo y se instala la nueva versión del módulo. Cuando se modifica un módulo T-SQL compilado de forma nativa, puede modificar las opciones siguientes.  
  
-   Parámetros  
  
-   EXECUTE AS  
  
-   NIVEL DE AISLAMIENTO DE TRANSACCIÓN  
  
-   LANGUAGE  
  
-   DATEFIRST  
  
-   DATEFORMAT  
  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
>  No es posible convertir módulos T-SQL compilados de forma nativa en módulos compilados de forma no nativa. No es posible convertir módulos T-SQL compilados de forma no nativa en módulos compilados de forma nativa.  
  
 Para obtener más información sobre la funcionalidad y la sintaxis de ALTER PROCEDURE, vea [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md).  
  
 Si ejecuta sp_recompile en un módulo T-SQL compilado de forma nativa, hará que se vuelva a compilar en la siguiente ejecución.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se crea una tabla con optimización para memoria (T1) y un procedimiento almacenado compilado de forma nativa (SP1) que selecciona todas las columnas de T1. Después, se modifica SP1 para quitar la cláusula EXECUTE AS, cambiar el valor de LANGUAGE y seleccionar una sola columna (C1) de T1.  
  
```  
CREATE TABLE [dbo].[T1]  
(  
[c1] [int] NOT NULL,  
[c2] [float] NOT NULL,  
CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
 SELECT c1, c2 from dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
 SELECT c1 from dbo.T1  
END  
GO  
  
```  
  
  
