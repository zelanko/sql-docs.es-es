---
description: DBCC TRACEOFF (Transact-SQL)
title: DBCC TRACEOFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRACEOFF_TSQL
- TRACEOFF
- DBCC TRACEOFF
- DBCC_TRACEOFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- trace flags [SQL Server], disabling
- DBCC TRACEOFF statement
- disabling trace flags
ms.assetid: 1379afba-6480-454b-9c65-5e64cb4f3415
author: pmasl
ms.author: umajay
ms.openlocfilehash: 1b6990452c110cb012e206389a679688d2ff961d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479807"
---
# <a name="dbcc-traceoff-transact-sql"></a>DBCC TRACEOFF (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

Deshabilita las marcas de seguimiento especificados.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
DBCC TRACEOFF ( trace# [ ,...n ] [ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*trace#*  
Es el número de la marca de seguimiento que se va a deshabilitar.  
  
**-1**  
Deshabilita las marcas de seguimiento de forma global.  
  
WITH NO_INFOMSGS  
Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="remarks"></a>Observaciones  
Las marcas de seguimiento se usan para personalizar algunas características que controlan el funcionamiento de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC TRACEOFF devuelve:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permisos  
Requiere la pertenencia al rol fijo de servidor **sysadmin** .
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se deshabilita la marca de seguimiento `3205`.
  
```sql
DBCC TRACEOFF (3205);   
GO  
```  
  
En el siguiente ejemplo se deshabilita primero la marca de seguimiento `3205` de forma global.
  
```sql
DBCC TRACEOFF (3205, -1);   
GO  
```  
  
En el siguiente ejemplo se deshabilitan las marcas de seguimiento `3205` y `260` de forma global.
  
```sql
DBCC TRACEOFF (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
