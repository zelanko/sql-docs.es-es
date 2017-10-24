---
title: '@@TOTAL_READ (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TOTAL_READ_TSQL'
- '@@TOTAL_READ'
dev_langs:
- TSQL
helpviewer_keywords:
- number of disk reads
- disks [SQL Server], number of disk reads
- '@@TOTAL_READ function'
- total read [SQL Server]
- read activity since last started
ms.assetid: b505fbe9-9569-4f3d-80b9-b64b5109ac98
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 7b4fa5a60334267f1c91674fecef44fe10c2b202
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40totalread-transact-sql"></a>& #x 40; & #x 40; TOTAL_READ (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de lecturas de disco (no de caché) realizadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
@@TOTAL_READ  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **integer**  
  
## <a name="remarks"></a>Comentarios  
 Para mostrar un informe que contenga varias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estadísticas, incluidos los de lectura y escritura de actividad, ejecutan **sp_monitor**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo devolver el número total de disco lee y escribe a partir de la fecha y hora actuales.  
  
```  
SELECT @@TOTAL_READ AS 'Reads', @@TOTAL_WRITE AS 'Writes', GETDATE() AS 'As of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Reads       Writes      As of                   
----------- ----------- ----------------------  
7760        97263       12/5/2006 10:23:00 PM   
```  
  
## <a name="see-also"></a>Vea también  
 [sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funciones estadísticas del sistema &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)   
 [@@TOTAL_WRITE &#40;Transact-SQL&#41;](../../t-sql/functions/total-write-transact-sql.md)  
  
  

