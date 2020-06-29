---
title: 'Paso 1: Copiar el paquete de la lección 4 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a2d07500e357d69ba0e07d5453ae7df7f0244360
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440432"
---
# <a name="step-1-copying-the-lesson-4-package"></a>Paso 1: Copia del paquete de la lección 4
  En esta tarea, creará una copia del paquete que ha creado en la lección 4, denominado Lesson 4.dtsx. También puede agregar al proyecto el paquete completado de la lección 4 que se incluye con el tutorial y, después, copiar ese paquete. Usará esta nueva copia en toda la lección 5.  
  
### <a name="to-copy-the-lesson-4-package"></a>Para copiar el paquete de la lección 4  
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server 2012**y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , haga clic en **Abrir**, haga clic en **Proyecto o solución**, seleccione **SSIS Tutorial** , haga clic en **Abrir**y, después, haga doble clic en **SSIS Tutorial.sln**.  
  
3.  En el Explorador de soluciones, haga clic con el botón derecho en **Lesson 4.dtsx**y luego haga clic en **Copiar**.  
  
4.  En Explorador de soluciones, haga clic con el botón secundario en **paquetes SSIS**y, a continuación, haga clic en **pegar**.  
  
     De manera predeterminada, el paquete copiado se denomina Lesson 5.dtsx.  
  
5.  En el Explorador de soluciones, haga doble clic en **Lesson 5.dtsx** para abrir el paquete.  
  
6.  Haga clic con el botón secundario en cualquier parte del fondo de la pestaña **flujo de control** y, después, haga clic en **propiedades**.  
  
7.  En el ventana Propiedades, actualice la `Name` propiedad a `Lesson 5` .  
  
8.  Haga clic en el cuadro de la propiedad **Id.** , haga clic en la flecha desplegable y luego haga clic en **\<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson-4-package"></a>Para agregar el paquete de la lección 4 completada  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.  
  
2.  En Explorador de soluciones, haga clic con el botón secundario en **paquetes SSIS**y haga clic en **Agregar paquete existente**.  
  
3.  En el cuadro de diálogo **Agregar copia de paquete existente** , en **Ubicación del paquete**, seleccione sistema de **archivos**.  
  
4.  Haga clic en el botón examinar **(...)** , vaya a la **Lección 4. DTSX** del equipo y, a continuación, haga clic en **abrir**.  
  
     Para descargar todos los paquetes de lecciones de este tutorial, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **descargas** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie y pegue el paquete de la lección 4 tal como se describe en los pasos 3 a 8 del procedimiento anterior.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 2: Habilitación y configuración de configuraciones de paquete](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
  
