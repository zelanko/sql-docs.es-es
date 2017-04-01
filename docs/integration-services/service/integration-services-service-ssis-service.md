---
title: "Servicio Integration Services (servicio SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servicio Integration Services, acerca del servicio Integration Services"
  - "SQL Server Integration Services, servicio"
  - "servicio [Integration Services]; acerca del servicio Integration Services"
  - "servicio [Integration Services]"
  - "SQL Server Integration Services, servicio"
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Servicio Integration Services (servicio SSIS)
  Los temas de esta sección describen el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio de Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . No se requiere este servicio para crear, guardar y ejecutar los paquetes de Integration Services. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacena objetos, valores y datos operativos en la base de datos **SSISDB** para los proyectos que se han implementado en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante el modelo de implementación de proyectos. El servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que es una instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , hospeda la base de datos. Para obtener más información sobre la base de datos, vea [Catálogo de SSIS](../../integration-services/service/ssis-catalog.md). Para obtener más información sobre la implementación de proyectos en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Implementar proyectos en el servidor de Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
## Capacidades de administración  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un servicio de Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] solo está disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Ejecutar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona las siguientes capacidades de administración:  
  
-   Iniciar paquetes almacenados en ubicaciones locales y remotas  
  
-   Detener paquetes que se ejecutan en ubicaciones locales y remotas  
  
-   Supervisar paquetes que se ejecutan en ubicaciones locales y remotas  
  
-   Importar y exportar paquetes  
  
-   Administrar el almacenamiento de paquetes  
  
-   Personalizar carpetas de almacenamiento  
  
-   Detener paquetes que se están ejecutando cuando se detiene el servicio  
  
-   Ver el registro de eventos de Windows  
  
-   Conectar con varios servidores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
## Tipo de inicio para el servicio Integration Services  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se instala al instalar el componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se inicia y el tipo de inicio del servicio se establece en automático. El servicio se debe ejecutar para poder supervisar los paquetes almacenados en el Almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] . El Almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] puede ser la base de datos msdb en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o las carpetas designadas en el sistema de archivos.  
  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no es necesario si únicamente desea diseñar y ejecutar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Sin embargo, sí se necesita para ver la lista de paquetes y supervisarlos con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## Tareas relacionadas  
  
-   [Establecer las propiedades del servicio Integration Services](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
-   [Ver los eventos para el servicio Integration Services](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
  