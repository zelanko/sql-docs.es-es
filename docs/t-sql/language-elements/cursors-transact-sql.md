---
title: Cursores (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], cursors
- functions [SQL Server], cursors
- cursors [SQL Server], statements
ms.assetid: 63000023-54fc-4efc-a30f-fb4d4db73aae
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 990b1bc3c44605e2b7debed67b88e5cd65770ed5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cursors-transact-sql"></a>Cursores (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones generan un conjunto de resultados completo, pero hay ocasiones cuando los resultados procesan mejores una fila a la vez. Abrir un cursor sobre un conjunto de resultados permite procesar el conjunto de resultados de fila en fila. Puede asignar un cursor a una variable o parámetro con un **cursor** tipo de datos.  
  
 Las operaciones de cursor están admitidas en las siguientes instrucciones:  
  
 [CERRAR](../../t-sql/language-elements/close-transact-sql.md)  
  
 [CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)  
  
 [CANCELA LA ASIGNACIÓN](../../t-sql/language-elements/deallocate-transact-sql.md)  
  
 [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
  
 [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [FETCH](../../t-sql/language-elements/fetch-transact-sql.md)  
  
 [ABRIR](../../t-sql/language-elements/open-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [CONJUNTO](../../t-sql/statements/set-statements-transact-sql.md)  
  
 Las siguientes funciones del sistema y procedimientos almacenados del sistema admiten también cursores:  
  
 [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)  
  
 [CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)  
  
 [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)  
  
 [sp_cursor_list](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)  
  
 [sp_describe_cursor](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)  
  
 [sp_describe_cursor_columns](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)  
  
 [sp_describe_cursor_tables](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Cursores](../../relational-databases/cursors.md)  
  
  

