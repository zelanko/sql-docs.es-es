---
title: Sys. sp_rda_reconcile_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 504085ff53415a7cf84bdb4aabf5eff567391a0c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827407"
---
# <a name="syssp_rda_reconcile_indexes-transact-sql"></a>Sys. sp_rda_reconcile_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Pone en cola una tarea de esquema para conciliar los índices en la tabla remota. Una vez que la tarea finaliza correctamente, la tabla remota tiene los mismos índices que existen en la tabla habilitada para Stretch local.  
  
 Si hay otra tarea en cola para conciliar los índices cuando se llama a **sp_rda_reconcile_indexes**, este procedimiento almacenado no pone en cola una tarea duplicada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @objname =] *' objName '*  
 Es el nombre completo o no completo de la tabla habilitada para stretch para la que desea conciliar los índices. Las comillas solo son necesarias si se especifica un objeto calificado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="see-also"></a>Consulte también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
