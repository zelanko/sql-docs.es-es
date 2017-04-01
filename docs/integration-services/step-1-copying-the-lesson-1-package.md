---
title: "Paso 1: Copiar el paquete de la lecci&#243;n 1 | Microsoft Docs"
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
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Paso 1: Copiar el paquete de la lecci&#243;n 1
En esta tarea, creará una copia del paquete que ha creado en la lección 1, denominado Lesson 1.dtsx. Si no ha completado la lección 1, puede agregar al proyecto el paquete completado de la lección 1 que se incluye con el tutorial y, después, copiar dicho paquete. Usará esta nueva copia en toda la lección 2.  
  
### Para crear el paquete de la lección 2  
  
1.  Si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools no está abierto, haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server 2012** y, después, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo**, haga clic en **Abrir** y en **Proyecto o solución**, haga clic en la carpeta **SSIS Tutorial**, haga clic en **Abrir** y, después, haga doble clic en **SSIS Tutorial.sln**.  
  
3.  En el Explorador de soluciones, haga clic con el botón derecho en **Lesson 1.dtsx** y luego haga clic en **Copiar**.  
  
4.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS** y, después, haga clic en **Pegar**.  
  
    De forma predeterminada, el paquete copiado se denominará Lesson 2.dtsx.  
  
5.  En el Explorador de soluciones, haga doble clic en **Lesson 2.dtsx** para abrir el paquete  
  
6.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de **Flujo de control** y haga clic en **Propiedades**.  
  
7.  En la ventana Propiedades, actualice la propiedad **Nombre** a **Lesson 2**.  
  
8.  Haga clic en el cuadro de la propiedad **Id.**, haga clic en la flecha desplegable y luego haga clic en **<Generate New ID>**.  
  
### Para agregar el paquete de la lección 1 completada  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools y el proyecto SSIS Tutorial.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en **Paquetes SSIS** y haga clic en **Agregar paquete existente**.  
  
3.  En el cuadro de diálogo **Agregar copia de paquete existente**, en **Ubicación del paquete**, seleccione **Sistema de archivos**.  
  
4.  Haga clic en el botón Examinar **(…)**, vaya a **Lesson 1.dtsx** en el equipo y, después, haga clic en **Abrir**.  
  
    Para descargar todos los paquetes de lecciones de este tutorial, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie y pegue el paquete de la lección 1 tal como se describe en los pasos 3 a 8 del procedimiento anterior.  
  
## Siguiente tarea de la lección  
[Paso 2: agregar y configurar el contenedor de bucles Foreach](../integration-services/step-2-adding-and-configuring-the-foreach-loop-container.md)  
  
