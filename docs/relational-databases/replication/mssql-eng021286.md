---
title: MSSQL_ENG021286 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021286 error
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e0db9097b57dcef2fafba41c771251c8042b2f20
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363239"
---
# <a name="mssql_eng021286"></a>MSSQL_ENG021286
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|21286|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La tabla de conflictos '%1!' no existe.|  
  
## <a name="explanation"></a>Explicación  
 Este error se produce si la tabla de conflictos de un artículo mencionado en [sysmergearticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) no existe realmente. El error se puede producir al intentar agregar o quitar una columna de una tabla publicada para la replicación de mezcla.  
  
## <a name="user-action"></a>Acción del usuario  
 Ejecute [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos donde falta la tabla en conflicto para comprobar que no existen problemas de coherencia de datos.  
  
 Si la tabla de conflictos falta en un suscriptor, quite y vuelva a crear la suscripción. Si la tabla de conflictos falta en un publicador, quite todas las suscripciones, quite la publicación y vuelva a crear la publicación y todas las suscripciones. Para obtener más información sobre la creación de publicación, vea [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md) y [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
