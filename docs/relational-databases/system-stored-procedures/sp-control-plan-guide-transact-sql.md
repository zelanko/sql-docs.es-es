---
title: sp_control_plan_guide (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_control_plan_guide
- sp_control_plan_guide_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_control_plan_guide
ms.assetid: c96d43d5-6507-4d66-b3f5-f44c0617cb5c
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f093a05ebbfe14a0d9436b0b2a9503aadc5b6440
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spcontrolplanguide-transact-sql"></a>sp_control_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita, habilita o deshabilita una guía de plan.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_control_plan_guide [ @operation = ] N'<control_option>'  
  [ , [ @name = ] N'plan_guide_name' ]  
  
<control_option>::=  
{   
    DROP   
  | DROP ALL  
  | DISABLE  
  | DISABLE ALL  
  | ENABLE   
  | ENABLE ALL  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 **N'** *plan_guide_name* **'**  
 Especifica la guía de plan que se va a quitar, habilitar o deshabilitar. *plan_guide_name* se resuelve en la base de datos actual. Si no se especifica, *plan_guide_name* el valor predeterminado es NULL.  
  
 DROP  
 Quita la Guía de plan especificada por *plan_guide_name*. Una vez quitada una guía de plan, las ejecuciones futuras de una consulta que coincidía anteriormente con la guía de plan no se ven afectadas por dicha guía de plan.  
  
 DROP ALL  
 Quita todas las guías de plan de la base de datos actual. **N'***plan_guide_name* no se puede especificar cuando se especifica DROP ALL.  
  
 DISABLE  
 Deshabilita la Guía de plan especificada por *plan_guide_name*. Una vez deshabilitada una guía de plan, las ejecuciones futuras de una consulta que coincidía anteriormente con la guía de plan no se ven afectadas por dicha guía de plan.  
  
 DISABLE ALL  
 Deshabilita todas las guías de plan de la base de datos actual. **N'***plan_guide_name* no se puede especificar cuando se especifica DISABLE ALL.  
  
 ENABLE  
 Permite que la Guía de plan especificada por *plan_guide_name*. Una guía de plan puede coincidir con una consulta apta después de ser habilitada. De manera predeterminada, las guías de plan se habilitan en el momento en que se crean.  
  
 ENABLE ALL  
 Habilita todas las guías de plan de la base de datos actual. **N'***plan_guide_name***'**no se puede especificar cuando se especifica ENABLE ALL.  
  
## <a name="remarks"></a>Comentarios  
 Se producirá un error si se intenta quitar o modificar una función, procedimiento almacenado o desencadenador DML al que una guía de plan, habilitada o deshabilitada, haga referencia.  
  
 Al deshabilitar una guía de plan deshabilitada o habilitar una guía de plan habilitada, no se produce ningún cambio o error.  
  
 Guías de planes no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md). Sin embargo, puede ejecutar **sp_control_plan_guide** con la opción DROP o DROP ALL en cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar **sp_control_plan_guide** en una guía de plan de tipo OBJECT (crear especificación de  **@type ='**objeto**'** ) requiere el permiso ALTER en el objeto que se hace referencia a la Guía de plan. Todas las demás guías de plan requieren el permiso ALTER DATABASE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enabling-disabling-and-dropping-a-plan-guide"></a>A. Habilitar, deshabilitar y quitar una guía de plan  
 El ejemplo siguiente crea una guía de plan, la deshabilita, la habilita y la quita.  
  
```  
--Create a procedure on which to define the plan guide.  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country;  
END  
GO  
--Create the plan guide.  
EXEC sp_create_plan_guide N'Guide3',  
    N'SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country',  
    N'OBJECT',  
    N'Sales.GetSalesOrderByCountry',  
    NULL,  
    N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
GO  
--Disable the plan guide.  
EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
GO  
--Enable the plan guide.  
EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
GO  
--Drop the plan guide.  
EXEC sp_control_plan_guide N'DROP', N'Guide3';  
```  
  
### <a name="b-disabling-all-plan-guides-in-the-current-database"></a>B. Deshabilitar todas las guías de plan de la base de datos actual.  
 En el ejemplo siguiente se deshabilitan todas las guías de plan de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_control_plan_guide N'DISABLE ALL';  
```  
  
## <a name="see-also"></a>Vea también  
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [Guías de plan](../../relational-databases/performance/plan-guides.md)  
  
  
