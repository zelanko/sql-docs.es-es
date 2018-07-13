---
title: MSSQLSERVER_9002 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 470dc989a6f3bbe7009069eeeb2b99aec96cce92
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429504"
---
# <a name="mssqlserver9002"></a>MSSQLSERVER_9002
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9002|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_IS_FULL|  
|Texto del mensaje|El registro de transacciones de la base de datos '%.*ls' está lleno. Para saber por qué no se puede volver a utilizar el espacio del registro, vea la columna log_reuse_wait_desc de sys.databases.|  
  
## <a name="explanation"></a>Explicación  
 El registro de la base de datos se ha quedado sin espacio. En la columna **log_reuse_wait_desc** de **sys.databases** se describe por qué no se puede volver a utilizar el espacio del registro.  
  
## <a name="user-action"></a>Acción del usuario  
 Use **sys.databases** para determinar la razón por la que el registro está lleno y solucione el problema. Para obtener más información, vea "Solucionar problemas de un registro de transacciones lleno (Error 9002)" en los Libros en pantalla de SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Solucionar problemas de un registro de transacciones lleno &#40;Error 9002 de SQL Server&#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
