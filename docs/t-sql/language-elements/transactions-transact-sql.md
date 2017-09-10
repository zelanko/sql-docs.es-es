---
title: Transacciones (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Transactions
- Transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactions [SQL Server]
- transactions [SQL Server], about transactions
- UOW [SQL Server]
- unit of work [SQL Server]
ms.assetid: 1485c375-921a-42af-a871-bb333cc08d3e
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8660d0ac8d6205a94fdab24f41e41bac40a8671e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="transactions-transact-sql"></a>Transacciones (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Una transacción es una unidad única de trabajo. Si una transacción tiene éxito, todas las modificaciones de los datos realizadas durante la transacción se confirman y se convierten en una parte permanente de la base de datos. Si una transacción encuentra errores y debe cancelarse o revertirse, se borran todas las modificaciones de los datos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciona en los siguientes tres modos de transacción.  
  
 Transacciones de confirmación automática  
 Cada instrucción individual es una transacción.  
  
 Transacciones explícitas  
 Cada transacción se inicia explícitamente con la instrucción BEGIN TRANSACTION y se termina explícitamente con una instrucción COMMIT o ROLLBACK.  
  
 Transacciones implícitas  
 Se inicia implícitamente una nueva transacción cuando se ha completado la anterior, pero cada transacción se completa explícitamente con una instrucción COMMIT o ROLLBACK.  
  
 Transacciones de ámbito de lote  
 Una transacción implícita o explícita de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se inicia en una sesión de MARS (conjuntos de resultados activos múltiples), que solo es aplicable a MARS, se convierte en una transacción de ámbito de lote. Si no se confirma o revierte una transacción de ámbito de lote cuando se completa el lote, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la revierte automáticamente.  
  
## <a name="in-this-section"></a>En esta sección  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona las siguientes instrucciones de transacción.  
  
|||  
|-|-|  
|[BEGIN DISTRIBUTED TRANSACTION](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)|[ROLLBACK TRANSACTION](../../t-sql/language-elements/rollback-transaction-transact-sql.md)|  
|[COMENZAR LA TRANSACCIÓN](../../t-sql/language-elements/begin-transaction-transact-sql.md)|[ROLLBACK WORK](../../t-sql/language-elements/rollback-work-transact-sql.md)|  
|[CONFIRMAR TRANSACCIÓN](../../t-sql/language-elements/commit-transaction-transact-sql.md)|[GUARDE LA TRANSACCIÓN](../../t-sql/language-elements/save-transaction-transact-sql.md)|  
|[CONFIRMAR EL TRABAJO](../../t-sql/language-elements/commit-work-transact-sql.md)||  
  
## <a name="see-also"></a>Vea también  
 [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
