---
title: '@@DBTS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 9d06a019d162c6c8455efd1c85e49ec109763d0a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82804726"
---
# <a name="x40x40dbts-transact-sql"></a>&#x40;&#x40;DBTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta función devuelve el valor del tipo de datos **timestamp** actual de la base de datos actual. La base de datos actual tendrá un valor de marca de tiempo único garantizado.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>Tipos de valores devueltos
**varbinary**
  
## <a name="remarks"></a>Observaciones  
@@DBTS devuelve el último valor de marca de tiempo de la base de datos actual que se ha usado. Cuando se inserta o actualiza una fila con una columna de tipo **timestamp** se genera un valor de marca de tiempo nuevo.
  
Los cambios en los niveles de aislamiento de transacción no afectan a la función @@DBTS.
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se devuelve el valor actual de **timestamp** de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>Consulte también
[Funciones de configuración &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[Cursor Concurrency &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md) (Simultaneidad de cursor [ODBC])  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  
