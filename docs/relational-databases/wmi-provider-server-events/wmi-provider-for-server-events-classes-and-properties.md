---
title: Proveedor WMI de clases y propiedades de eventos de servidor
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 000aafb6c7fa7d0c78c0fa5a5596727b8736caad
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888155"
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>Proveedor WMI de clases y propiedades de eventos de servidor
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Los eventos de servidor siguientes componen el modelo de programación del proveedor WMI de eventos de servidor. Hay dos categorías principales de eventos que se pueden consultar emitiendo las consultas WQL contra el proveedor. Son eventos del lenguaje de definición de datos (DDL) y eventos de seguimiento. También se puede consultar los eventos de Service Broker BROKER_QUEUE_DISABLED y QUEUE_ACTIVATION. Tenga en cuenta la naturaleza inclusiva de los diagramas del árbol siguientes. El evento DDL_ASSEMBLY_EVENTS, por ejemplo, incluye los eventos ALTER_ASSEMBLY, DROP_ASSEMBLY y CREATE_ASSEMBLY. De igual forma, el evento TRC_FULL_TEXT incluye los eventos FT_CRAWL_ABORTED, FT_CRAWL_STOPPED y FT_CRAWL_STARTED. ALL_EVENTS cubre todos los eventos DDL, eventos de seguimiento, QUEUE_ACTIVATION y BROKER_QUEUE_DISABLED.  
  
 Para saber qué propiedades se puede consultar desde un evento o grupo de eventos, consulte el esquema de eventos. De forma predeterminada, el esquema de eventos se instala en el directorio siguiente: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd.  
  
 Como alternativa, puede hacer referencia al esquema de eventos publicado en [https://schemas.microsoft.com/sqlserver](https://go.microsoft.com/fwlink/?linkid=43100) .  
  
 Por ejemplo, al hacer referencia al evento ALTER_DATABASE, aprenderá que su evento primario se DDL_SERVER_LEVEL_EVENTS y que sus propiedades son **TSQLCommand** y **DatabaseName**. El evento también hereda las propiedades **SQLInstance**, **posttime**, **ComputerName**, **SPID**y **LoginName**. El evento no tiene ningún evento secundario.  
  
> [!NOTE]  
>  Los procedimientos almacenados del sistema que realizan operaciones similares a DDL también pueden activar notificaciones de eventos. Pruebe las notificaciones de eventos para determinar su respuesta a los procedimientos almacenados del sistema que se ejecutan. Por ejemplo, la instrucción CREATE TYPE y **sp_addtype** procedimiento almacenado activarán una notificación de eventos que se crea en un evento de CREATE_TYPE. Para obtener más información, vea [eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 **Eventos y grupos de eventos del Lenguaje de definición de datos**  
  
 ![Árbol de eventos del proveedor WMI de eventos de servidor](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "Árbol de eventos del proveedor WMI de eventos de servidor")  
  
 **Eventos y grupos de eventos de seguimiento**  
  
 ![Eventos y grupos de eventos de seguimiento](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "Eventos y grupos de eventos de seguimiento")  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos del proveedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [Usar WQL con el proveedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
