---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06656cdbeabe8e439b2a73bf78f5d90bfc44b8b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025565"
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|601|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|No se pudo continuar el examen con NOLOCK debido al movimiento de los datos.|  
  
## <a name="explanation"></a>Explicación  
El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no puede continuar la ejecución de la consulta porque está intentando leer datos actualizados o eliminados por otra transacción. La consulta está utilizando la sugerencia de bloqueo NOLOCK o el nivel de aislamiento de las transacciones READ UNCOMMITTED.  
  
Normalmente, se deniega el acceso a los datos modificados por otra transacción debido a los bloqueos colocados en los datos. Sin embargo, la sugerencia de bloqueo NOLOCK y el nivel de aislamiento de las transacciones READ UNCOMMITTED permiten que una consulta lea los datos bloqueados por otra transacción. Es lo que se conoce como lectura de datos sucios porque pueden leerse valores que aún no se han confirmado y que están sujetos a cambios.  
  
## <a name="user-action"></a>Acción del usuario  
Este error cancela la consulta. Vuelva a enviar la consulta o quite la sugerencia de bloqueo NOLOCK.  
  
## <a name="see-also"></a>Consulte también  
[MSSQLSERVER_605](../../relational-databases/errors-events/mssqlserver-605-database-engine-error.md)  
[Sugerencias de tabla &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-table.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](~/t-sql/statements/set-transaction-isolation-level-transact-sql.md)  
  
