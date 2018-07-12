---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d0cf2eed90e1aea1f636322a0a728720222e0935
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423484"
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
    
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
    >  Puede quitar la base de datos reflejada cuando está todavía habilitada la creación de reflejo solo después de un error de instrucción SET PARTNER OFF.  
  
## <a name="see-also"></a>Vea también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Configurar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [Preparar una base de datos reflejada para la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
  
