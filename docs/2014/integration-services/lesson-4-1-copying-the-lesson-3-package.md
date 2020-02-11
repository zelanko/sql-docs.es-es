---
title: 'Paso 1: Copiar el paquete de la lección 3 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c3a765f23b4bfcdd4d8f0ff84ac8d363424882bc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767457"
---
# <a name="step-1-copying-the-lesson-3-package"></a>Paso 1: copiar el paquete de la lección 3
  En esta tarea, creará una copia del paquete que ha creado en la lección 3, denominado Lesson 3.dtsx. Por otra parte, si no ha completado la lección 3, puede agregar al proyecto el paquete completado de la lección 3 que se incluye con el tutorial y, a continuación, copiar dicho paquete para trabajar. Usará esta nueva copia en toda la lección 4.  
  
### <a name="to-create-the-lesson-4-package"></a>Para crear el paquete de la lección 4  
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server**y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **archivo** , haga clic en **abrir**, haga clic en **proyecto o solución**, seleccione **SSIS tutorial** , haga clic en **abrir**y, a continuación, haga doble clic en **SSIS tutorial. sln**.  
  
3.  En el Explorador de soluciones, haga clic con el botón derecho en **Lesson 3.dtsx**y, después, haga clic en **Copiar**.  
  
4.  En Explorador de soluciones, haga clic con el botón secundario en **paquetes SSIS**y, a continuación, haga clic en **pegar**.  
  
     De forma predeterminada, el paquete copiado se denomina Lesson 4.dtsx.  
  
5.  En Explorador de soluciones, haga doble clic en la **Lección 4. DTSX** para abrir el paquete.  
  
6.  Haga clic con el botón derecho en cualquier parte del fondo de la pestaña **Flujo de control** y haga clic en **Propiedades**.  
  
7.  En el ventana Propiedades, actualice la `Name` propiedad a `Lesson 4`.  
  
8.  Haga clic en el cuadro de la propiedad **ID** y, a continuación, en la lista, haga clic en ** \<generar nuevo ID>**.  
  
### <a name="to-add-the-completed-lesson-3-package"></a>Para agregar el paquete de la lección 3 completada  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y abra el proyecto SSIS Tutorial.  
  
2.  En Explorador de soluciones, haga clic con el botón secundario en **paquetes SSIS**y haga clic en **Agregar paquete existente**.  
  
3.  En el cuadro de diálogo **Agregar copia de paquete existente** , en **Ubicación del paquete**, seleccione sistema de **archivos**.  
  
4.  Haga clic en el botón Examinar **(…)**, busque Lesson 3.dtsx en el equipo y, después, haga clic en **Abrir**.  
  
     Para descargar todos los paquetes de lecciones de este tutorial, haga lo siguiente.  
  
    1.  Vaya a [Integration Services ejemplos de productos](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **descargas** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie y pegue el paquete de la lección 3 tal como se describe en los pasos del 3 a 8 del procedimiento anterior.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 2: Crear un archivo dañado](lesson-4-2-creating-a-corrupted-file.md)  
  
  
