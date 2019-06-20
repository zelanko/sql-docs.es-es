---
title: MSSQL_ENG004929 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG004929 error
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 526c5b0bb1b7c5dd0d7cf1485f7e399b6f1fbff9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666980"
---
# <a name="mssqleng004929"></a>MSSQL_ENG004929
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|4929|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se puede modificar el % S_MSG ' %. * ls' porque se está publicando para replicación.|  
  
## <a name="explanation"></a>Explicación  
 Normalmente este error se produce si intenta quitar la restricción de clave principal en una tabla que está publicada para replicación transaccional. La replicación transaccional requiere una clave principal para cada tabla publicada; por tanto, no se puede quitar la restricción.  
  
## <a name="user-action"></a>Acción del usuario  
 Para quitar la restricción, primero quite el artículo asociado con la tabla. Para obtener más información, vea [Agregar y quitar artículos de publicaciones existentes](publish/add-articles-to-and-drop-articles-from-existing-publications.md). Si se produce este error en una base de datos que no está replicada, ejecute [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) para asegurarse de que los objetos de la base de datos no están marcados como replicados.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
