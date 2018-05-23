---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85a3954b37ca6f3467bf1fc0d4fafda7dadb59ad
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1457|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_PAGE_UNDO_PENDING|  
|Texto del mensaje|Se interrumpió la sincronización de la base de datos reflejada, '%.*ls' y ésta quedó en un estado incoherente. Error del comando ALTER DATABASE. Asegúrese de que hay una copia de seguridad la base de datos reflejada y de que la base de datos está en línea, y vuelva a conectar la instancia del servidor reflejado y permita que la base de datos reflejada finalice la sincronización.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje indica un error en la instrucción ALTER DATABASE *nombreDeBaseDeDatos* SET PARTNER OFF. El error al intentar quitar el reflejo de la base de datos ha interrumpido la sincronización de la base de datos reflejada. La base de datos se encuentra en un estado incoherente.  
  
## <a name="user-action"></a>Acción del usuario  
Para solucionar este error, puede realizar una de las siguientes acciones:  
  
-   Restaure el contacto entre el servidor reflejado y el principal para permitir la sincronización de la base de datos reflejada.  
  
-   Quite la base de datos reflejada.  
  
    Después de quitar la base de datos reflejada, puede crear una nueva base de datos reflejada a partir de las copias de seguridad.  
  
    > [!NOTE]  
    > Puede quitar la base de datos reflejada cuando está todavía habilitada la creación de reflejo solo después de un error de instrucción SET PARTNER OFF.  
  
## <a name="see-also"></a>Ver también  
[Creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[Configurar la creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
[Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
[Preparar una base de datos reflejada para la creación de reflejo &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
