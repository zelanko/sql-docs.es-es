---
title: "Ejecutar un paquete en herramientas de datos de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Paquetes de Integration Services, ejecutar"
  - "paquetes SSIS, ejecutar"
  - "paquetes [Integration Services], ejecución"
  - "paquetes de SQL Server Integration Services, ejecutar"
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# Ejecutar un paquete en herramientas de datos de SQL Server
  Los paquetes se ejecutan normalmente en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante el desarrollo, la depuración y la comprobación de los paquetes. Cuando se ejecuta un paquete desde el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , siempre se ejecuta inmediatamente.  
  
 Mientras se ejecuta un paquete, el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] muestra el progreso de la ejecución en la pestaña **Progreso** . Puede ver la hora de inicio y de fin del paquete y sus tareas y contendores, además de información acerca de las tareas o contenedores del paquete que generó un error. Una vez que el paquete ha terminado de ejecutarse, la información de tiempo de ejecución permanece disponible en la pestaña **Resultados de la ejecución**. Para obtener más información, vea la sección "Informes de progreso" en el tema [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 **Implementación en tiempo de diseño**. Cuando se ejecuta un paquete en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], el paquete se genera y luego se implementa en una carpeta. Antes de ejecutar el paquete, puede especificar la carpeta en que se implementa el paquete. Si no especifica una carpeta, se usa de forma predeterminada la carpeta **bin** de forma predeterminada. Este tipo de implementación se denomina implementación en tiempo de diseño.  
  
### Para ejecutar un paquete en herramientas de datos de SQL Server  
  
1.  En el Explorador de soluciones, si la solución contiene varios proyectos, haga clic con el botón derecho en el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete y, después, haga clic en **Establecer como objeto StartUp** para establecer el proyecto inicial.  
  
2.  En el Explorador de soluciones, si el proyecto contiene varios paquetes, haga clic con el botón derecho en un paquete y, después, haga clic en **Establecer como objeto StartUp** para establecer el paquete inicial.  
  
3.  Para ejecutar un paquete, use uno de los procedimientos siguientes:  
  
    -   Abra el paquete que desea ejecutar y haga clic en **Iniciar depuración** en la barra de menús, o presione F5. Cuando se termine de ejecutar el paquete, presione Mayús+F5 para volver al modo de diseño.  
  
    -   En el Explorador de soluciones, haga clic con el botón derecho en el paquete y, después, haga clic en **Ejecutar paquete**.  
  
### Para especificar una carpeta diferente para la implementación en tiempo de diseño  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta del proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que quiera ejecutar y, después, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **\<nombre del proyecto> Página de propiedades**, haga clic en **Compilar**.  
  
3.  Actualice el valor de la propiedad OutputPath para especificar la carpeta que quiere usar para la implementación en tiempo de diseño y haga clic en **Aceptar**.  
  
## Vea también  
 [Ejecución de proyectos y paquetes](https://msdn.microsoft.com/library/hh213290.aspx)   
 [paquetes de Integration Services (SSIS)](https://msdn.microsoft.com/library/ms141134.aspx)  
  
  