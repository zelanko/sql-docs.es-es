---
title: Ver un seguimiento guardado (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 706c100a68a2b077a000e88d6cf093efbddb0ede
ms.sourcegitcommit: ddb682c0061c2a040970ea88c051859330b8ac00
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51570664"
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
  
  
