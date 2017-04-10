---
title: "Agregar sangr&#237;a | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Agregar sangr&#237;a
El Editor de consultas permite aplicar sangría a grandes secciones de código en un solo paso y cambiar la extensión de la sangría.  
  
## Aplicar sangría a líneas de código  
  
#### Para aplicar sangría a varias líneas de código  
  
1.  En la barra de herramientas, haga clic en **Nueva consulta**.  
  
2.  Cree una segunda consulta que seleccione las columnas **BusinessEntityID**, FirstName, **MiddleName**y **LastName** de la tabla **Person** del esquema **Person** . Coloque cada columna en una línea separada de manera que el código tenga el aspecto siguiente:  
  
    ```  
    -- Search for a contact  
    SELECT   
    BusinessEntityID,  
    FirstName,   
    MiddleName,   
    LastName  
    FROM Person.Person  
    WHERE LastName = 'Sanchez';  
    GO  
    ```  
  
3.  Seleccione todo el texto desde `BusinessEntityID` hasta `LastName`.  
  
4.  En la barra de herramientas del **Editor SQL** , haga clic en **Aumentar sangría** para aplicar la sangría a todas las líneas al mismo tiempo.  
  
#### Para cambiar la sangría predeterminada  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Expanda **Editor de texto**, **Todos los lenguajes**, haga clic en **Pestañas** y configure los valores de sangría apropiados. Observe que puede cambiar tanto el tamaño de la sangría como el de las pestañas y especificar si éstas deben cambiarse por espacios.  
  
    ![Apariencia del cuadro de diálogo Pestañas](../../tools/sql-server-management-studio/media/tabsdialog.gif "Apariencia del cuadro de diálogo Pestañas")  
  
3.  Haga clic en **Aceptar**.  
  
## Siguiente tarea de la lección  
[Maximizar el Editor de consultas](../../tools/sql-server-management-studio/maximizing-query-editor.md)  
  
  
  
