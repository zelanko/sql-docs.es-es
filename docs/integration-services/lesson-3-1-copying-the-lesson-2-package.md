---
title: 'Paso 1: Copiar el paquete de la lección 2 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae60895da9a461b7bcf7fb8fa034833e39c68e1a
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51637792"
---
# <a name="lesson-3-1---copying-the-lesson-2-package"></a>Lección 3-1: Copiar el paquete de la lección 2
En esta tarea, creará una copia del paquete que ha creado en la lección 2, denominado Lesson 2.dtsx. También puede agregar al proyecto el paquete completado de la lección 2 que se incluye con el tutorial y, después, copiar dicho paquete. Usará esta nueva copia en toda la lección 3.  
  
### <a name="to-create-the-lesson-3-package"></a>Para crear el paquete de la lección 3  
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server 2012** y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , haga clic en **Abrir**, haga clic en **Proyecto o solución**, seleccione **SSIS Tutorial** , haga clic en **Abrir**y, después, haga doble clic en **SSIS Tutorial.sln**.  
  
3.  En el Explorador de soluciones, haga clic con el botón derecho en **Lesson 2.dtsx**y, después, haga clic en **Copiar**.  
  
4.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS** y, después, haga clic en **Pegar**.  
  
    De forma predeterminada, el paquete copiado se denomina Lesson 3.dtsx.  
  
5.  En el Explorador de soluciones, haga doble clic en **Lesson 3.dtsx** para abrir el paquete.  
  
6.  Haga clic con el botón derecho en cualquier parte del fondo de la pestaña **Flujo de control** y haga clic en **Propiedades**.  
  
7.  En la ventana Propiedades, actualice la propiedad **Nombre** a **Lesson 3**.  
  
8.  Haga clic en el cuadro para la propiedad **ID** y, en la lista, haga clic en **<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson2-package"></a>Para agregar el paquete de la lección 2 completada  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y abra el proyecto SSIS Tutorial.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS**y haga clic en **Agregar paquete existente**.  
  
3.  En el cuadro de diálogo **Agregar copia de paquete existente** , en **Ubicación del paquete**, seleccione **Sistema de archivos**.  
  
4.  Haga clic en el botón de búsqueda **(…)** , vaya a **Lesson 2.dtsx** en el equipo y, después, haga clic en **Abrir**.  
  
    Para descargar todos los paquetes de lecciones de este tutorial, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie y pegue el paquete de la lección 3 tal como se describe en los pasos del 3 a 8 del procedimiento anterior.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 2: Agregar y configurar el registro](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
