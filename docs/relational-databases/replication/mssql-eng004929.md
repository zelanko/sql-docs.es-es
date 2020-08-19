---
description: MSSQL_ENG004929
title: MSSQL_ENG004929 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG004929 error
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: be71e42aa8fa2c7495724ffd3e533aa52737b28a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88379481"
---
# <a name="mssql_eng004929"></a>MSSQL_ENG004929
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|4929|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se puede modificar el %1! '%2!' porque se está publicando para replicación.|  
  
## <a name="explanation"></a>Explicación  
 Normalmente este error se produce si intenta quitar la restricción de clave principal en una tabla que está publicada para replicación transaccional. La replicación transaccional requiere una clave principal para cada tabla publicada; por tanto, no se puede quitar la restricción.  
  
## <a name="user-action"></a>Acción del usuario  
 Para quitar la restricción, primero quite el artículo asociado con la tabla. Para más información, vea [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md). Si se produce este error en una base de datos que no está replicada, ejecute [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para asegurarse de que los objetos de la base de datos no están marcados como replicados.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
