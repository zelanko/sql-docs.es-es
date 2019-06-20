---
title: Ver la información del filtro (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abeeac1dc2c6d06a0b1ce89f4dff35415f7189fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63285622"
---
# <a name="view-filter-information-transact-sql"></a>Ver la información del filtro (Transact-SQL)
  En este tema se describe cómo utilizar las funciones integradas para ver la información del filtro de seguimiento.  
  
### <a name="to-view-filter-information"></a>Para ver la información del filtro  
  
1.  Ejecute **fn_trace_getfilterinfo** especificando el identificador del seguimiento del que se precisa información de filtro. Esta función devuelve una tabla con los filtros, las columnas a las que se aplican los filtros y los valores a los que se aplica el filtro.  
  
     Llame a la función de esta manera:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getfilterinfo(trace_id)  
    ```  
  
## <a name="see-also"></a>Vea también  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
