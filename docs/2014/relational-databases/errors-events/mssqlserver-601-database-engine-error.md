---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 43c15019df09863af85e57d46b21e0b70ad49c08
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413221"
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
    
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
  
## <a name="see-also"></a>Vea también  
 [MSSQLSERVER_605](mssqlserver-605-database-engine-error.md)   
 [Sugerencias de tabla &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)  
  
  
