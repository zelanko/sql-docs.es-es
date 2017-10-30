---
title: "Integration Services (SSIS) Server y el catálogo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 939f31adf1ab0a975bd4339dabab310ef9025049
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-server-and-catalog"></a>Integration Services (SSIS) Server y el catálogo
  Después de diseñar y probar paquetes en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede implementar los proyectos que contienen los paquetes en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 El servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos de **SSISDB** . La base de datos almacena los objetos siguientes: paquetes, proyectos, parámetros, permisos, propiedades del servidor e historial operativo.  
  
 La base de datos de **SSISDB** expone la información de objetos en vistas públicas que puede consultar. La base de datos también proporciona procedimientos almacenados a los que puede llamar para administrar los objetos.  
  
 Para poder implementar los proyectos en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , debe crear el catálogo de **SSISDB** .  
  
 Para obtener información general de la funcionalidad del catálogo SSISDB, vea [catálogo de SSIS](../../integration-services/service/ssis-catalog.md).  
  
## <a name="high-availability"></a>Alta disponibilidad  
 Como otras bases de datos de usuario, la base de datos de **SSISDB** admite la creación de reflejo de la base de datos y la replicación. Para obtener más información acerca de la creación de reflejo y replicación, consulte [creación de reflejo de base de datos &#40; SQL Server &#41; ](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 También puede proporcionar alta disponibilidad de SSISDB y su contenido mediante la realización de uso de SSIS y grupos de disponibilidad AlwaysOn. Para obtener más información, consulte esta entrada de blog de Matt Masson, [SSIS con Always On](http://go.microsoft.com/fwlink/?LinkId=255873), en blogs.msdn.com.  
  
##  <a name="ssms"></a> Servidor de Integration Services en SQL Server Management Studio  
 Al conectarse a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos de **SSISDB** , ve los objetos siguientes en el Explorador de objetos:  
  
-   **Base de datos SSISDB**  
  
     La base de datos de **SSISDB** aparece en el nodo **Bases de datos** del Explorador de objetos. Puede consultar las vistas y llamar a los procedimientos almacenados que administran el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los objetos que están almacenados en el servidor.  
  
-   **Catálogos de Integration Services**  
  
     En el nodo **Catálogos de Integration Services** hay carpetas para los proyectos y los entornos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
-   [Ver la lista de paquetes en el servidor de servicios de integración](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Implementación de Integration Services (SSIS) proyectos y paquetes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
-   [Ejecutar paquetes de Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, [SSIS con Always On](http://go.microsoft.com/fwlink/?LinkId=255873), en blogs.msdn.com.  
  
  

