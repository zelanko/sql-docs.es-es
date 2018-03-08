---
title: SET NOCOUNT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NOCOUNT
- SET_NOCOUNT_TSQL
- NOCOUNT_TSQL
- SET NOCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- NOCOUNT option
- number of rows affected by statement
- row affected by statements [SQL Server]
- counting rows
- SET NOCOUNT statement
ms.assetid: eb3e6727-cb26-4bc2-84c7-171cbac02029
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9e90ba175c632ff9a8a494e154dae057fb11b0c8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="set-nocount-transact-sql"></a>SET NOCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Evita que se devuelva el mensaje que muestra el recuento del número de filas afectadas por una instrucción o un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] como parte del conjunto de resultados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET NOCOUNT { ON | OFF }   
```  
  
## <a name="remarks"></a>Comentarios  
 Si se establece SET NOCOUNT en ON, no se devuelve el recuento. Cuando SET NOCOUNT es OFF, sí se devuelve ese número.  
  
 El @@ROWCOUNT función se actualiza incluso cuando SET NOCOUNT es ON.  
  
 SET NOCOUNT ON impide el envío al cliente de mensajes DONE_IN_PROC por cada instrucción de un procedimiento almacenado. En los procedimientos almacenados que contengan varias instrucciones que no devuelven mucha información real o en los procedimientos que contengan bucles de [!INCLUDE[tsql](../../includes/tsql-md.md)], establecer SET NOCOUNT en ON puede suponer una mejora significativa del rendimiento, ya que el tráfico de la red se reduce en gran medida.  
  
 La configuración especificada por SET NOCOUNT está activa en tiempo de ejecución, no en tiempo de análisis.  
  
 Para ver la configuración actual de este valor, ejecute la consulta siguiente.  
  
```  
DECLARE @NOCOUNT VARCHAR(3) = 'OFF';  
IF ( (512 & @@OPTIONS) = 512 ) SET @NOCOUNT = 'ON';  
SELECT @NOCOUNT AS NOCOUNT;  
  
```  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo no se muestra el mensaje que indica el número de filas afectado.  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT OFF;  
GO  
-- Display the count message.  
SELECT TOP(5)LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- SET NOCOUNT to ON to no longer display the count message.  
SET NOCOUNT ON;  
GO  
SELECT TOP(5) LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- Reset SET NOCOUNT to OFF  
SET NOCOUNT OFF;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
