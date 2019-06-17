---
title: Migrar los planes de consulta | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66f1f8f57dca3ad2edba3f4b63100b2de3ae5659
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779117"
---
# <a name="migrate-query-plans"></a>Migrar los planes de consulta
  En la mayoría de los casos, al actualizar una base de datos a la versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se obtendrá una mejora del rendimiento de las consultas. No obstante, si tiene consultas de gran importancia que se han optimizado cuidadosamente con el fin de obtener el máximo rendimiento, es probable que desee conservar los planes de consulta de dichas consultas antes de llevar a cabo la actualización mediante la creación de una guía de plan para cada una de ellas. Si tras la actualización, el optimizador de consultas elige un plan menos eficiente para una o varias de las consultas, podrá habilitar las guías de plan y obligar al optimizador de consultas a utilizar los planes previos a la actualización.  
  
 Siga estos pasos para crear planes de guía antes de llevar a cabo la actualización:  
  
1.  Registre el plan actual para cada consulta de misión crítica utilizando el [sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) procedimiento almacenado y especificar el plan de consulta en la sugerencia de consulta USE PLAN.  
  
2.  Compruebe que la guía de plan se aplica a la consulta.  
  
3.  Actualice la base de datos a la versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Los planes se conservan en las guías de plan residentes en la base en datos actualizada y sirven de reserva en caso de regresión de los planes tras la actualización.  
  
     Recomendamos no habilitar las guías de plan tras la actualización, ya que es posible que se pierdan oportunidades de conseguir mejores planes en la nueva versión o recompilaciones beneficiosas gracias a las estadísticas actualizadas.  
  
4.  Si tras la actualización se escogen planes menos eficientes, active todas las guías de plan o bien solo un subconjunto de ellas con el fin de invalidar los nuevos planes.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo registrar un plan para una consulta antes de la actualización por medio de la creación de una guía de plan.  
  
### <a name="step-1-collect-the-plan"></a>Paso 1: Recopilar el Plan  
 El plan de consulta registrado en la guía de plan debe estar en formato XML. Es posible generar planes de consulta en formato XML de las siguientes formas:  
  
-   [SET SHOWPLAN_XML](/sql/t-sql/statements/set-showplan-xml-transact-sql)  
  
-   [SET STATISTICS XML](/sql/t-sql/statements/set-statistics-xml-transact-sql)  
  
-   Consultando la columna query_plan de la [sys.dm_exec_query_plan](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql) función de administración dinámica.  
  
-   El [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [Showplan XML](../../relational-databases/event-classes/showplan-xml-event-class.md), [Showplan XML Statistics Profile](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md), y [Showplan XML For Query Compile](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md) las clases de eventos.  
  
 En el siguiente ejemplo se recopila el plan de consulta para la instrucción `SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;` mediante la consulta a vistas de administración dinámica.  
  
```  
USE AdventureWorks;  
GO  
SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%';  
GO  
```  
  
### <a name="step-2-create-the-plan-guide-to-force-the-plan"></a>Paso 2: Crear la Guía de Plan para forzar el Plan  
 Utilizando el plan de consulta con formato XML (obtenido mediante cualquiera de los métodos explicados) en la guía de plan, copie y pegue el plan de consulta como un literal de cadena en la sugerencia de consulta USE PLAN especificada en la cláusula OPTION de sp_create_plan_guide.  
  
 Dentro del propio plan XML, escape las comillas (') que aparezcan en el plan antes de crear la guía de plan, insertando para ello unas segundas comillas. Por ejemplo, a un plan que contiene `WHERE A.varchar = 'This is a string'` habrá que agregarle unas segundas comillas para que el código quede `WHERE A.varchar = ''This is a string''`.  
  
 En el ejemplo siguiente se crea una guía de plan para el plan de consulta recopilado en el paso 1, y se inserta el XML Showplan par la consulta en el parámetro `@hints`. Por razones de brevedad, el ejemplo solo incluye resultados parciales de Showplan.  
  
```  
EXECUTE sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',  
@type = N'SQL',  
@module_or_batch = NULL,  
@params = NULL,  
@hints = N'OPTION(USE PLAN N''<ShowPlanXML xmlns=''''https://schemas.microsoft.com/sqlserver/2004/07/showplan''''   
    Version=''''0.5'''' Build=''''9.00.1116''''>  
    <BatchSequence><Batch><Statements><StmtSimple>  
    ...  
    </StmtSimple></Statements></Batch>  
    </BatchSequence></ShowPlanXML>'')';  
GO  
```  
  
### <a name="step-3-verify-that-the-plan-guide-is-applied-to-the-query"></a>Paso 3: Compruebe que la Guía de Plan se aplica a la consulta  
 Vuelva a ejecutar la consulta y examine el plan de consulta generado. Observará que el plan coincide con el plan especificado en la guía de plan.  
  
## <a name="see-also"></a>Vea también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Sugerencias de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guías de plan](../../relational-databases/performance/plan-guides.md)  
  
  
