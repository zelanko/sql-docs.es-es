---
title: "Paso 1: copiar el paquete de la lecci&#243;n 3 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Paso 1: copiar el paquete de la lecci&#243;n 3
En esta tarea, creará una copia del paquete que ha creado en la lección 3, denominado Lesson 3.dtsx. Por otra parte, si no ha completado la lección 3, puede agregar al proyecto el paquete completado de la lección 3 que se incluye con el tutorial y, a continuación, copiar dicho paquete para trabajar. Usará esta nueva copia en toda la lección 4.  
  
### Para crear el paquete de la lección 4  
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server** y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo**, haga clic en **Abrir**, haga clic en **Proyecto o solución**, seleccione **SSIS Tutorial**, haga clic en **Abrir** y, después, haga doble clic en **SSIS Tutorial.sln**.  
  
3.  En el Explorador de soluciones, haga clic con el botón derecho en **Lesson 3.dtsx** y, después, haga clic en **Copiar**.  
  
4.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS** y, después, haga clic en **Pegar**.  
  
    De forma predeterminada, el paquete copiado se denomina Lesson 4.dtsx.  
  
5.  En el Explorador de soluciones, haga doble clic en **Lesson 4.dtsx** para abrir el paquete.  
  
6.  Haga clic con el botón derecho en cualquier parte del fondo de la pestaña **Flujo de control** y haga clic en **Propiedades**.  
  
7.  En la ventana Propiedades, actualice la propiedad **Name** a **Lesson 4**.  
  
8.  Haga clic en el cuadro para la propiedad **ID** y, en la lista, haga clic en **<Generate New ID>**.  
  
### Para agregar el paquete de la lección 3 completada  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y abra el proyecto SSIS Tutorial.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS** y haga clic en **Agregar paquete existente**.  
  
3.  En el cuadro de diálogo **Agregar copia de paquete existente**, en **Ubicación del paquete**, seleccione **Sistema de archivos**.  
  
4.  Haga clic en el botón para examinar **(…)**, vaya a Lesson 3.dtsx en la máquina y, después, haga clic en **Abrir**.  
  
    Para descargar todos los paquetes de lecciones de este tutorial, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie y pegue el paquete de la lección 3 tal como se describe en los pasos del 3 a 8 del procedimiento anterior.  
  
## Siguiente tarea de la lección  
[Paso 2: Crear un archivo dañado](../integration-services/step-2-creating-a-corrupted-file.md)  
  
