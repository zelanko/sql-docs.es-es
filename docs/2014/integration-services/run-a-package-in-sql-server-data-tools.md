---
title: Ejecutar un paquete en SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6a0d9551f4ad6984ec67bc51e636144195f20b9c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211215"
---
# <a name="run-a-package-in-sql-server-data-tools"></a>Ejecutar un paquete en SQL Server Data Tools
  Los paquetes se ejecutan normalmente en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] durante el desarrollo, la depuración y la comprobación de los paquetes. Cuando se ejecuta un paquete desde el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , siempre se ejecuta inmediatamente.  
  
 Mientras se ejecuta un paquete, el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] muestra el progreso de la ejecución en la pestaña **Progreso** . Puede ver la hora de inicio y de fin del paquete y sus tareas y contendores, además de información acerca de las tareas o contenedores del paquete que generó un error. Una vez que el paquete ha terminado de ejecutarse, la información de tiempo de ejecución permanece disponible en la pestaña **Resultados de la ejecución** . Para obtener más información, vea la sección "Informes de progreso" en el tema [Debugging Control Flow](control-flow/control-flow.md).  
  
 **Implementación en tiempo de diseño**. Cuando se ejecuta un paquete en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], el paquete se genera y luego se implementa en una carpeta. Antes de ejecutar el paquete, puede especificar la carpeta en que se implementa el paquete. Si no especifica una carpeta, se usa de forma predeterminada la carpeta **bin** de forma predeterminada. Este tipo de implementación se denomina implementación en tiempo de diseño.  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>Para ejecutar un paquete en herramientas de datos de SQL Server  
  
1.  En el Explorador de soluciones, si la solución contiene varios proyectos, haga clic con el botón derecho en el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete y, después, haga clic en **Establecer como objeto StartUp** para establecer el proyecto inicial.  
  
2.  En el Explorador de soluciones, si el proyecto contiene varios paquetes, haga clic con el botón derecho en un paquete y, después, haga clic en **Establecer como objeto StartUp** para establecer el paquete inicial.  
  
3.  Para ejecutar un paquete, use uno de los procedimientos siguientes:  
  
    -   Abra el paquete que desea ejecutar y haga clic en **Iniciar depuración** en la barra de menús, o presione F5. Cuando se termine de ejecutar el paquete, presione Mayús+F5 para volver al modo de diseño.  
  
    -   En el Explorador de soluciones, haga clic con el botón derecho en el paquete y, después, haga clic en **Ejecutar paquete**.  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>Para especificar una carpeta diferente para la implementación en tiempo de diseño  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta del proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que quiera ejecutar y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **\<nombre del proyecto> Página de propiedades**, haga clic en **Compilar**.  
  
3.  Actualice el valor de la propiedad OutputPath para especificar la carpeta que quiere usar para la implementación en tiempo de diseño y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Execution of Projects and Packages](packages/run-integration-services-ssis-packages.md)  (Ejecución de proyectos y paquetes)  
 [Paquetes de Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
