---
title: "Integration Services (SSIS) Server y el cat&#225;logo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "paquetes [Integration Services], administración"
  - "administrar paquetes [Integration Services]"
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Integration Services (SSIS) Server y el cat&#225;logo
  Después de diseñar y probar paquetes en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede implementar los proyectos que contienen los paquetes en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 El [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server es una instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda el **SSISDB** base de datos. La base de datos almacena los objetos siguientes: paquetes, proyectos, parámetros, permisos, propiedades del servidor e historial operativo.  
  
 La base de datos de **SSISDB** expone la información de objetos en vistas públicas que puede consultar. La base de datos también proporciona procedimientos almacenados a los que puede llamar para administrar los objetos.  
  
 Para poder implementar los proyectos para el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server, deberá crear el **SSISDB** catálogo.  
  
 Para obtener información general de la funcionalidad del catálogo SSISDB, vea [catálogo de SSIS](../../integration-services/service/ssis-catalog.md).  
  
## Alta disponibilidad  
 Como otras bases de datos de usuario, la base de datos de **SSISDB** admite la creación de reflejo de la base de datos y la replicación. Para obtener más información acerca de la creación de reflejo y replicación, consulte [creación de reflejo de base de datos & #40; SQL Server & #41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 También puede proporcionar alta disponibilidad de SSISDB y su contenido haciendo uso de SSIS y grupos de disponibilidad AlwaysOn. Para obtener más información, consulte esta entrada de blog de Matt Masson, [SSIS con Always On](http://go.microsoft.com/fwlink/?LinkId=255873), en blogs.msdn.com.  
  
##  <a name="ssms"></a> Servidor de Integration Services en SQL Server Management Studio  
 Cuando se conecta a una instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda el **SSISDB** base de datos, vea los siguientes objetos en el Explorador de objetos:  
  
-   **Base de datos SSISDB**  
  
     La base de datos de **SSISDB** aparece en el nodo **Bases de datos** del Explorador de objetos. Puede consultar las vistas y llamar a los procedimientos almacenados que administran el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los objetos que están almacenados en el servidor.  
  
-   **Catálogos de Integration Services**  
  
     En el nodo **Catálogos de Integration Services** hay carpetas para los proyectos y los entornos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## Tareas relacionadas  
  
-   [Crear el catálogo de SSIS](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [Ver la lista de paquetes en el servidor de Integration Services](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Implementar proyectos en el servidor de Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
-   [Ejecutar un paquete en el Servidor SSIS con SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## Contenido relacionado  
 Entrada de blog, [SSIS con Always On](http://go.microsoft.com/fwlink/?LinkId=255873), en blogs.msdn.com.  
  
  