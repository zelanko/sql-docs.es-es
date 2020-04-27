---
title: Conéctese a cualquier componente de SQL Server desde SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SQL Server Management Studio
- saving connections
- components [SQL Server], connections
- SQL Server Management Studio [SQL Server], connections
ms.assetid: 5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 342624645e9bd88d0a7afd08b3c18225fc2c14ce
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245374"
---
# <a name="connect-to-any-sql-server-component-from-sql-server-management-studio"></a>Conectar a un componente de SQL Server desde SQL Server Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona funcionalidad para administrar todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Utilice [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para conectarse a:  
  
-   Una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Aunque [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] permite trabajar con consultas sin necesidad de establecer primero una conexión a un origen de datos, la mayoría de las demás tareas necesitan una conexión. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] proporciona el cuadro de diálogo **Conectar al servidor** para configurar las propiedades de conexión a los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se inicia [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , aparece el cuadro de diálogo **Conectar al servidor** , que le pide que se conecte a un servidor. El cuadro de diálogo **Conectar al servidor** conserva la configuración de conexión de la última vez que se utilizó.  
  
> [!NOTE]  
>  Es posible desactivar esta característica con el fin de que no se inicie ninguna conexión automáticamente. Para más información, consulte [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="saving-connections"></a>guardar conexiones  
 Puede guardar las conexiones a servidores concretos en Servidores registrados o en proyectos del Explorador de soluciones.  
  
### <a name="saving-connections-in-registered-servers"></a>Guardar las conexiones en Servidores registrados  
 Al registrar un servidor, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] guarda la información de conexión en Servidores registrados. Para conectarse a un servidor registrado, haga doble clic en su nombre en Servidores registrados. A continuación, el Explorador de objetos iniciará una conexión al servidor.  
  
### <a name="saving-connections-in-solution-explorer"></a>Guardar las conexiones en el Explorador de soluciones  
 El Explorador de soluciones permite almacenar consultas, scripts, conexiones y otra información asociada en un proyecto. Cada proyecto de script contiene un nodo denominado **Conexiones**en el que es posible guardar una o más conexiones. Para agregar una conexión, haga clic con el botón derecho en **Conexiones**y, a continuación, haga clic en **Nueva conexión**. Para obtener acceso a una conexión guardada, expanda **Conexiones** y haga doble clic en la conexión. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abre una ventana de consulta asociada a esa conexión. Una vez guardados, los scripts conservan la asociación a una conexión concreta.  
  
## <a name="see-also"></a>Consulte también  
 [Usar SQL Server Management Studio](../sql-server-management-studio-ssms.md)   
 [Explorador de objetos](../object/object-explorer.md)  
  
  
