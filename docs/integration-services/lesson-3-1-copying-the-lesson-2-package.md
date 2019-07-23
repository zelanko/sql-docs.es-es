---
title: 'Paso 1: Copia del paquete de la lección 2 | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 235e6e3d5ce700c230641364df548765f3be4255
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086545"
---
# <a name="lesson-3-1-copy-the-lesson-2-package"></a>Lección 3-1: Copia del paquete de la lección 2

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En esta tarea, se crea una copia del paquete Lesson 2.dtsx de la lección 2. Si no ha completado la lección 2, puede agregar al proyecto el paquete completado de la lección 2 que se incluye con el tutorial y, después, copiar dicho paquete. Esta nueva copia se usará en toda la lección 3.

## <a name="create-the-lesson-3-package"></a>Creación del paquete de la lección 3

Siga estos pasos si va a copiar la lección 2 completada.  Para copiar el ejemplo de la lección 2, vea la sección siguiente.

1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, seleccione **Inicio** > **Todos los programas** > **Microsoft SQL Server 2017** y, después, seleccione **SQL Server Data Tools**.

2.  En el menú **Archivo**, seleccione **Abrir** > **Proyecto o solución**, haga clic en la carpeta **SSIS Tutorial**, haga clic en **Abrir**, y, después, haga doble clic en **SSIS Tutorial.sln**.

3.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Lesson 2.dtsx** y, después, seleccione **Copiar**.

4.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y, después, seleccione **Pegar**.

    De forma predeterminada, el nombre del paquete copiado es Lesson 3.dtsx.

5.  En el **Explorador de soluciones**, haga doble clic en **Lesson 3.dtsx** para abrir el paquete.

6.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de **Flujo de control** y seleccione **Propiedades**.

7.  En la ventana **Propiedades**, cambie la propiedad **Nombre** a **Lesson 3**.

8.  Haga clic en el cuadro de la propiedad **ID**, haga clic en la flecha desplegable y después seleccione **\<Generar nuevo Id>** .

## <a name="add-the-completed-lesson-2-package"></a>Adición del paquete de la lección 2 completada

1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.

2.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y seleccione **Agregar paquete existente**.

3.  En el cuadro de diálogo **Agregar copia de paquete existente**, en **Ubicación del paquete**, seleccione **Sistema de archivos**.

4.  Haga clic en el botón Examinar **(…)** , vaya a **Lesson 2.dtsx** en el equipo y, después, haga clic en **Abrir**.

5.  Copie y pegue el paquete de la lección 3 como se describe en los pasos 3 a 8 de la sección anterior.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 2: Adición y configuración del registro](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
