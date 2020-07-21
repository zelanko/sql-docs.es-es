---
title: Motor de SQL Server Extended Events
description: El motor de eventos extendidos de SQL Server permite la definición de eventos y el procesamiento de datos de eventos, administra eventos extendidos y mantiene una lista de sesiones.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], engine
ms.assetid: d74642a5-42b9-4a15-aa3d-f98bfe695050
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9178b6246c32c54aee6979bec00bac8b53e700fe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756868"
---
# <a name="sql-server-extended-events-engine"></a>Motor de SQL Server Extended Events

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  El motor de Extended Events [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una colección de servicios y objetos que:  
  
-   Habilita la definición de eventos.  
  
-   Habilita el procesamiento de los datos de eventos.  
  
-   Administra los objetos y servicios de Extended Events en el sistema.  
  
-   Mantiene una lista de las sesiones de Extended Events y administra el acceso a dicha lista.  
  
 El motor de Extended Events no proporciona eventos o acciones que se van a llevar a cabo cuando se activa un evento. Los procesos que utiliza el motor de Extended Events definen la interacción con el motor. Estos procesos agregan los puntos de evento y proporcionan las acciones que se van a llevar a cabo en respuesta a la activación de eventos.  
  
 La ilustración siguiente muestra una vista simplificada de una sesión de Extended Events. Para más información, consulte [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md).  
  
 ![Arquitectura de eventos extendidos detallada](../../relational-databases/extended-events/media/xearchitecturedetailed.gif "Arquitectura de eventos extendidos detallada")  
  
 Tenga en cuenta lo siguiente:  
  
-   Cada proceso de Windows puede tener uno o más módulos (**proceso Win32**, **módulo Win32**). También se les conoce como módulos *binarios* o *ejecutables*.  
  
-   Cada uno de los módulos de los procesos de Windows puede contener uno o varios paquetes de eventos extendidos (**Paquete**), que contienen uno o más objetos de eventos extendidos (**Tipo**, **Destino**, **Acción**, **Asignación**, **Predicado**y **Evento**).  
  
-   Dentro de un proceso de host solo puede haber una instancia del motor de eventos extendidos (**motor de eventos extendidos**) que:  
  
    -   Administra algunos aspectos de la sesión (por ejemplo, enumerar las sesiones).  
  
    -   Administra el envío (**Distribuidor**). Es similar a un grupo de subprocesos.  
  
    -   Administra los búferes de la memoria (**Búfer**) para los eventos. Cuando se llenan los búferes, los búferes se envían a los destinos.  
  
-   Una vez que se crea una sesión y, opcionalmente, los eventos se enlazan a la sesión (**Contexto de la sesión**):  
  
    -   Las instancias de los destinos (**Instancia de destino**) también pueden crearse y agregarse a la sesión.  
  
    -   Cuando se llenan los búferes, dichos búferes se envían a los destinos.  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
