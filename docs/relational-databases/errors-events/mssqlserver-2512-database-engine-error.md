---
title: MSSQLSERVER_2512 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2512 (Database Engine error)
ms.assetid: 989b527f-5b02-403c-9b7f-51580f4e7688
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bff6abf4bf03604e63a0f1e300b0d0f50983ebb0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2512"></a>MSSQLSERVER_2512
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2512|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_DUPLICATE_KEYS|  
|Texto del mensaje|Error de tabla: Id. de objeto O_ID, Id. de índice I_ID, Id. de partición PN_ID, Id. de unidad de asignación ID A_ID (tipo TYPE). Hay claves duplicadas en la página P_ID1, zona SLOT1 y en la página P_ID2, zona SLOT2.|  
  
## <a name="explanation"></a>Explicación  
Los dos intervalos especificados tienen claves idénticas, incluido cualquier elemento **uniqueifier**.  
  
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
  
### <a name="results-of-running-repair-options"></a>Resultados de ejecutar opciones REPAIR  
Si uno de los registros es un fantasma o el índice no es único, DBCC puede reparar este problema volviendo a generar el índice. De lo contrario, si es necesario, REPAIR eliminará el intervalo *SLOT2* de la página *P_ID2* o marcará la zona como fantasma.  
  
