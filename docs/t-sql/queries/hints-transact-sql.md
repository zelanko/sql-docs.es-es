---
title: Sugerencias (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a404f015c177fe38985c07470645e9a16e2cb716
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="hints-transact-sql"></a>Sugerencias (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Las sugerencias son opciones o estrategias especificadas para que el procesador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las aplique en instrucciones SELECT, INSERT, UPDATE o DELETE. Las sugerencias reemplazan a cualquier plan de ejecución que pueda seleccionar el optimizador de consultas para una consulta.  
  
> [!CAUTION]  
>  Puesto que el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecciona normalmente el mejor plan de ejecución para una consulta, se recomienda que las sugerencias \<join_hint>, \<query_hint> y \<table_hint> solamente se usen como último recurso y por parte de desarrolladores y administradores de bases de datos experimentados.
  
 En esta sección se describen las sugerencias siguientes:  
  
-   [Sugerencias de combinación](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Sugerencias de consulta](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Sugerencia de tabla](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
