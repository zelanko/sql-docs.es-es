---
title: Sys.sp_flush_log (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs: TSQL
helpviewer_keywords: sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36bc92271f4c4125c2f9d6d1b3bff014071cefff
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Vuelca en el disco el registro de transacciones de la base de datos actual, de forma que protege todas las transacciones durables diferidas que se hayan confirmado previamente.  
  
 Si elige utilizar la durabilidad diferida por sus ventajas en el rendimiento, pero también desea tener un límite garantizado de la cantidad de datos que se pueden perder en el bloqueo o conmutación por error de un servidor, ejecute `sys.sp_flush_log` periódicamente. Por ejemplo, si quiere asegurarse de no perder más de x segundos en datos, debe ejecutar `sp_flush_log` cada x segundos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 Si se ejecuta `sys.sp_flush_log`, se garantiza que todas las transacciones durables diferidas que se hayan confirmado previamente se convierten en durables. Vea el tema conceptual [controlar la durabilidad de transacciones](../../relational-databases/logs/control-transaction-durability.md) para obtener más información.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parámetros  
 Ninguno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Un código de retorno con valor 1 indica un procedimiento correcto.  Cualquier otro valor indica error.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="sample-code"></a>Código de ejemplo  
  
```tsql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  
