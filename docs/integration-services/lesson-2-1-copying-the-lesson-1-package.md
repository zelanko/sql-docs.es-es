---
title: 'Paso 1: Copia del paquete de la lección 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 66077bac6ef3ce7f52b03eb5a439aa24a89449a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65722732"
---
# <a name="lesson-2-1-copy-the-lesson-1-package"></a>Lección 2-1: Copia del paquete de la lección 1

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En esta tarea, se crea una copia del paquete **Lesson 1.dtsx**. Si no ha completado la lección 1, puede usar el paquete completado de la lección 1 que se incluye con este tutorial. En el resto de la lección 2 se usa esta copia nueva.  
  
## <a name="create-the-lesson-2-package"></a>Creación del paquete de la lección 2  

Siga estos pasos si va a copiar la Lección 1 completada.  Para copiar el ejemplo de la lección 1, vea la sección siguiente.
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, seleccione **Inicio** > **Todos los programas** > **Microsoft SQL Server 2017** y, después, seleccione **SQL Server Data Tools**.  
  
2.  En el menú **Archivo**, seleccione **Abrir** > **Proyecto o solución**, haga clic en la carpeta **SSIS Tutorial**, haga clic en **Abrir**, y, después, haga doble clic en **SSIS Tutorial.sln**.  
  
3.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Lesson 1.dtsx** y, después, seleccione **Copiar**.  
  
4.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y, después, seleccione **Pegar**.  
  
    De forma predeterminada, el paquete copiado se denomina **Lesson 2.dtsx**.  
  
5.  En el **Explorador de soluciones**, haga doble clic en **Lesson 2.dtsx** para abrir el paquete.  
  
6.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de **Flujo de control** y seleccione **Propiedades**.  
  
7.  En la ventana **Propiedades**, cambie la propiedad **Nombre** a **Lesson 2**.  
  
8.  Haga clic en el cuadro de la propiedad **ID**, haga clic en la flecha desplegable y después seleccione **\<Generar nuevo Id>** .  
  
## <a name="use-the-sample-lesson-1-package"></a>Uso del paquete de la lección 1 de ejemplo  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.  
  
2.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y seleccione **Agregar paquete existente**.  
  
3.  En el cuadro de diálogo **Agregar copia de paquete existente**, en **Ubicación del paquete**, seleccione **Sistema de archivos**.  
  
4.  Haga clic en el botón Examinar **(…)** , vaya a **Lesson 1.dtsx** en el equipo y, después, haga clic en **Abrir**.  
  
5.  Copie y pegue el paquete de la lección 1 como se describe en los pasos 3 a 8 de la sección anterior.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente

[Paso 2: Adición y configuración del contenedor de bucles Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
