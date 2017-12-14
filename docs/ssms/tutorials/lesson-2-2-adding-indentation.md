---
title: "Agregar sangría | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 21b8fbca046e733afd062b07e5316694cb0adc76
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-2-2---adding-indentation"></a>Lección 2.2: Agregar sangría
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] El Editor de consultas permite aplicar sangría a grandes secciones de código en un solo paso y cambiar la extensión de la sangría.  
  
## <a name="indenting-code"></a>Aplicar sangría a líneas de código  
  
#### <a name="to-indent-multiple-lines-of-code"></a>Para aplicar sangría a varias líneas de código  
  
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
  
#### <a name="to-change-the-default-indentation"></a>Para cambiar la sangría predeterminada  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Expanda **Editor de texto**, **Todos los lenguajes**, haga clic en **Pestañas** y configure los valores de sangría apropiados. Observe que puede cambiar tanto el tamaño de la sangría como el de las pestañas y especificar si éstas deben cambiarse por espacios.  
  
    ![Apariencia del cuadro de diálogo Pestañas](./media/lesson-2-2-adding-indentation/tabsdialog.gif "Apariencia del cuadro de diálogo Pestañas")  
  
3.  Haga clic en **Aceptar**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Maximizar el Editor de consultas](../../tools/sql-server-management-studio/lesson-2-3-maximizing-query-editor.md)  
  
  
  
