---
title: Supervisión del uso de la CPU | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], CPU usage
- tuning databases [SQL Server], CPU usage
- processors [SQL Server], monitoring usage
- database performance [SQL Server], CPU usage
- monitoring CPU usage [SQL Server]
- server performance [SQL Server], CPU usage
- database monitoring [SQL Server], CPU usage
- monitoring [SQL Server], CPU usage
- processors [SQL Server]
- CPU [SQL Server], monitoring
- monitoring server performance [SQL Server], CPU usage
ms.assetid: 2a02a3b6-07b2-4ad0-8a24-670414d19812
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e46610823432efde0cc757e3dff317227b7548ac
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747707"
---
# <a name="monitor-cpu-usage"></a>Supervisar el uso de la CPU
  Supervise una instancia de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] periódicamente para determinar si los índices de uso de la CPU son normales. Un índice de uso de la CPU constantemente alto puede indicar la necesidad de actualizar la CPU o de agregar varios procesadores. Además, un uso alto de la CPU puede indicar que hay una aplicación mal optimizada o diseñada. La optimización de la aplicación puede reducir el uso de la CPU.  
  
 El contador **Procesador: % de tiempo de procesador** en el Monitor de sistema es la forma más eficaz de determinar el uso de la CPU. Este contador supervisa el tiempo que la CPU dedica a la ejecución de un subproceso que no está inactivo. Un estado continuado de entre el 80 y el 90 por ciento puede ser indicativo de que es necesario actualizar la CPU o bien agregar más procesadores. Para sistemas con múltiples procesadores, es necesario supervisar una instancia independiente de este contador para cada procesador. Este valor representa la suma del tiempo de procesador en un procesador específico. Para determinar la media para todos los procesadores de impresión, utilice el contador **Sistema: % Tiempo total de procesador** en su lugar.  
  
 Para supervisar el uso del procesador también puede utilizar los siguientes contadores:  
  
-   **Procesador: % Tiempo privilegiado**  
  
     Porcentaje de tiempo de procesador dedicado a la ejecución de comandos del kernel de Microsoft Windows, como el procesamiento de solicitudes de E/S de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si este contador es constantemente alto cuando los contadores **Disco físico** son altos, considere la posibilidad de instalar un subsistema de disco más rápido o eficaz.  
  
    > [!NOTE]  
    >  Los diversos controladores de disco emplean distintos intervalos de tiempo de proceso del kernel. Los controladores eficaces utilizan menos tiempo privilegiado y dejan más tiempo de proceso disponible para aplicaciones del usuario, y aumentan así el rendimiento global.  
  
-   **Procesador: % Tiempo de usuario**  
  
     Porcentaje de tiempo que el procesador dedica a la ejecución de procesos de usuario, como por ejemplo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Sistema: Longitud de cola del procesador**  
  
     Número de subprocesos en espera del tiempo del procesador. Se produce un punto de congestión en el procesador cuando los subprocesos de un proceso requieren más ciclos de procesador que los disponibles. Si bastantes procesos intentan utilizar el tiempo de procesador, puede que sea necesario instalar un procesador más rápido. Si dispone de una sistema con múltiples procesadores, puede agregar un procesador.  
  
 Cuando examine el uso de los procesadores, tenga en cuenta el tipo de trabajo que realiza la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza muchos cálculos, como consultas relativas a agregados o consultas enlazadas a memoria que no requieren E/S del disco, puede utilizarse el 100% del tiempo del procesador. Si esto afecta negativamente al rendimiento de otras aplicaciones, pruebe a variar la carga de trabajo. Por ejemplo, dedique el equipo a ejecutar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los valores de uso en torno al 100%, que indican que se están procesando muchas solicitudes de clientes, pueden mostrar que los procesos están en cola, en espera del tiempo del procesador y están causando un punto de congestión. Para solucionar este problema, agregue procesadores de mayor velocidad.  
  
  
