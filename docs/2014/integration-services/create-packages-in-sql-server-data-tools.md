---
title: Crear paquetes en SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7053c5cd9780e578697c1bc08e6bb1b0c32ca1f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62828881"
---
# <a name="create-packages-in-sql-server-data-tools"></a>Crear paquetes en herramientas de datos de SQL Server
  Los paquetes que creó en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mediante el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] se guardan en el sistema de archivos. Para guardar un paquete en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o en el almacén de paquetes, necesita guardar una copia del paquete. Para más información, vea [Guardar una copia de un paquete](../../2014/integration-services/save-a-copy-of-a-package.md).  
  
 En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], puede crear un paquete nuevo utilizando uno de los métodos siguientes:  
  
-   Usar la plantilla de paquete que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye.  
  
-   Utilización de una plantilla personalizada  
  
     Para utilizar paquetes personalizados como plantillas en la creación de nuevos paquetes, solo tiene que copiarlos en la carpeta DataTransformationItems. De forma predeterminada, esta carpeta se encuentra en C:\Archivos de programa\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
-   Copiar un paquete existente.  
  
     Si los paquetes existentes incluyen funcionalidades que desea volver a usar, puede general el flujo de control y los flujos de datos en el nuevo paquete más rápidamente copiando y pegando objetos desde otros paquetes. Para más información sobre el uso de copiar y pegar en proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , vea [Volver a utilizar objetos de paquete](reuse-of-package-objects.md).  
  
     Si crea un nuevo paquete mediante la copia de un paquete existente o mediante el uso de un paquete personalizado como plantilla, también se copian el nombre y GUID del paquete existente. Deberá actualizar el nombre y el GUID del nuevo paquete para diferenciarlo del paquete del que se copió. Por ejemplo, si los paquetes tienen el mismo GUID, es más difícil identificar el paquete al que pertenecen los datos del registro. Puede volver a generar el GUID en la propiedad `ID` y actualizar el valor de la propiedad `Name` mediante la ventana Propiedades de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para más información, vea [Establecer las propiedades de paquetes](set-package-properties.md) y [dtutil (utilidad)](dtutil-utility.md).  
  
-   Usar un paquete personalizado que ha designado como una plantilla.  
  
-   Ejecutar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
     El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] crea un paquete completo para una importación o exportación simples. Este asistente configura las conexiones, el origen y el destino, y agrega las transformaciones de datos que se necesiten para poder ejecutar la importación o exportación inmediatamente. Si lo desea, puede guardar el paquete para ejecutarlo de nuevo posteriormente o refinarlo y mejorarlo en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Sin embargo, si lo guarda, debe agregar el paquete a un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] existente para poder cambiar o ejecutar el paquete en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 En los procedimientos siguientes se describe cómo crear o eliminar un paquete en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Para ver un vídeo donde se muestra cómo crear un paquete básico con la plantilla de paquete predeterminada, visite [Crear un paquete básico (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131023).  
  
### <a name="to-create-a-package-in-sql-server-data-tools-using-the-package-template"></a>Para crear un paquete en herramientas de datos de SQL Server mediante la plantilla de paquete  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el que desea crear un paquete.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Paquetes SSIS** y, después, haga clic en **Nuevo paquete de SSIS**.  
  
3.  Opcionalmente, agregue flujo de control, tareas de flujo de datos y controladores de eventos al paquete. Para más información, vea [Flujo de control](control-flow/control-flow.md), [Flujo de datos](data-flow/data-flow.md)y [Controladores de eventos de Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md).  
  
4.  En el menú **Archivo** , haga clic en **Guardar los elementos seleccionados** para guardar el nuevo paquete.  
  
    > [!NOTE]  
    >  Puede guardar un paquete vacío.  
  
  
