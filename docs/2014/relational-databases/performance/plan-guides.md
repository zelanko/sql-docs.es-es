---
title: Guías de plan | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- SQL plan guides
- OPTIMIZE FOR query hint
- RECOMPILE query hint
- OBJECT plan guide
- plan guides [SQL Server], about plan guides
- OPTION clause
- plan guides [SQL Server]
- USE PLAN query hint
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f6b2bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ea11c177533a6101bb0654ca0450e85ea855d9a5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085725"
---
# <a name="plan-guides"></a>Guías de plan
  Las guías de plan permiten optimizar el rendimiento de las consultas cuando no pueda o no desee cambiar directamente el texto de la consulta real en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Las guías de plan influyen en la optimización de las consultas adjuntando sugerencias de consulta o un plan de consulta fijo para ellas. Las guías de plan pueden ser de gran utilidad cuando el rendimiento de un pequeño subconjunto de consultas de una aplicación de base de datos proporcionado por otro proveedor no es el esperado. En la guía de plan, se especifica la instrucción Transact-SQL que se desea optimizar y además una cláusula OPTION que incluye las sugerencias de consulta que se desean usar o un plan de consulta específico con el que desea optimizar la consulta. Cuando la consulta se ejecuta, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hace coincidir la instrucción Transact-SQL con la guía de plan y además adjunta en tiempo de ejecución la cláusula OPTION a la consulta o usa el plan de consulta especificado.  
  
 El número total de guías de plan que se pueden crear solo está limitado por los recursos de los que disponga el sistema. No obstante, las guías de plan deberían limitarse a aquellas consultas de gran importancia cuyo rendimiento se desea mejorar o estabilizar. No se deben usar las guías de plan para influenciar la mayor parte de la carga de la consulta de una aplicación implementada.  
  
> [!NOTE]  
>  Las guías de plan no se pueden usar en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Las guías de plan son visibles en todas las ediciones. También se pueden adjuntar bases de datos que incluyen guías de plan a cualquier versión. Las guías de plan permanecen intactas cuando se restaura o adjunta una base de datos a una versión actualizada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="types-of-plan-guides"></a>Tipos de guías de plan  
 Se pueden crear los siguientes tipos de guías de plan.  
  
 OBJECT [guía de plan]  
 Una guía de plan OBJECT compara las consultas que se ejecutan en el contexto de procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] , funciones escalares definidas por el usuario, funciones definidas por el usuario con valores de tabla de múltiples instrucciones y desencadenadores DML.  
  
 Suponga que el siguiente procedimiento almacenado, que usa el parámetro `@Country`_`region` , está en una aplicación de base de datos que se implementa con la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
CREATE PROCEDURE Sales.GetSalesOrderByCountry (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h, Sales.Customer AS c,   
        Sales.SalesTerritory AS t  
    WHERE h.CustomerID = c.CustomerID  
        AND c.TerritoryID = t.TerritoryID  
        AND CountryRegionCode = @Country_region  
END;  
```  
  
 Asuma que este procedimiento almacenado ha sido compilado y optimizado para `@Country`_`region = N'AU'` (Australia). Sin embargo, dado hay relativamente pocos pedidos de ventas que se originen en Australia, el rendimiento se reduce cuando la consulta ejecuta usando valores para los parámetros que se corresponden con países con más pedidos de ventas. Dado que el mayor número de pedidos de ventas se origina en Estados Unidos, el rendimiento de un plan de consulta generado para `@Country`\_`region = N'US'` será probablemente mejor para todos los valores posibles del parámetro `@Country`\_`region` .  
  
 Puede solucionar este problema modificando el procedimiento almacenado y agregando la sugerencia de consulta `OPTIMIZE FOR` a la consulta. No obstante, puesto que el procedimiento almacenado se encuentra en una aplicación implementada, no puede modificar directamente el código de la aplicación. En su lugar, puede crear la guía de plan siguiente en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT *FROM Sales.SalesOrderHeader AS h,  
        Sales.Customer AS c,  
        Sales.SalesTerritory AS t  
        WHERE h.CustomerID = c.CustomerID   
            AND c.TerritoryID = t.TerritoryID  
            AND CountryRegionCode = @Country_region',  
@type = N'OBJECT',  
@module_or_batch = N'Sales.GetSalesOrderByCountry',  
@params = NULL,  
@hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
 Cuando se ejecute la consulta especificada en la instrucción `sp_create_plan_guide` , se modificará la consulta antes de la optimización para incluir la cláusula `OPTIMIZE FOR (@Country = N''US'')` .  
  
 Guía de plan SQL  
 Una guía de plan de SQL compara las consultas que se ejecutan en el contexto de instrucciones independientes de [!INCLUDE[tsql](../../includes/tsql-md.md)] y lotes que no forman parte de un objeto de base de datos. Las guías de plan basadas en SQL también se pueden usar para comparar consultas que se parametrizan en un formulario especificado. Las guías de plan de SQL se aplican a las instrucciones y lotes independientes de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Con frecuencia, las aplicaciones envían esas instrucciones usando el procedimiento almacenado del sistema [sp_executesql](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql) . Considere, por ejemplo, el siguiente lote independiente:  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 Para evitar que se genere un plan de ejecución paralelo en esta consulta, cree la siguiente guía de plan y establezca la sugerencia de consulta `MAXDOP` en `1` en el parámetro `@hints` .  
  
```  
sp_create_plan_guide   
@name = N'Guide2',   
@stmt = N'SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC',  
@type = N'SQL',  
@module_or_batch = NULL,   
@params = NULL,   
@hints = N'OPTION (MAXDOP 1)';  
```  
  
> [!IMPORTANT]  
>  Los valores que se proporcionan para los argumentos `@module_or_batch` y `@params` de la instrucción `sp_create_plan guide` deben coincidir con el texto correspondiente enviado en la consulta real. Para obtener más información, vea [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) y [Usar SQL Server Profiler para crear y probar guías de plan](plan-guides.md).  
  
 También se pueden crear guías de plan SQL en consultas que se parametrizan en el mismo formulario cuando se establece el valor de la opción SET de base de datos PARAMETERIZATION en FORCED, o cuando se crea una guía de plan TEMPLATE en la que se especifica que debe parametrizarse una clase de consultas.  
  
 TEMPLATE, guía de plan  
 Una guía de plan TEMPLATE compara consultas independientes que se parametrizan en un formulario especificado. Estas guías de plan se usan para reemplazar la opción PARAMETERIZATION actual de una base de datos para una clase de consultas por medio de SET.  
  
 Puede crear una guía de plan TEMPLATE en cualquiera de las situaciones siguientes:  
  
-   Se ha establecido el valor de la opción PARAMETRIZATION de la base de datos en FORCED mediante el mandato SET, pero hay consultas que desea compilar según las reglas parametrización simple.  
  
-   Se ha establecido el valor de la opción PARAMETERIZATION de la base de datos en SIMPLE (el valor predeterminado), pero desea que intente la parametrización forzada en una clase de consultas.  
  
## <a name="plan-guide-matching-requirements"></a>Requisitos de coincidencia de la guía de plan  
 Las guías de plan tienen como ámbito la base de datos en la que se crean. Por tanto, solo se pueden buscar las coincidencias con la consulta de las guías de plan que existen en la base de datos actual cuando se ejecuta una consulta. Por ejemplo, si [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] es la base de datos actual y se ejecuta la consulta siguiente:  
  
 `SELECT FirstName, LastName FROM Person.Person;`  
  
 Solo las guías de plan de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] serán aptas para buscar las coincidencias con esta consulta. No obstante, si la base de datos actual es [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y se ejecutan las instrucciones siguientes:  
  
 `USE DB1;`  
  
 `SELECT FirstName, LastName FROM Person.Person;`  
  
 Solo las guías de plan de `DB1` serán aptas para buscar las coincidencias con la consulta, puesto que la consulta se ejecuta en el contexto de `DB1`.  
  
 En el caso de las guías de plan basadas en SQL o TEMPLATE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] examina los valores para los argumentos @module_or_batch y @params con una consulta, comparando ambos valores carácter a carácter. Esto significa que se debe proporcionar el texto exactamente como lo recibe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el lote real.  
  
 Cuando @type = 'SQL' y @module_or_batch se establece en NULL, el valor de @module_or_batch se establece en el valor de @stmt. Esto significa que el valor de *statement_text* debe proporcionarse en formato idéntico, carácter a carácter, en que se envía a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para facilitar esta concordancia no se realiza ninguna conversión interna.  
  
 Cuando una guía de plan normal (SQL u OBJECT) y una guía de plan TEMPLATE se pueden aplicar a una instrucción, solo se utilizará la guía de plan normal.  
  
> [!NOTE]  
>  El lote que contiene la instrucción en la que quiere crear una guía de plan no puede contener una instrucción USE *database* .  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>Efecto de la guía de plan en la caché del plan  
 Al crear una guía de plan en un módulo, se quita el plan de consulta para dicho módulo de la caché del plan. Al crear una guía de plan de tipo OBJECT o SQL en un lote, se quita el plan de consulta para un lote que tiene el mismo valor hash. Al crear una guía de plan de tipo TEMPLATE, se quitan todos los lotes de instrucción única de la memoria caché del plan dentro de esa base de datos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Tema|  
|----------|-----------|  
|Describe cómo crear una guía de plan.|[Crear una nueva guía de plan](create-a-new-plan-guide.md)|  
|Describe cómo crear una guía de plan para consultas con parámetros.|[Crear una guía de plan para consultas parametrizadas](create-a-plan-guide-for-parameterized-queries.md)|  
|Describe cómo controlar el comportamiento de parametrización de consultas mediante guías de plan.|[Especificar el comportamiento de parametrización de consultas por medio de guías de plan](specify-query-parameterization-behavior-by-using-plan-guides.md)|  
|Describe cómo incluir un plan de consulta fijo en una guía de plan.|[Aplicar un plan de consulta fijo a una guía de plan](apply-a-fixed-query-plan-to-a-plan-guide.md)|  
|Describe cómo especificar sugerencias de consulta en una guía de plan.|[Asociar sugerencias de consulta a una guía de plan](attach-query-hints-to-a-plan-guide.md)|  
|Describe cómo ver las propiedades de la guía de plan.|[Ver propiedades de la guía de plan](view-plan-guide-properties.md)|  
|Describe cómo usar SQL Server Profiler para crear y probar guías de plan.|[Usar SQL Server Profiler para crear y probar guías de plan](plan-guides.md)|  
|Describe cómo validar las guías de plan.|[Validar guías de planes tras una actualización](validate-plan-guides-after-upgrade.md)|  
  
## <a name="see-also"></a>Vea también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql)   
 [sys.plan_guides &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-plan-guides-transact-sql)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql)  
  
  
