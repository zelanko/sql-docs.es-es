---
title: Especificar el comportamiento de parametrización de consultas por medio de guías de plan | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 06ed5433d23501016a0ea308c9238fcf7bc1b3c1
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582072"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>Especificar el comportamiento de parametrización de consultas por medio de guías de plan
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando la opción de base de datos PARAMETERIZATION se establece en SIMPLE, el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede optar por parametrizar las consultas. Esto quiere decir que todos los valores literales incluidos en una consulta se sustituirán por parámetros. Este proceso se conoce como parametrización simple. Cuando la parametrización SIMPLE está habilitada, no se pueden controlar las consultas que se parametrizarán y las que no. No obstante, puede especificar que todas las consultas de una base de datos se parametricen estableciendo la opción PARAMETERIZATION de base de datos en FORCED. Este proceso se conoce como parametrización forzada.  
  
 Puede cambiar el comportamiento de parametrización de una base de datos por medio de guías de plan tal y como se indica a continuación:  
  
-   Cuando la opción PARAMETERIZATION de base de datos se establece en SIMPLE, puede especificar que se intente realizar una parametrización forzada en una clase determinada de consultas. Para ello, cree una guía de plan TEMPLATE en la consulta con parámetros y especifique la sugerencia de consulta PARAMETERIZATION FORCED en el procedimiento almacenado [sp_create_plan_guide](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) . Puede considerar este tipo de guía de plan como una forma de habilitar la parametrización forzada solo para una determinada clase de consultas, no para todas.  
  
-   Cuando la opción PARAMETERIZATION de la base de datos se establece en FORCED, puede especificar que para una clase determinada de consultas se intente solamente realizar la parametrización simple, y no la parametrización forzada. Para ello, cree una guía de plan TEMPLATE en la consulta con parametrización forzada y especifique la sugerencia de consulta PARAMETERIZATION SIMPLE en el procedimiento almacenado **sp_create_plan_guide**.  
  
 Fíjese en la consulta siguiente en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 Como administrador de base de datos, ha decidido que no desea habilitar la parametrización forzada para todas las consultas de la base de datos. No obstante, desea evitar los costos de compilación en todas las consultas que son sintácticamente equivalentes a consultas anteriores y que solo difieren en los valores literales constantes. En otras palabras, desea que la consulta se parametrice para poder reutilizar un plan de consulta. En este caso, siga los pasos siguientes:  
  
1.  Recupere la consulta con parámetros. El único modo seguro de obtener este valor para usarlo en **sp_create_plan_guide** consiste en usar el procedimiento almacenado del sistema [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) .  
  
2.  Cree la guía de plan en la consulta con parámetros, especificando la sugerencia de consulta PARAMETERIZATION FORCED.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    > [!IMPORTANT]  
    >  As part of parameterizing a query, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assigns a data type to the parameters that replace the literal values, depending on the value and size of the literal. The same process occurs to the value of the constant literals passed to the **@stmt** output parameter of **sp_get_query_template**. Because the data type specified in the **@params** argument of **sp_create_plan_guide** must match that of the query as it is parameterized by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], you may have to create more than one plan guide to cover the complete range of possible parameter values for the query.  
  
 El siguiente script puede utilizarse para obtener la consulta con parámetros y, a continuación, crear una guía de plan en ella.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 Asimismo, en una base de datos en la que ya esté habilitada la parametrización forzada, puede asegurarse de que la consulta de ejemplo y otras consultas sintácticamente equivalentes, salvo por sus valores literales constantes, tengan parámetros definidos según las reglas de parametrización simple. Para ello, especifique PARAMETERIZATION SIMPLE, en lugar de PARAMETERIZATION FORCED, en la cláusula OPTION.  
  
> [!NOTE]  
>  Las guías de plan TEMPLATE asocian las instrucciones con las consultas enviadas en lotes que están formadas solamente por una instrucción. Las instrucciones incluidas en lotes de varias instrucciones no tienen la posibilidad de ser elegidas por las guías de plan TEMPLATE.  
  
  
