---
title: "MSSQL_ENG004929 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG004929"
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG004929
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|4929|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se puede modificar el %1! '%2!' porque se está publicando para replicación.|  
  
## Explicación  
 Normalmente este error se produce si intenta quitar la restricción de clave principal en una tabla que está publicada para replicación transaccional. La replicación transaccional requiere una clave principal para cada tabla publicada; por tanto, no se puede quitar la restricción.  
  
## Acción del usuario  
 Para quitar la restricción, primero quite el artículo asociado con la tabla. Para obtener más información, consulte [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md). Si este error se produce en una base de datos que no se replica, ejecute [sp_removedbreplication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para asegurarse de que los objetos de la base de datos no están marcados como replicados.  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  