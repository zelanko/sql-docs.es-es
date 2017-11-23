---
title: "Establecer tiempo de estadísticas (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_TIME_TSQL
- SET STATISTICS TIME
dev_langs: TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- time [SQL Server], statement processing statistics
- SET STATISTICS TIME statement
- STATISTICS TIME option
- statements [SQL Server], statistical information
- parsing [SQL Server], SET STATISTICS TIME statement
- compile times [SQL Server]
- execution processing time [SQL Server]
ms.assetid: eec2e1cd-a29d-4cf3-a271-be9d61506f15
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 523227164984cdabcb65afa3b9213c1cb0d0f18e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra el número de milisegundos necesarios para analizar, compilar y ejecutar cada instrucción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET STATISTICS TIME { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentarios  
 Cuando SET STATISTICS TIME es ON, se muestran las estadísticas de tiempo de una instrucción. Cuando es OFF no se muestran las estadísticas de tiempo.  
  
 La opción SET STATISTICS TIME se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede calcular estadísticas precisas en el modo de fibra, que se activa cuando se habilita la **agrupación ligera** opción de configuración.  
  
 El **cpu** columna en el **sysprocesses** tabla solo se actualiza cuando se ejecuta una consulta con SET STATISTICS TIME ON. Cuando SET STATISTICS TIME es OFF, **0** se devuelve.  
  
 Las opciones ON y OFF también afectan a la columna CPU en la vista Información del proceso para la actividad actual, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Para utilizar SET STATISTICS TIME, los usuarios deben tener permisos apropiados para ejecutar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. El permiso SHOWPLAN no es necesario.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestran los tiempos de ejecución, análisis y compilación del servidor.  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS TIME ON;  
GO  
SELECT ProductID, StartDate, EndDate, StandardCost   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS TIME OFF;  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
(269 row(s) affected)  
  
SQL Server Execution Times:  
   CPU time = 0 ms,  elapsed time = 2 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET STATISTICS IO &#40; Transact-SQL &#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
