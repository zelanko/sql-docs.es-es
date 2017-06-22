---
title: Error del motor de base de datos MSSQLSERVER_802 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 802 (Database Engine error)
ms.assetid: 5892ed24-4dcb-4bf9-a8a4-a7ca898832d5
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83a4a02b0977f3a1b9feec0ad720aef6728cb906
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver802---database-engine-error"></a>Error del motor de base de datos MSSQLSERVER_802
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|802|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NO_BUFS|  
|Texto del mensaje|No hay suficiente memoria disponible en el grupo de búferes.|  
  
## <a name="explanation"></a>Explicación  
Esto se debe a que el grupo de búferes está lleno y no puede crecer más.  
  
## <a name="user-action"></a>Acción del usuario  
En la siguiente lista se describen los pasos generales que ayudarán a resolver los errores de memoria:  
  
1.  Compruebe si otras aplicaciones o servicios están consumiendo memoria en este servidor. Vuelva a configurar las aplicaciones o servicios menos críticos para que consuman menos memoria.  
  
2.  Empiece a recopilar los contadores del monitor de rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Buffer Manager**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Memory Manager**.  
  
3.  Compruebe los siguientes parámetros de configuración de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   **memoria de servidor máxima**  
  
    -   **memoria de servidor mínima**  
  
    -   **memoria mínima por consulta**  
  
    Observe si hay algún valor fuera de lo normal y corríjalo según sea necesario. Investigue el porqué de los mayores requisitos de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se hace una lista de la configuración predeterminada en "Establecer las opciones de configuración del servidor" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Observe la salida de DBCC MEMORYSTATUS y la forma en que cambia cuando aparecen estos mensajes de error.  
  
5.  Compruebe la carga de trabajo (el número de sesiones simultáneas y las consultas que se están ejecutando actualmente).  
  
Las siguientes acciones pueden hacer que haya más memoria disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Si otras aplicaciones además de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están consumiendo recursos, intente detenerlas o ejecutarlas en otro servidor.  
  
-   Si ha configurado **max server memory**, aumente su valor.  
  
Ejecute los siguientes comandos DBCC para liberar varias cachés de la memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
Si el problema persiste, necesitará investigar más y, posiblemente, reducir la carga de trabajo.  
  

