---
title: Administrar el servicio de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- services [Integration Services], configuring
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc3b1eb4e73b3d77b49cc9f485e0a6fc456a8875
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057790"
---
# <a name="manage-the-integration-services-service"></a>Administrar el servicio Integration Services
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]admite el servicio para mantener la compatibilidad con versiones anteriores [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]de. A partir de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 Al instalar el componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se instala también el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se inicia y el tipo de inicio del servicio se establece en automático. Sin embargo, también debe instalar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para usar el servicio y administrar los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacenados y en ejecución.  
  
> [!NOTE]  
>  No se puede conectar a una instancia del [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] servicio desde la [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] versión de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Es decir, en el cuadro de diálogo **Conectar con el servidor** , no se puede escribir el nombre de un servidor en el que solamente se está ejecutando [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Sin embargo, puede modificar el archivo de configuración para el servicio y, de ese modo, administrar paquetes almacenados en una instancia de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] desde [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](service/integration-services-service-ssis-service.md).  
  
 Solo puede instalar una única instancia del servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en un equipo. El servicio no es específico de una instancia determinada de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Para realizar la conexión con el servicio se utiliza el nombre del equipo en el que se ejecuta.  
  
 Puede administrar el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mediante uno de los siguientes complementos de Microsoft Management Console (MMC): los servicios o el Administrador de configuración de SQL Server. Antes de que pueda administrar paquetes en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], asegúrese de que se ha iniciado el servicio.  
  
 De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se configura para administrar los paquetes de la base de datos msdb de la instancia del [!INCLUDE[ssDE](../includes/ssde-md.md)] que se instala al mismo tiempo que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Si no se instala al mismo tiempo una instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)], el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se configura para administrar paquetes de la base de datos msdb de la instancia local predeterminada del [!INCLUDE[ssDE](../includes/ssde-md.md)]. Para administrar paquetes que están almacenados en una instancia con nombre o remota de [!INCLUDE[ssDE](../includes/ssde-md.md)], o en varias instancias de [!INCLUDE[ssDE](../includes/ssde-md.md)], tiene que modificar el archivo de configuración para el servicio. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](service/integration-services-service-ssis-service.md).  
  
 De manera predeterminada, el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está configurado para dejar de ejecutar paquetes cuando se detiene el servicio. Sin embargo, el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no espera a que los paquetes se detengan y es posible que algunos paquetes sigan ejecutándose después de detener el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Si se detiene el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], puede seguir ejecutando paquetes con el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)], la Utilidad de ejecución de paquetes y la utilidad del símbolo del sistema **dtexec** (dtexec.exe). Sin embargo, no podrá supervisar los paquetes en ejecución.  
  
 De manera predeterminada, el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se ejecuta en el contexto de la cuenta Servicio de red.  
  
 El servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] escribe en el registro de eventos de Windows. Puede ver los eventos del servicio en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. También puede ver los eventos del servicio mediante el Visor de eventos de Windows.  
  
### <a name="to-set-properties-of-integration-services-service-using-the-services-snap-in"></a>Para establecer las propiedades del servicio Integration Services con el complemento Servicios  
  
-   [Establecer las propiedades del servicio Integration Services](../../2014/integration-services/set-the-properties-of-the-integration-services-service.md)  
  
### <a name="to-view-service-events-for-integration-services-service"></a>Para ver los eventos del servicio para el servicio Integration Services  
  
-   [Ver los eventos para el servicio Integration Services](../../2014/integration-services/view-events-for-the-integration-services-service.md)  
  
## <a name="see-also"></a>Consulte también  
 [Servicio de Integration Services &#40;servicio SSIS&#41;](service/integration-services-service-ssis-service.md)   
 [Configuración del servicio Integration Services &#40;servicio SSIS&#41;](configuring-the-integration-services-service-ssis-service.md)   
 [Asistente para importación y exportación de SQL Server](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [Utilidad DTExec](packages/dtexec-utility.md)   
 [Execution of Projects and Packages](packages/run-integration-services-ssis-packages.md) (Ejecución de proyectos y paquetes)  
  
  
