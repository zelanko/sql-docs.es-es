---
title: MSSQLSERVER_2575 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2575 (Database Engine error)
ms.assetid: 92dfe449-a122-4730-942b-e1d319862d20
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 540cf73d796153bfb3f09f4fdf3b6e9daaad335a
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2575"></a>MSSQLSERVER_2575
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2575|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_IAM_PAGE_WAS_NOT_SEEN|  
|Texto del mensaje|El siguiente puntero de la página IAM (Mapa de asignación de índices) P_ID2 [Id. de objeto O_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación A_ID (tipo TYPE)] apunta a la página IAM P_ID1, pero no se detectó en el recorrido.|  
  
## <a name="explanation"></a>Explicación  
Se encontró una página IAM (Mapa de asignación de índices) para el índice especificado; sin embargo, no se encontró la página IAM para el puntero de página siguiente.  
  
## <a name="user-action"></a>Acción del usuario  
  
### <a name="look-for-hardware-failure"></a>Busque un error de hardware  
Ejecute un diagnóstico de hardware y corrija cualquier problema. Examine también los registros del sistema y de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows así como el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver si el error se produjo como resultado de un error de hardware. Arregle cualquier problema relacionado con el hardware que encuentre en estos registros.  
  
Si sigue teniendo problemas de datos dañados, intente intercambiar diferentes componentes de hardware para aislar el problema. Asegúrese de que el sistema no tiene habilitada la memoria caché de escritura en el controlador de disco. Si cree que el problema se debe a la caché de escritura, póngase en contacto con su proveedor de hardware.  
  
Finalmente, puede resultarle útil cambiar a un nuevo sistema de hardware. Este cambio puede incluir volver a formatear las unidades de disco y volver a instalar el sistema operativo.  
  
### <a name="restore-from-backup"></a>Restaure mediante la copia de seguridad  
Si el problema no está relacionado con el hardware y tiene una copia de seguridad limpia disponible, úsela para restaurar la base de datos.  
  
### <a name="run-dbcc-checkdb"></a>Ejecute DBCC CHECKDB  
Si no tiene disponible una copia de seguridad limpia, ejecute DBCC CHECKDB sin una cláusula REPAIR para determinar el alcance de los daños. DBCC CHECKDB recomendará el uso de una cláusula REPAIR. A continuación, ejecute DBCC CHECKDB con la cláusula REPAIR apropiada para reparar el problema.  
  
> [!CAUTION]  
> Si no está seguro del efecto que tendrá DBCC CHECKDB con una cláusula REPAIR en los datos, póngase en contacto con su proveedor principal de soporte antes de ejecutar esta instrucción.  
  
Si ejecuta DBCC CHECKDB con una de las cláusulas REPAIR y no se soluciona el problema, póngase en contacto con su proveedor principal de soporte.  
  
#### <a name="results-of-running-repair-options"></a>Resultados de ejecutar opciones REPAIR  
DBCC volverá a generar el índice.  
  
## <a name="see-also"></a>Vea también  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  

