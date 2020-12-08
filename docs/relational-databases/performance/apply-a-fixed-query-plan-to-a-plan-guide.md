---
title: Aplicar un plan de consulta fijo a una guía de plan | Microsoft Docs
description: Obtenga información sobre cómo aplicar un plan de consulta fijo a una guía de plan del tipo OBJECT o SQL en SQL Server. En este ejemplo se crea una guía de plan para una instrucción SQL ad hoc sencilla.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: bbf401f9-af7c-48e7-8a43-bf25e8af2fd7
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 550933e8c8152bd021c871d4e466f1b9fafb3907
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505452"
---
# <a name="apply-a-fixed-query-plan-to-a-plan-guide"></a>Aplicar un plan de consulta fijo a una guía de plan
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Puede aplicar un plan de consulta fijo a una guía de plan del tipo OBJECT o SQL. Las guías de plan que se aplican a un plan de consulta fijo resultan útiles cuando ya se tiene constancia de un plan de ejecución existente cuyo rendimiento es mejor que el del seleccionado por el optimizador para una consulta determinada.  
  
 El ejemplo siguiente crea una guía de plan para una instrucción SQL ad hoc sencilla. El plan de consulta deseado para esta instrucción se proporciona en la guía de plan si se especifica el plan de presentación XML para la consulta directamente en el parámetro `@hints` . El ejemplo ejecuta primero la instrucción SQL para generar un plan en la memoria caché del plan. Para los fines de este ejemplo, se supone que el plan generado es el plan deseado y que no se requiere ninguna optimización adicional de la consulta. El plan de presentación XML para la consulta se obtiene consultando las vistas de administración dinámica `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`y `sys.dm_exec_text_query_plan` y está asignado a la variable `@xml_showplan` . A continuación, la variable `@xml_showplan` se pasa a la instrucción `sp_create_plan_guide` en el parámetro `@hints` . O bien, puede crear una guía de plan a partir de un plan de consulta de la memoria caché del plan con el procedimiento almacenado [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = @xml_showplan;  
GO  
```  
  
  
