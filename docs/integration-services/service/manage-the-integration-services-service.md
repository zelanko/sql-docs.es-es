---
title: "Administrar el servicio Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servicio de Integration Services, configurar"
  - "servicios [Integration Services], configurar"
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 63
---
# Administrar el servicio Integration Services
    
> **IMPORTANTE:** En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 Al instalar el componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se instala también el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se inicia y el tipo de inicio del servicio se establece en automático. Sin embargo, también debe instalar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para usar el servicio y administrar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacenados y en ejecución.  
  
> **NOTA:** Para conectar directamente con una instancia del servicio Integration Services heredado, tendrá que usar la versión de SQL Server Management Studio (SSMS) alineada con la versión de SQL Server en la que se ejecuta el servicio Integration Services. Por ejemplo, para conectar con el servicio Integration Services heredado que se ejecuta en una instancia de SQL Server 2016, debe usar la versión de SSMS publicada para SQL Server 2016. [Descarga de SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).
>
>   En el cuadro de diálogo **Conectar con el servidor** de SSMS, no se puede escribir el nombre de un servidor en el que se está ejecutando una versión anterior del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. En cambio, para administrar paquetes almacenados en un servidor remoto, no tiene que conectarse a la instancia del servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en ese servidor remoto. En su lugar, modifique el archivo de configuración para el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de manera que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] muestre los paquetes almacenados en el servidor remoto. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 Solo puede instalar una única instancia del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo. El servicio no es específico de una instancia determinada de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para realizar la conexión con el servicio se utiliza el nombre del equipo en el que se ejecuta.  
  
 Puede administrar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante uno de los siguientes complementos de Microsoft Management Console (MMC): los servicios o el Administrador de configuración de SQL Server. Antes de que pueda administrar paquetes en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], asegúrese de que se ha iniciado el servicio.  
  
 De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para administrar los paquetes de la base de datos msdb de la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que se instala al mismo tiempo que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si no se instala al mismo tiempo una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)], el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para administrar paquetes de la base de datos msdb de la instancia local predeterminada del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para administrar paquetes que están almacenados en una instancia con nombre o remota de [!INCLUDE[ssDE](../../includes/ssde-md.md)], o en varias instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)], tiene que modificar el archivo de configuración para el servicio. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
 De manera predeterminada, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está configurado para dejar de ejecutar paquetes cuando se detiene el servicio. Sin embargo, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no espera a que los paquetes se detengan y es posible que algunos paquetes sigan ejecutándose después de detener el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Si se detiene el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede seguir ejecutando paquetes con el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)], la Utilidad de ejecución de paquetes y la utilidad del símbolo del sistema **dtexec** (dtexec.exe). Sin embargo, no podrá supervisar los paquetes en ejecución.  
  
 De manera predeterminada, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se ejecuta en el contexto de la cuenta Servicio de red.  
  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escribe en el registro de eventos de Windows. Puede ver los eventos del servicio en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. También puede ver los eventos del servicio mediante el Visor de eventos de Windows.  
  
### Para establecer las propiedades del servicio Integration Services con el complemento Servicios  
  
-   [Establecer las propiedades del servicio Integration Services](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
### Para ver los eventos del servicio para el servicio Integration Services  
  
-   [Ver los eventos para el servicio Integration Services](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
## Vea también  
 [Servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md)   
 [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)   
 [Asistente para importación y exportación de SQL Server](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)   
 [dtexec (utilidad)](../../integration-services/packages/dtexec-utility.md)   
 [Ejecución de proyectos y paquetes](https://msdn.microsoft.com/library/ms141708(v=sql.130).aspx)  
  
  