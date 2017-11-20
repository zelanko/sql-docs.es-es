---
title: "Paso 1: Creación de la integración de una nuevo proyecto de servicios | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 162bd2913648f8164c11fb425f8ca58a976c74a2
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-1---creating-a-new-integration-services-project"></a>Lección 1: 1: crear un nuevo proyecto de Integration Services
El primer paso al crear un paquete en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es crear un proyecto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Este proyecto incluye las plantillas para los objetos —orígenes de datos, vistas de orígenes de datos y paquetes— que se utilizan en una solución de transformación de datos.  
  
Los paquetes que creará en este tutorial de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] interpretan los valores de los datos dependientes de la configuración regional. Si no tiene configurado el equipo para usar la opción de configuración regional Inglés (Estados Unidos), debe establecer propiedades adicionales en el paquete. Los paquetes utilizados en las lecciones 2 a 5 se copian del paquete creado en la lección 1, y no necesita actualizar las propiedades dependientes de la configuración regional en los paquetes copiados.  
  
> [!NOTE]  
> Este tutorial necesita Microsoft SQL Server Data Tools.  
>   
> Para obtener más información sobre cómo instalar SQL Server Data Tools, consulte [Descargar SQL Server Data Tools](http://msdn.microsoft.com/en-us/data/hh297027).  
  
### <a name="to-create-a-new-integration-services-project"></a>Para crear un proyecto de Integration Services  
  
1.  En el menú **Inicio** , elija **Todos los programas**, **Microsoft SQL Server**y, a continuación, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto** para crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
3.  En el cuadro de diálogo **Nuevo proyecto** , expanda el nodo **Business Intelligence** bajo **Plantillas instaladas**y seleccione **Proyecto de Integration Services** en el panel **Plantillas** .  
  
4.  En el cuadro **Nombre** , cambie el nombre predeterminado por **SSIS Tutorial**. Opcionalmente, desactive la casilla **Crear directorio para la solución** .  
  
5.  Acepte la ubicación predeterminada o haga clic en **Examinar** para desplazarse a la carpeta que desee utilizar. En el cuadro de diálogo **Ubicación del proyecto** , haga clic en la carpeta y, a continuación, haga clic en **Seleccionar carpeta**.  
  
6.  Haga clic en **Aceptar**.  
  
    De forma predeterminada, se creará un paquete vacío, denominado **Package.dtsx**, que se agregará al proyecto bajo Paquetes SSIS.  
  
7.  En la barra de herramientas del **Explorador de soluciones** , haga clic con el botón derecho en **Package.dtsx**, haga clic en **Cambiar nombre**y cambie el nombre del paquete predeterminado por **Lesson 1.dtsx**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 2: agregar y configurar un administrador de conexiones de archivos planos](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  

