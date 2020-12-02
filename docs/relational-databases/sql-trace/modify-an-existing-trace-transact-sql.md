---
description: Modificar un seguimiento existente (Transact-SQL)
title: Modificación de un seguimiento existente (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], modifying
- modifying traces
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d6f706093032867835830d0cf98afb86c07e93f7
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "88455377"
---
# <a name="modify-an-existing-trace-transact-sql"></a>Modificar un seguimiento existente (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe cómo utilizar procedimientos almacenados para modificar un seguimiento existente.  
  
### <a name="to-modify-an-existing-trace"></a>Para modificar un seguimiento existente  
  
1.  Si el seguimiento ya se está ejecutando, ejecute **sp_trace_setstatus** especificando **@status = 0** para detener el seguimiento.  
  
2.  Para modificar los eventos del seguimiento, ejecute **sp_trace_setevent** , especificando los cambios a través de los parámetros. Los parámetros son, por este orden:  

    -   **\@traceid** (identificador de seguimiento)  
  
    -   **\@eventid** (identificador del evento)  
  
    -   **\@columnid** (identificador de columna)  
  
    -   **\@on** (activado)  
  
     Al modificar el parámetro **\@on**, tenga presente su interacción con el parámetro **\@columnid**:  
  
    |ACTIVAR|Identificador de columna|Resultado|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|El evento se activa, se establece en ON. Se borran todas las columnas.|  
    ||NOT NULL|La columna se activa, se establece en ON, para el evento especificado.|  
    |OFF (**0**)|NULL|El evento se desactiva, se establece en OFF. Se borran todas las columnas.|  
    ||NOT NULL|La columna se desactiva, se establece en OFF, para el evento especificado.|  
  
> [!IMPORTANT]
>  A diferencia de los procedimientos almacenados normales, los parámetros de todos los procedimientos almacenados de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (<strong>sp_trace_ *xx*</strong>) tienen establecimiento inflexible de tipos y no admiten la conversión automática de tipos de datos. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devuelve un error.  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
