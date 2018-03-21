---
title: Ver un seguimiento guardado (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9567b1d72e7f857b770738732217277c63488be0
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2018
---
# <a name="view-a-saved-trace-transact-sql"></a>Ver un seguimiento guardado (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo utilizar las funciones integradas para ver un seguimiento guardado.  
  
### <a name="to-view-a-specific-trace"></a>Para ver un seguimiento específico  
  
1.  Ejecute **fn_trace_getinfo** especificando el identificador del seguimiento del que se precisa información. Esta función devuelve una tabla con el seguimiento, la propiedad del seguimiento e información acerca de la propiedad.  
  
     Llame a la función de esta manera:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>Para ver todas los seguimientos existentes  
  
1.  Ejecute **fn_trace_getinfo** especificando `0` o `default`. Esta función devuelve una tabla con todos los seguimiento, sus propiedades e información acerca de estas propiedades.  
  
     Invoque la función de la siguiente manera:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework  
 Para ejecutar la función integrada **fn_trace_getinfo**, el usuario necesita el siguiente permiso:  
  
 ALTER TRACE en el servidor.  
  
## <a name="see-also"></a>Ver también  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [Ver y analizar seguimientos con SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
