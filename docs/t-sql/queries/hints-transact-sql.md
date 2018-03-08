---
title: Sugerencias (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bddb86e431c252a45e68a52a4e7192d9fcbc5006
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="hints-transact-sql"></a>Sugerencias (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Las sugerencias son opciones o estrategias especificadas para que el procesador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las aplique en instrucciones SELECT, INSERT, UPDATE o DELETE. Las sugerencias reemplazan a cualquier plan de ejecución que pueda seleccionar el optimizador de consultas para una consulta.  
  
> [!CAUTION]  
>  Dado que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] optimizador de consultas normalmente selecciona el mejor plan de ejecución para una consulta, se recomienda que \<las sugerencias join_hint >, \<query_hint >, y \<sugerenciatabla > se usa solo como último recurso por experimentados los programadores y administradores de base de datos.
  
 En esta sección se describen las sugerencias siguientes:  
  
-   [Sugerencias de combinación](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Sugerencias de consulta](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Sugerencia de tabla](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
