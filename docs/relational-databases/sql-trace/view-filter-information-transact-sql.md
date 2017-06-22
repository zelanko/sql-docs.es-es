---
title: "Ver la información del filtro (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce6c2cf81a054b4dd32fe9a74039a5388c80c5c7
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

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
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
