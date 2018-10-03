---
title: 'Paso 1: Copiar el paquete de la lección 4 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76017bf54455d702dbea060e4f966765ddb1e47b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070025"
---
# <a name="step-1-copying-the-lesson-4-package"></a>Paso 1: Copiar el paquete de la lección 4
  En esta tarea, creará una copia del paquete que ha creado en la lección 4, denominado Lesson 4.dtsx. También puede agregar al proyecto el paquete completado de la lección 4 que se incluye con el tutorial y, después, copiar ese paquete. Usará esta nueva copia en toda la lección 5.  
  
### <a name="to-copy-the-lesson-4-package"></a>Para copiar el paquete de la lección 4  
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server 2012**y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , haga clic en **Abrir**, haga clic en **Proyecto o solución**, seleccione **SSIS Tutorial** , haga clic en **Abrir**y, después, haga doble clic en **SSIS Tutorial.sln**.  
  
3.  En el Explorador de soluciones, haga clic con el botón derecho en **Lesson 4.dtsx**y luego haga clic en **Copiar**.  
  
4.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS**y, después, haga clic en **Pegar**.  
  
     De manera predeterminada, el paquete copiado se denomina Lesson 5.dtsx.  
  
5.  En el Explorador de soluciones, haga doble clic en **Lesson 5.dtsx** para abrir el paquete.  
  
6.  Haga clic con el botón derecho en cualquier parte del fondo de la pestaña **Flujo de control** y luego haga clic en **Propiedades**.  
  
7.  En la ventana Propiedades, actualice el `Name` propiedad `Lesson 5`.  
  
8.  Haga clic en el cuadro para la **ID** propiedad, a continuación, haga clic en la flecha desplegable y, a continuación, haga clic en  **\<generar nuevo Id. >**.  
  
### <a name="to-add-the-completed-lesson-4-package"></a>Para agregar el paquete de la lección 4 completada  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS** y haga clic en **Agregar paquete existente**.  
  
3.  En el cuadro de diálogo **Agregar copia de paquete existente** , en **Ubicación del paquete**, seleccione **Sistema de archivos**.  
  
4.  Haga clic en el botón Examinar **(…)** , vaya a **Lesson 4.dtsx** en el equipo y, después, haga clic en **Abrir**.  
  
     Para descargar todos los paquetes de lecciones de este tutorial, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie y pegue el paquete de la lección 4 tal como se describe en los pasos 3 a 8 del procedimiento anterior.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 2: Habilitar y configurar las configuraciones de paquetes](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
  
