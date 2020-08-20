---
description: Eliminar un seguimiento (Transact-SQL)
title: Eliminación de un seguimiento guardado (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d3264c9fe9622bdddee3aecd002193c245c5b457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455385"
---
# <a name="delete-a-trace-transact-sql"></a>Eliminar un seguimiento (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe el modo de utilizar procedimientos almacenados para eliminar un seguimiento.  
  
 Para obtener un ejemplo de cómo usar los procedimientos almacenados de seguimiento, vea [Crear un seguimiento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
### <a name="to-delete-a-trace"></a>Para eliminar un seguimiento  
  
1.  Ejecute **sp_trace_setstatus** y especifique `@status = 0` para detener el seguimiento.  
  
2.  Ejecute **sp_trace_setstatus** y especifique `@status = 2` para cerrar el seguimiento y eliminar su información del servidor.  
  
> [!NOTE]  
>  Para poder cerrar un seguimiento, primero debe detenerse.  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
