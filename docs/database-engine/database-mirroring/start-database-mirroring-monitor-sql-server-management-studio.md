---
title: Iniciar el Monitor de creación de reflejo de la base de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- Database Mirroring Monitor [SQL Server], starting
- database mirroring [SQL Server], monitoring
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 647ec47952f11f926c95a1f84ededdd0ad9fad75
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836959"
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>Iniciar el Monitor de creación de reflejo de la base de datos (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Monitor de creación de reflejo de la base de datos forma parte del Monitor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que se inicia desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  El Monitor de creación de reflejo de la base de datos no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>Para iniciar el Monitor de creación de reflejo de la base de datos  
  
1.  Después de conectarse a la instancia del servidor principal, en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol del servidor.  
  
2.  Expanda **Bases de datos**y seleccione la base de datos que desee supervisar.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, luego, haga clic en **Iniciar Monitor de creación de reflejo de la base de datos**.  
  
4.  En el cuadro de diálogo **Monitor de creación de reflejo de la base de datos** , haga clic en **Registrar base de datos reflejada** para registrar una o varias bases de datos reflejadas.  
  
    > [!NOTE]  
    >  Al registrar una base de datos en un asociado, la base de datos se registra automáticamente en el otro asociado. Si el monitor ya dispone de credenciales de conexión para la otra instancia de asociado, se utilizan para conectarse. De lo contrario, el monitor intenta conectarse mediante Autenticación de Windows. Si desea cambiar las credenciales utilizadas para conectarse a una de las instancias del servidor, haga clic en **Mostrar el cuadro de diálogo para administrar conexiones de instancia del servidor cuando haga clic en Aceptar**.  
  
 Para obtener más información sobre el Monitor de creación de reflejo de la base de datos, vea [Información general del Monitor de creación de reflejo de la base de datos](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md).  
  
## <a name="see-also"></a>Ver también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
  
