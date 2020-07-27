---
title: 'Paso 1: Copiar el paquete de la lección 5 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a8df0901617b22317b2a87616be7b769c749d298
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922136"
---
# <a name="lesson-6-1-copy-the-lesson-5-package"></a>Lección 6-1: Copiar el paquete de la lección 5

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



En esta tarea se crea una copia del paquete **Lesson 5.dtsx** de la lección 5. Si no ha completado la lección 5, puede agregar al proyecto el paquete completado de la lección 5 incluido en el tutorial y luego realizar una copia para trabajar con ella. Esta nueva copia se usa en toda la lección 6. 

> [!IMPORTANT]
> Después de copiar el paquete de la lección 5, si tiene los paquetes de las lecciones anteriores en la solución, haga clic con el botón derecho en cada paquete de las lecciones 1 a 5 y seleccione **Excluir del proyecto**. Cuando termine, debe tener solo **Lesson 6.dtsx** en la solución.   
  
## <a name="create-the-lesson-6-package"></a>Crear el paquete de la lección 6  
  
Use este procedimiento si va a copiar la lección 5 completada.  Para copiar la lección 5 de ejemplo, vea la sección siguiente.

1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, seleccione **Inicio** > **Todos los programas** > **Microsoft SQL Server 2017** y, después, seleccione **SQL Server Data Tools**.

2.  En el menú **Archivo**, seleccione **Abrir** > **Proyecto o solución**, haga clic en la carpeta **SSIS Tutorial**, haga clic en **Abrir**, y, después, haga doble clic en **SSIS Tutorial.sln**.

3.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Lesson 5.dtsx** y luego seleccione **Copiar**.

4.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y, después, seleccione **Pegar**.

    De forma predeterminada, el nombre del paquete copiado es **Lesson 5.dtsx**.

5.  En el **Explorador de soluciones**, haga doble clic en **Lesson 5.dtsx** para abrir el paquete.

6.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de **Flujo de control** y seleccione **Propiedades**.

7.  En la ventana **Propiedades**, cambie la propiedad **Nombre** por **Lesson 6**.

8.  Seleccione el cuadro de la propiedad **Id.** , seleccione la flecha desplegable y, después, seleccione **\<Generate New ID>** .

## <a name="add-the-completed-lesson-5-package"></a>Agregar el paquete de la lección 5 completado

1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.

2.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y seleccione **Agregar paquete existente**.

3.  En el cuadro de diálogo **Agregar copia de paquete existente** , en **Ubicación del paquete**, seleccione **Sistema de archivos**.

4.  Seleccione el botón Examinar **(…)** , vaya a **Lesson 5.dtsx** en el equipo y luego seleccione **Abrir**.

5.  Copie y pegue el paquete de la lección 5 como se ha explicado en los pasos 3 a 8 de la sección anterior.

## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 2: Convertir el proyecto al modelo de implementación de proyectos](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
