---
title: 'Paso 1: Copiar el paquete de la lección 4 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d97cf4f9f877ad29f1e5b17d9f79df4a8171b8ed
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65721750"
---
# <a name="lesson-5-1-copy-the-lesson-4-package"></a>Lección 5-1: Copiar el paquete de la lección 4

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En esta tarea se crea una copia del paquete **Lesson 4.dtsx** de la lección 4. Si no ha completado la lección 4, puede agregar al proyecto el paquete completado de la lección 4 incluido en el tutorial y luego realizar una copia para trabajar con ella. Esta nueva copia se usa en toda la lección 5.  
  
## <a name="create-the-lesson-5-package"></a>Crear el paquete de la lección 5  
  
Use este procedimiento si va a copiar la lección 4 completada.  Para copiar la lección 4 de ejemplo, vea la sección siguiente.

1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, seleccione **Inicio** > **Todos los programas** > **Microsoft SQL Server 2017** y, después, seleccione **SQL Server Data Tools**.

2.  En el menú **Archivo**, seleccione **Abrir** > **Proyecto o solución**, seleccione la carpeta **SSIS Tutorial** y luego **Abrir**.  Luego haga doble clic en **SSIS Tutorial.sln**.

3.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Lesson 4.dtsx** y luego seleccione **Copiar**.

4.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y luego seleccione **Pegar**.

    De forma predeterminada, el nombre del paquete copiado es **Lesson 4.dtsx**.

5.  En el **Explorador de soluciones**, haga doble clic en **Lesson 4.dtsx** para abrir el paquete.

6.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de **Flujo de control** y seleccione **Propiedades**.

7.  En la ventana **Propiedades**, cambie la propiedad **Nombre** por **Lesson 5**.

8.  Haga clic en el cuadro de la propiedad **ID**, haga clic en la flecha desplegable y después seleccione **\<Generar nuevo Id>**.

## <a name="add-the-completed-lesson-4-package"></a>Agregar el paquete de la lección 4 completado

1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.

2.  En **el Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y seleccione **Agregar paquete existente**.

3.  En el cuadro de diálogo **Agregar copia de paquete existente** , en **Ubicación del paquete**, seleccione **Sistema de archivos**.

4.  Seleccione el botón Examinar **(…)**, vaya a **Lesson 4.dtsx** en el equipo y luego seleccione **Abrir**.

5.  Copie y pegue el paquete de la lección 4 como se ha explicado en los pasos 3 a 8 de la sección anterior.
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente  
[Paso 2: Habilitar y configurar configuraciones de paquetes](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
