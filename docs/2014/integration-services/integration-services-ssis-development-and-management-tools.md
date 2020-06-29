---
title: Entornos de Integration Services (SSIS) y Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65ee6741020d9d67f9b87ecea92022f47e6adc50
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436542"
---
# <a name="integration-services-ssis-and-studio-environments"></a>Entornos de Studio e Integration Services (SSIS)
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye dos estudios para trabajar con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para desarrollar los paquetes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que una solución empresarial requiere. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] proporciona el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el que se crean paquetes.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para administrar paquetes en un entorno de producción.  
  
## <a name="sql-server-data-tools"></a>SQL Server Data Tools  
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
  
