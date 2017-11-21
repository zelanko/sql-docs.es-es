---
title: MSSQLSERVER_701 | Microsoft Docs
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
- 701 (Database Engine error)
ms.assetid: 3b975000-63a1-43c2-a40f-89d0a8a36bef
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0923e3d8078d720775ecbb8a321348e9b3bf4d89
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver701"></a>MSSQLSERVER_701
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|701|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NOSYSMEM|  
|Texto del mensaje|Memoria de sistema insuficiente para ejecutar esta consulta.|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha podido asignar suficiente memoria para ejecutar la consulta. Esto puede deberse a diversos motivos, incluidos la configuración del sistema operativo, la disponibilidad de memoria física o los límites de memoria de la carga de trabajo actual. En la mayoría de los casos, la transacción errónea no es la causa de este error.  
  
Las consultas de diagnóstico, como las instrucciones DBCC, pueden generar un error porque el servidor no tiene suficiente memoria.  
  
Se agotó el tiempo de espera mientras los recursos de memoria ejecutaban la consulta en el grupo de recursos 'predeterminado'.  
  
## <a name="user-action"></a>Acción del usuario  
Si no utiliza el regulador de recursos, le recomendamos que compruebe el estado y la carga generales del servidor, o la configuración del grupo de recursos o del grupo de carga de trabajo.  
  
En la siguiente lista se describen los pasos generales que ayudarán a resolver los errores de memoria:  
  
1.  Compruebe si otras aplicaciones o servicios están consumiendo memoria en este servidor. Vuelva a configurar las aplicaciones o servicios menos críticos para que consuman menos memoria.  
  
2.  Empiece a recopilar los contadores del monitor de rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Buffer Manager**, **SQL Server: Memory Manager**.  
  
3.  Compruebe los siguientes parámetros de configuración de memoria de SQL Server:  
  
    -   **memoria de servidor máxima**  
  
    -   **memoria de servidor mínima**  
  
    -   **memoria mínima por consulta**  
  
    Observe si hay algún valor fuera de lo normal. Corríjalos según sea necesario. Investigue el porqué de los mayores requisitos de memoria. La configuración predeterminada se enumera en "Establecer las opciones de configuración del servidor" en los Libros en pantalla de SQL Server.  
  
4.  Observe la salida de DBCC MEMORYSTATUS y la forma en que cambia cuando aparecen estos mensajes de error.  
  
5.  Compruebe la carga de trabajo (por ejemplo, el número de sesiones simultáneas y las consultas que se están ejecutando actualmente).  
  
Las siguientes acciones pueden hacer que haya más memoria disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Si otras aplicaciones además de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están consumiendo recursos, intente detener su ejecución o plantéese ejecutarlas en otro servidor. Esto quitará presión externa de la memoria.  
  
-   Si ha configurado **max server memory**, aumente su valor.  
  
Ejecute los siguientes comandos DBCC para liberar varias cachés de la memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
Si el problema persiste, necesitará investigar más y, posiblemente, reducir la carga de trabajo.  
  

