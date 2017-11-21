---
title: '@@DBTS (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 4a90150c55cdeb89788fdb86faf8aef8a1efdcd2
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40dbts-transact-sql"></a>&#x40;&#x40;DBTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el valor del tipo de datos **timestamp** actual de la base de datos actual. Se garantiza que la marca de tiempo es única en la base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto
**varbinary**
  
## <a name="remarks"></a>Comentarios  
@@DBTS devuelve el valor de marca de tiempo utilizó por última vez de la base de datos actual. Se genera un nuevo valor de marca de tiempo cuando se inserta o actualiza una fila con una columna de tipo **timestamp** .
  
El @@DBTS función no se ve afectada por los cambios en los niveles de aislamiento de transacción.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelve el valor actual **timestamp** desde el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>Vea también
[Funciones de configuración &#40; Transact-SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[Simultaneidad de cursor &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40; Transact-SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  

