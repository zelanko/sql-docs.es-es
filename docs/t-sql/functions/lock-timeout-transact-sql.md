---
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 10e21a229628f8c24e35e846a07ab0b847a8ff85
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822929"
---
# <a name="x40x40lock_timeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el valor actual de tiempo de espera de bloqueo en milisegundos para la sesión actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **integer**  
  
## <a name="remarks"></a>Observaciones  
 SET LOCK_TIMEOUT permite a una aplicación establecer el tiempo máximo que espera una instrucción en un recurso bloqueado. Cuando una instrucción ha esperado más tiempo que el indicado en LOCK_TIMEOUT, la instrucción bloqueada se cancela automáticamente y se devuelve un mensaje de error a la aplicación.  
  
 @@LOCK_TIMEOUT devuelve un valor de -1 si SET LOCK_TIMEOUT aún no se ha ejecutado en la sesión actual.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra el conjunto de resultados cuando no se establece un valor en LOCK_TIMEOUT.  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 En este ejemplo se establece LOCK_TIMEOUT en 1800 milisegundos y, luego, se llama a @@LOCK_TIMEOUT.  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones de configuración &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
