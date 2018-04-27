---
title: Herramientas de implementación y administración de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1a5190bd675c6ab9fac9b14090ed553eed3bef09
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-ssis-development-and-management-tools"></a>Herramientas de implementación y administración de Integration Services (SSIS)
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye dos estudios para trabajar con paquetes:  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para desarrollar los paquetes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que una solución empresarial requiere. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] proporciona el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el que se crean paquetes.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para administrar paquetes en un entorno de producción.  
  
## <a name="sql-server-data-tools"></a>Herramientas de datos de SQL Server  
 Al trabajar en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], se pueden realizar las siguientes tareas:  
  
-   Ejecutar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para crear paquetes básicos que copian datos de un origen en un destino.  
  
-   Crear paquetes que incluyan flujo de control complejo, flujo de datos, lógica controlada por eventos y registro.  
  
-   Probar y depurar paquetes mediante las características de solución de problemas y supervisión en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , y las características de depuración en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Crear configuraciones que actualizan las propiedades de los paquetes y los objetos de paquete en el tiempo de ejecución.  
  
-   Crear una utilidad de implementación que pueda instalar paquetes y sus dependencias en otros equipos.  
  
-   Guardar copias de paquetes en la base de datos msdb de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el almacén de paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] y el sistema de archivos.  
  
 Para obtener más información sobre [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], consulte [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx).  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] proporciona el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que utiliza para administrar los paquetes, supervisar los paquetes en ejecución y determinar el impacto y el linaje de los datos de los objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Al trabajar en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], se pueden realizar las siguientes tareas:  
  
-   Crear carpetas para organizar paquetes de una manera que sirva para su organización.  
  
-   Ejecutar paquetes que se almacenan en el equipo local mediante la utilidad de ejecución de paquetes.  
  
-   Ejecutar la Utilidad de ejecución de paquetes para generar una línea de comandos para usarse al ejecutar a utilidad de símbolo del sistema **dtexec** (dtexec.exe).  
  
-   Importar y exportar paquetes hacia y desde la base de datos msdb de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el Almacén de paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] y el sistema de archivos.  
