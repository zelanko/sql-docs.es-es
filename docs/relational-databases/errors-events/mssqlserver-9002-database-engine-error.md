---
title: MSSQLSERVER_9002 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 757dabfc59775ac407dd5d1ceece2d067d32eacd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761603"
---
# <a name="mssqlserver9002"></a>MSSQLSERVER_9002
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Ver también  
[Solucionar problemas de un registro de transacciones lleno &#40;Error 9002 de SQL Server&#41;](~/relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
