---
title: Transacciones (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/25/2017
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
ms.sourcegitcommit: 0463d237614b25667c8402da70b7c5e4217d4ef5
ms.openlocfilehash: c09104746dff6c34d94192217b8f2635cb0adc67
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="transactions-transact-sql"></a>Transacciones (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Una transacción es una unidad única de trabajo. Si una transacción tiene éxito, todas las modificaciones de los datos realizadas durante la transacción se confirman y se convierten en una parte permanente de la base de datos. Si una transacción encuentra errores y debe cancelarse o revertirse, se borran todas las modificaciones de los datos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]opera en los siguientes modos de transacción:  
  
 Transacciones de confirmación automática  
 Cada instrucción individual es una transacción.  
  
 Transacciones explícitas  
 Cada transacción se inicia explícitamente con la instrucción BEGIN TRANSACTION y se termina explícitamente con una instrucción COMMIT o ROLLBACK.  
  
 Transacciones implícitas  
 Se inicia implícitamente una nueva transacción cuando se ha completado la anterior, pero cada transacción se completa explícitamente con una instrucción COMMIT o ROLLBACK.  
  
 Transacciones de ámbito de lote  
 Una transacción implícita o explícita de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se inicia en una sesión de MARS (conjuntos de resultados activos múltiples), que solo es aplicable a MARS, se convierte en una transacción de ámbito de lote. Si no se confirma o revierte una transacción de ámbito de lote cuando se completa el lote, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la revierte automáticamente.  

> [!NOTE] 
> Para conocer consideraciones especiales relacionadas con los productos de almacenamiento de datos, vea [transacciones (almacenamiento de datos de SQL)](transactions-sql-data-warehouse.md).   

## <a name="in-this-section"></a>En esta sección  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]proporciona las siguientes instrucciones de transacción:  
  
|||  
|-|-|  
|[BEGIN DISTRIBUTED TRANSACTION](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)|[ROLLBACK TRANSACTION](../../t-sql/language-elements/rollback-transaction-transact-sql.md)|  
|[BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md)|[ROLLBACK WORK](../../t-sql/language-elements/rollback-work-transact-sql.md)|  
|[COMMIT TRANSACTION](../../t-sql/language-elements/commit-transaction-transact-sql.md)|[SAVE TRANSACTION](../../t-sql/language-elements/save-transaction-transact-sql.md)|  
|[COMMIT WORK](../../t-sql/language-elements/commit-work-transact-sql.md)||  
  
## <a name="see-also"></a>Vea también  
 [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

