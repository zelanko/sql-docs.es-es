---
title: 'Paso 1: Copiar el paquete de la lección 5 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ede34999b9ca7a18a2bb5ec997c4a93735b82be2
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389596"
---
# <a name="step-1-copying-the-lesson-5-package"></a>Paso 1: Copiar el paquete de la lección 5
  En esta tarea, creará una copia del paquete que ha creado en la lección 5, denominado Lesson 5.dtsx. También puede agregar al proyecto el paquete completado de la lección 5 que se incluye con el tutorial y, a continuación, copiar dicho paquete. Utilizará esta nueva copia en toda la lección 6.  
  
### <a name="to-copy-the-lesson-5-package"></a>Para copiar el paquete de la lección 5  
  
1.  Si SQL Server Data Tools no está abierto, haga clic en Inicio, seleccione Todos los programas, seleccione Microsoft SQL Server 2012 y, a continuación, haga clic en SQL Server Data Tools.  
  
2.  En el menú Archivo, haga clic en Abrir, haga clic en Proyecto o solución, seleccione SSIS Tutorial, haga clic en Abrir y, después, haga doble clic en SSIS Tutorial.sln.  
  
3.  En el Explorador de soluciones, haga clic con el botón secundario en Lesson 5.dtsx y, a continuación, haga clic en Copiar.  
  
4.  En el Explorador de soluciones, haga clic con el botón secundario en Paquetes SSIS y, a continuación, haga clic en Pegar.  
  
     De forma predeterminada, el paquete copiado se denomina Lesson 6.dtsx.  
  
5.  En el Explorador de soluciones, haga doble clic en Lesson 6.dtsx para abrir el paquete.  
  
6.  Haga clic con el botón secundario en cualquier parte del fondo de la pestaña Flujo de control y luego haga clic en Propiedades.  
  
7.  En la ventana Propiedades, actualice la propiedad Nombre a Lesson 6.  
  
8.  Haga clic en el cuadro de la propiedad ID y, a continuación, haga clic en la flecha desplegable y, a continuación, haga clic en \<generar nuevo Id. >.  
  
### <a name="to-add-the-completed-lesson-5-package"></a>Para agregar el paquete de la lección 5 completada  
  
1.  Abra SQL Server Data Tools y el proyecto SSIS Tutorial.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en Paquetes SSIS y haga clic en Agregar paquete existente.  
  
3.  En el cuadro de diálogo Agregar copia de paquete existente, en Ubicación del paquete, seleccione Sistema de archivos.  
  
4.  Haga clic en el botón Examinar (…), vaya a Lesson 5.dtsx en el equipo y, después, haga clic en **Abrir**.  
  
     Para descargar todos los paquetes de lecciones de este tutorial, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie y pegue el paquete de la lección 5 tal como se describe en los pasos 3 a 8 del procedimiento anterior.  
  
     Después de copiar el paquete de la lección 5, si tiene actualmente los paquetes de las lecciones anteriores en la solución, haga clic con el botón secundario en cada paquete de las lecciones 1 a 5 y, a continuación, haga clic en Excluir del proyecto. Cuando termine, debe tener solo Lesson 6.dtsx en la solución.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 2: Convertir el proyecto al modelo de implementación de proyectos](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
  
