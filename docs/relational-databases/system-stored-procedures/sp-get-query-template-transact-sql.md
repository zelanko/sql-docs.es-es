---
title: sp_get_query_template (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17fa74789d172177747ed398c43ae5ac9f1f1db5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spgetquerytemplate-transact-sql"></a>sp_get_query_template (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el formato con parámetros de una consulta. Los resultados devueltos simulan el formato con parámetros de un consulta resultante cuando se utiliza la parametrización forzada. sp_get_query_template se utiliza principalmente al crear guías de plan TEMPLATE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>Argumentos  
 '*query_text*'  
 Es la consulta para la que se va a generar la versión con parámetros. '*query_text*' debe incluirse entre comillas simples y precedida por el especificador Unicode n. N'*query_text*' es el valor asignado a la @querytext parámetro. Esto es de tipo **nvarchar (max)**.  
  
 @templatetext  
 Es un parámetro de salida de tipo **nvarchar (max)**, suministrado como se indica, para recibir el formulario parametrizado de *query_text* como un literal de cadena.  
  
 @parameters  
 Es un parámetro de salida de tipo **nvarchar (max)**, suministrado como se indica, para recibir un literal de cadena de los tipos de datos y los nombres de parámetro con parámetros en @templatetext.  
  
## <a name="remarks"></a>Comentarios  
 sp_get_query_template devuelve un error cuando se produce lo siguiente:  
  
-   No se parametriza los valores literales constantes en *query_text*.  
  
-   *query_text* es NULL, no una cadena de Unicode, no es válida sintácticamente o no se pueden compilar.  
  
 Si sp_get_query_template devuelve un error, no se modifican los valores de la @templatetext y @parameters parámetros de salida.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol de base de datos public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el formato con parámetros de una consulta que contiene dos valores literales constantes.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @my_templatetext nvarchar(max)  
DECLARE @my_parameters nvarchar(max)  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
        FROM Production.ProductModel pm   
        INNER JOIN Production.ProductInventory pi  
        ON pm.ProductModelID = pi.ProductID  
        WHERE pi.ProductID = 2  
        GROUP BY pi.ProductID, pi.Quantity  
        HAVING SUM(pi.Quantity) > 400',  
@my_templatetext OUTPUT,  
@my_parameters OUTPUT;  
SELECT @my_templatetext;  
SELECT @my_parameters;  
```  
  
 Estos son los resultados con parámetros del parámetro `@my_templatetext``OUTPUT`:  
  
 `select pi . ProductID , SUM ( pi . Quantity ) as Total`  
  
 `from Production . ProductModel pm`  
  
 `inner join Production . ProductInventory pi`  
  
 `on pm . ProductModelID = pi . ProductID`  
  
 `where pi . ProductID = @0`  
  
 `group by pi . ProductID , pi . Quantity`  
  
 `having SUM ( pi . Quantity ) > 400`  
  
 Observe que el primer literal constante, `2`, se convierte en un parámetro. El segundo literal, `400`, no se convierte porque está en una cláusula `HAVING`. Los resultados devueltos por sp_get_query_template simulan la forma con parámetros de una consulta cuando la opción PARAMETERIZATION de ALTER DATABASE está establecida en FORCED.  
  
 Estos son los resultados con parámetros del parámetro `@my_parameters OUTPUT`:  
  
```  
@0 int  
```  
  
> [!NOTE]  
>  El orden y el nombre de los parámetros en la salida de sp_get_query_template puede variar en la ingeniería de corrección rápida, el Service Pack y las actualizaciones de versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las actualizaciones también pueden hacer que se parametrice un conjunto distinto de literales constantes para la misma consulta y que se aplique un espaciado diferente a los resultados de ambos parámetros de salida.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Especificar el comportamiento de parametrización de consultas por medio de guías de plan](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
