---
title: Modificar una sesión de eventos extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 07f79ea126998f5949d47dd8fb111d32b72841c6
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/26/2019
ms.locfileid: "58478030"
---
# <a name="alter-an-extended-events-session"></a>Modificar una sesión de eventos extendidos

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Después de crear una sesión de eventos extendidos, puede modificarla según sus necesidades con el **Asistente para eventos extendidos de SQL Server**.  
  
## <a name="before-you-begin"></a>Antes de empezar  
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
 [Crear una sesión de eventos extendidos mediante el Editor de consultas](https://msdn.microsoft.com/library/cba0e02b-b201-4863-bf1b-9164e68e5fa8)  
  
  
