---
title: Modificar una sesión de eventos extendidos
description: Use el Asistente para eventos extendidos de SQL Server para modificar una sesión de eventos extendidos. Los cambios que puede realizar dependen de si la sesión está activa o inactiva.
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 26c54a8100f697275e87826e949f8b83276507a5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85778455"
---
# <a name="alter-an-extended-events-session"></a>Modificar una sesión de eventos extendidos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Después de crear una sesión de eventos extendidos, puede modificarla según sus necesidades con el **Asistente para eventos extendidos de SQL Server**.  
  
## <a name="before-you-begin"></a>Introducción  
 No puede modificar un destino para las sesiones activas e inactivas, y no puede cambiar las configuraciones de propiedades avanzadas de una sesión activa.  
  
 Puede realizar las siguientes modificaciones en las sesiones de eventos activas e inactivas:  
  
-   Agregar o quitar eventos de la sesión y modificar las configuraciones de eventos como campos, filtros y acciones de eventos.  
  
-   Agregar o quitar un destino de la sesión de eventos.  
  
-   Habilitar la opción **Iniciar la sesión de eventos al iniciar el servidor** .  
  
 Puede realizar las siguientes modificaciones adicionales en una sesión de eventos inactiva:  
  
-   Habilitar la opción **Realizar el seguimiento de la relación entre eventos** .  
  
-   Cambiar la configuración de las propiedades avanzadas.  
  
> [!NOTE]  
>  El **Asistente para eventos extendidos de SQL Server** no admite la modificación de la sesión de eventos.  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>Cómo modificar una sesión de eventos extendidos con el Asistente para eventos extendidos de SQL Server  
  
-   En el Explorador de objetos, expanda **Administración**, expanda **Eventos extendidos**y, a continuación, expanda **Sesiones**.  
  
-   Haga clic con el botón derecho en la sesión que quiera modificar y luego haga clic en **Propiedades**.  
  
-   En el cuadro de diálogo **Propiedades** , realice los cambios adecuados y, a continuación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Consulte también  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [Crear una sesión de eventos extendidos mediante el Editor de consultas](quick-start-extended-events-in-sql-server.md)  
  
  
