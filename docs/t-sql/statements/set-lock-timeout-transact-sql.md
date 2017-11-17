---
title: SET LOCK_TIMEOUT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 754242a86367b07b98caa9f70f457b70d0840075
ms.openlocfilehash: 3de86c7f33afd6e708ad8e773470ec650e092d2c
ms.contentlocale: es-es
ms.lasthandoff: 09/12/2017

---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica el número de milisegundos que una instrucción espera a que se libere un bloqueo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>Argumentos  
 *timeout_period*  
 Es el número de milisegundos que transcurrirán antes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error de bloqueo. El valor -1 (predeterminado) indica que no hay límite de espera (es decir que se espera indefinidamente).  
  
 Cuando se espera un bloqueo durante más tiempo que el indicado, se devuelve un error. El valor 0 significa no esperar y devolver un mensaje en cuanto se encuentre un bloqueo.  
  
## <a name="remarks"></a>Comentarios  
 Al principio de una conexión, este valor es -1. Después de cambiarlo, el nuevo valor permanece en vigor para el resto de la conexión.  
  
 La opción SET LOCK_TIMEOUT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 La sugerencia de bloqueo READPAST es una alternativa a esta opción SET.  
  
 Las instrucciones CREATE DATABASE, ALTER DATABASE y DROP DATABASE no respetan el parámetro SET LOCK_TIMEOUT.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>R: establecer el tiempo de espera de bloqueo 1.800 milisegundos  
 En el ejemplo siguiente se establece el período de tiempo de espera de bloqueo en `1800` milisegundos.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. Establecer el tiempo de espera de bloqueo para esperar indefinidamente se libere un bloqueo.  
 En el ejemplo siguiente se establece el tiempo de espera de bloqueo para esperar indefinidamente y no expire nunca. Este es el comportamiento predeterminado que ya está establecido al principio de cada conexión.  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 En el ejemplo siguiente se establece el período de tiempo de espera de bloqueo en `1800` milisegundos. En esta versión, [!INCLUDE[ssDW](../../includes/ssdw-md.md)] analizar la instrucción correctamente, pero se omitirá el valor 1800 y seguir usando el comportamiento predeterminado.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>Vea también  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


