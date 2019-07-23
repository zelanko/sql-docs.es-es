---
title: MSSQLSERVER_8651 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8651 (Database Engine error)
ms.assetid: 4cc3498d-5449-4c4e-b1f9-3271831c725a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9e8341b3212229a29dec9291fd6d5206725b1788
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132269"
---
# <a name="mssqlserver8651"></a>MSSQLSERVER_8651
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8651|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|MEMGRANT_ERR|  
|Texto del mensaje|No se puede realizar la operación solicitada, la memoria de consulta mínima no está disponible. Reduzca el valor de la opción de configuración del servidor 'min memory per query'.|  
  
## <a name="explanation"></a>Explicación  
Otros procesos están consumiendo memoria del servidor (ejerciendo presión en la memoria del servidor).  
  
## <a name="user-action"></a>Acción del usuario  
Reduzca el valor configurado de la opción de configuración del servidor 'min memory per query' o reduzca la carga de consultas del servidor.  
  
En la siguiente lista se describen los pasos generales que ayudarán a resolver los errores de memoria:  
  
1.  Compruebe si otras aplicaciones o servicios están consumiendo memoria en este servidor. Vuelva a configurar las aplicaciones o servicios menos críticos para que consuman menos memoria.  
  
2.  Empiece a recopilar los contadores del monitor de rendimiento para **SQL Server: Administrador de búfer**, **SQL Server: Administrador de memoria**.  
  
3.  Compruebe los siguientes parámetros de configuración de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   **memoria de servidor máxima**  
  
    -   **memoria de servidor mínima**  
  
    -   **memoria mínima por consulta**  
  
    Observe si hay algún valor fuera de lo normal. Corríjalos según sea necesario. La configuración predeterminada se enumera en "Establecer las opciones de configuración del servidor" en los Libros en pantalla de SQL Server.  
  
4.  Compruebe la carga de trabajo (por ejemplo, el número de sesiones simultáneas y las consultas que se están ejecutando actualmente).  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

Las siguientes acciones pueden hacer que haya más memoria disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Si otras aplicaciones además de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están consumiendo recursos, intente detener su ejecución o plantéese ejecutarlas en otro servidor. Esto quitará presión externa de la memoria.  
  
-   Si ha configurado **max server memory**, aumente su valor.  
  
Ejecute los siguientes comandos DBCC para liberar varias cachés de la memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
Si el problema persiste, necesitará investigar más y, posiblemente, reducir la carga de trabajo.  
  
## <a name="see-also"></a>Consulte también  
[DBCC FREESYSTEMCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[Opciones de configuración del servidor &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[Buffer Manager (objeto de SQL Server)](~/relational-databases/performance-monitor/sql-server-buffer-manager-object.md)  
[Memory Manager (objeto de SQL Server)](~/relational-databases/performance-monitor/sql-server-memory-manager-object.md)  
  
