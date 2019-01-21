---
title: 'Paso 1: Copia del paquete de la lección 3 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba011dbb600ca2903aca6f9a3c6415f4663aea0a
ms.sourcegitcommit: e2fa721b6f46c18f1825dd1b0d56c0a6da1b2be1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2019
ms.locfileid: "54211076"
---
# <a name="lesson-4-1-copy-the-lesson-3-package"></a>Lección 4-1: Copia del paquete de la lección 3

En esta tarea, se crea una copia del paquete Lesson 3.dtsx de la lección 3. Si no ha completado la lección 3, puede agregar al proyecto el paquete completado de la lección 3 que se incluye con el tutorial y, después, realizar una copia del paquete con la que trabajar. Esta nueva copia se usará en toda la lección 4.  
  
## <a name="create-the-lesson-4-package"></a>Creación del paquete de la lección 4  
  
Siga estos pasos si va a copiar la lección 3 completada.  Para copiar el ejemplo de la lección 3, vea la sección siguiente.

1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, seleccione **Inicio** > **Todos los programas** > **Microsoft SQL Server 2017** y, después, seleccione **SQL Server Data Tools**.

2.  En el menú **Archivo**, seleccione **Abrir** > **Proyecto o solución**, haga clic en la carpeta **SSIS Tutorial**, haga clic en **Abrir**, y, después, haga doble clic en **SSIS Tutorial.sln**.

3.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Lesson 3.dtsx** y, después, seleccione **Copiar**.

4.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y, después, seleccione **Pegar**.

    De forma predeterminada, el nombre del paquete copiado es **Lesson 4.dtsx**.

5.  En el **Explorador de soluciones**, haga doble clic en **Lesson 4.dtsx** para abrir el paquete.

6.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de **Flujo de control** y seleccione **Propiedades**.

7.  En la ventana **Propiedades**, cambie la propiedad **Nombre** a **Lesson 4**.

8.  Haga clic en el cuadro de la propiedad **ID**, haga clic en la flecha desplegable y después seleccione **\<Generar nuevo Id>**.

## <a name="add-the-completed-lesson-3-package"></a>Adición del paquete de la lección 3 completada

1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.

2.  En **el Explorador de soluciones**, haga clic con el botón derecho en **Paquetes SSIS** y seleccione **Agregar paquete existente**.

3.  En el cuadro de diálogo **Agregar copia de paquete existente** , en **Ubicación del paquete**, seleccione **Sistema de archivos**.

4.  Haga clic en el botón Examinar **(…)**, vaya a **Lesson 3.dtsx** en el equipo y, después, haga clic en **Abrir**.

5.  Copie y pegue el paquete de la lección 3 como se describe en los pasos 3 a 8 de la sección anterior.

  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente  
[Paso 2: Creación de un archivo dañado](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
