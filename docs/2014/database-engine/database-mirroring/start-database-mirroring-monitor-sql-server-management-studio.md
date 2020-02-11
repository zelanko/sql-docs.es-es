---
title: Iniciar el Monitor de creación de reflejo de la base de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 7a48c6620d4395cd44aac6f43cd1817cfebf785e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62754897"
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>Iniciar el Monitor de creación de reflejo de la base de datos (SQL Server Management Studio)
  El Monitor de creación de reflejo de la base de datos forma parte del Monitor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que se inicia desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  El Monitor de creación de reflejo de la base de datos no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>Para iniciar el Monitor de creación de reflejo de la base de datos  
  
1.  Después de conectarse a la instancia del servidor principal, en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol del servidor.  
  
2.  Expanda **Bases de datos**y seleccione la base de datos que desee supervisar.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, luego, haga clic en **Iniciar Monitor de creación de reflejo de la base de datos**.  
  
4.  En el cuadro de diálogo **Monitor de creación de reflejo de la base de datos** , haga clic en **Registrar base de datos reflejada** para registrar una o varias bases de datos reflejadas.  
  
    > [!NOTE]  
    >  Al registrar una base de datos en un asociado, la base de datos se registra automáticamente en el otro asociado. Si el monitor ya dispone de credenciales de conexión para la otra instancia de asociado, se utilizan para conectarse. De lo contrario, el monitor intenta conectarse mediante Autenticación de Windows. Si desea cambiar las credenciales utilizadas para conectarse a una de las instancias del servidor, haga clic en **Mostrar el cuadro de diálogo para administrar conexiones de instancia del servidor cuando haga clic en Aceptar**.  
  
 Para obtener más información sobre el Monitor de creación de reflejo de la base de datos, vea [Información general del Monitor de creación de reflejo de la base de datos](database-mirroring-monitor-overview.md).  
  
## <a name="see-also"></a>Consulte también  
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
  
