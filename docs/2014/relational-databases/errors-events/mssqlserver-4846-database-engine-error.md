---
title: MSSQLSERVER_4846 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e8ba92a3ca62fd32ca36aac72c2de50eadc63b1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423774"
---
# <a name="mssqlserver4846"></a>MSSQLSERVER_4846
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|4846|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|BULKPROV_MEMORY|  
|Texto del mensaje|El proveedor de conjuntos masivos de datos no pudo asignar memoria.|  
  
## <a name="explanation"></a>Explicación  
 Se produjo un error de asignación de memoria.  
  
## <a name="user-action"></a>Acción del usuario  
 Para solucionar errores de memoria, siga estos pasos generales:  
  
1.  Compruebe si otras aplicaciones o servicios están consumiendo memoria en este servidor. Vuelva a configurar las aplicaciones o servicios menos críticos para que consuman menos memoria.  
  
2.  Empiece a recopilar los contadores del monitor de rendimiento para **SQL Server: Buffer Manager**, **SQL Server: Memory Manager**.  
  
3.  Compruebe los siguientes parámetros de configuración de memoria de SQL Server:  
  
    -   **memoria de servidor máxima**  
  
    -   **memoria de servidor mínima**  
  
    -   **memoria mínima por consulta**  
  
     Observe si hay algún valor fuera de lo normal. Corríjalos según sea necesario. Investigue los requisitos de memoria para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. La configuración predeterminada se enumera en "Establecer las opciones de configuración del servidor" en los Libros en pantalla de SQL Server.  
  
4.  Observe la salida de DBCC MEMORYSTATUS y la forma en que cambia cuando aparecen estos mensajes de error.  
  
5.  Compruebe la carga de trabajo (por ejemplo, el número de sesiones simultáneas y las consultas que se están ejecutando actualmente).  
  
 Las siguientes acciones pueden hacer que haya más memoria disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Si otras aplicaciones están consumiendo recursos, intente detener su ejecución o plantéese ejecutarlas en otro servidor. Esto quitará presión externa de la memoria.  
  
-   Si ha configurado **max server memory**, aumente su valor.  
  
 Ejecute los siguientes comandos DBCC para liberar varias cachés de la memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 Si el problema persiste, necesitará investigar más y, posiblemente, reducir la carga de trabajo.  
  
  
