---
title: Motor de SQL Server Extended Events | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], engine
ms.assetid: d74642a5-42b9-4a15-aa3d-f98bfe695050
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee2464f2900eab70546a1074fb2ff07d48cab871
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131105"
---
# <a name="sql-server-extended-events-engine"></a>Motor de SQL Server Extended Events
  El motor de Extended Events [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una colección de servicios y objetos que:  
  
-   Habilita la definición de eventos.  
  
-   Habilita el procesamiento de los datos de eventos.  
  
-   Administra los objetos y servicios de Extended Events en el sistema.  
  
-   Mantiene una lista de las sesiones de Extended Events y administra el acceso a dicha lista.  
  
 El motor de Extended Events no proporciona eventos o acciones que se van a llevar a cabo cuando se activa un evento. Los procesos que utiliza el motor de Extended Events definen la interacción con el motor. Estos procesos agregan los puntos de evento y proporcionan las acciones que se van a llevar a cabo en respuesta a la activación de eventos.  
  
 La ilustración siguiente muestra una vista simplificada de una sesión de Extended Events. Para más información, consulte [SQL Server Extended Events Sessions](sql-server-extended-events-sessions.md).  
  
 ![Arquitectura de eventos extendidos detallada](../../database-engine/media/xearchitecturedetailed.gif "Arquitectura de eventos extendidos detallada")  
  
 Observe lo siguiente:  
  
-   Cada proceso de Windows puede tener uno o más módulos (**proceso Win32**, **módulo Win32**). También se les conoce como módulos *binarios* o *ejecutables*.  
  
-   Cada uno de los módulos de los procesos de Windows puede contener uno o varios paquetes de eventos extendidos (**Paquete**), que contienen uno o más objetos de eventos extendidos (**Tipo**, **Destino**, **Acción**, **Asignación**, **Predicado**y **Evento**).  
  
-   Dentro de un proceso de host solo puede haber una instancia del motor de eventos extendidos (**motor de eventos extendidos**) que:  
  
    -   Administra algunos aspectos de la sesión (por ejemplo, enumerar las sesiones).  
  
    -   Administra el envío (**Distribuidor**). Es similar a un grupo de subprocesos.  
  
    -   Administra los búferes de la memoria (**Búfer**) para los eventos. Cuando se llenan los búferes, los búferes se envían a los destinos.  
  
-   Una vez que se crea una sesión y, opcionalmente, los eventos se enlazan a la sesión (**Contexto de la sesión**):  
  
    -   Las instancias de los destinos (**Instancia de destino**) también pueden crearse y agregarse a la sesión.  
  
    -   Cuando se llenan los búferes, dichos búferes se envían a los destinos.  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](extended-events.md)  
  
  
