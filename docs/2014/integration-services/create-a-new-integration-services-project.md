---
title: Crear un nuevo proyecto de Integration Services | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- projects [Integration Services], creating
- Integration Services projects, creating
- SQL Server Integration Services projects, creating
- SSIS projects, creating
ms.assetid: 1e23f259-0401-4333-ab4f-89809aae63b1
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4ee4484b97102b6bae3bd9496ee161233c47ee12
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105654"
---
# <a name="create-a-new-integration-services-project"></a>Crear un proyecto de Integration Services
  Este procedimiento crea un nuevo proyecto y una nueva solución de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
### <a name="to-create-a-new-integration-services-project"></a>Para crear un proyecto de Integration Services  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**.  
  
3.  En el cuadro de diálogo **Nuevo proyecto** , en el panel **Plantillas** , seleccione la plantilla **Proyecto de Integration Services** .  
  
     La plantilla **Proyecto de Integration Services** crea un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene un único paquete vacío.  
  
4.  Si lo desea, modifique el nombre y la ubicación del proyecto.  
  
     El nombre de la solución se actualiza automáticamente para que coincida con el nombre del proyecto.  
  
5.  Para crear una carpeta diferente para el archivo de solución, seleccione **Crear directorio para la solución**. Ésta es la opción predeterminada.  
  
6.  Si en el equipo hay instalado software de control de código fuente, seleccione **Agregar al control de código fuente**  para asociar el proyecto con el control de código fuente.  
  
7.  Si el software de control de código fuente es [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, se abre el cuadro de diálogo **Inicio de sesión en Visual SourceSafe** . En **Inicio de sesión en Visual SourceSafe**, proporcione un nombre de usuario, una contraseña y el nombre de la base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe. Haga clic en **Examinar** para buscar la base de datos.  
  
    > [!NOTE]  
    >  Para ver y cambiar el complemento de control de código fuente seleccionado y para configurar el entorno de control de código fuente, haga clic en **Opciones** en el menú **Herramientas** y, después, expanda el nodo **Control de código fuente**.  
  
8.  Haga clic en **Aceptar** para agregar la solución al **el Explorador de soluciones**r y agregar el proyecto a la solución.  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; proyectos](integration-services-ssis-projects-and-solutions.md)   
 [Agregar o quitar un proyecto de Integration Services en una solución](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
  