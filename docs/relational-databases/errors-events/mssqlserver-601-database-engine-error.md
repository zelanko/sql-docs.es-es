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
ms.openlocfilehash: a1c516a70788d16fc4c80e5ed0b9f0277eccf020
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728347"
---
# <a name="mssqlserver_601"></a>MSSQLSERVER_601
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|601|  
|Origen de eventos|MSSQLSERVER|  
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
  
