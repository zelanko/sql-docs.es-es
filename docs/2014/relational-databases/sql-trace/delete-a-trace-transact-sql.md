---
title: Eliminación de un seguimiento guardado (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e255ab5d72c8d7d0cfd935ba971b7f1c409ee38a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158006"
---
# <a name="delete-a-trace-transact-sql"></a>Eliminar un seguimiento (Transact-SQL)
  En este tema se describe el modo de utilizar procedimientos almacenados para eliminar un seguimiento.  
  
 Para obtener un ejemplo de cómo usar los procedimientos almacenados de seguimiento, vea [Crear un seguimiento &#40;Transact-SQL&#41;](create-a-trace-transact-sql.md).  
  
### <a name="to-delete-a-trace"></a>Para eliminar un seguimiento  
  
1.  Ejecute **sp_trace_setstatus** con **@status = 0** para detener el seguimiento.  
  
2.  Ejecute **sp_trace_setstatus** con **@status = 2** para cerrar el seguimiento y eliminar su información del servidor.  
  
> [!NOTE]  
>  Para poder cerrar un seguimiento, primero debe detenerse.  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
