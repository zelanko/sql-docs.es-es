---
title: "Customize the Parameters Pane in a Report (Report Builder) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ce9e8d5-911a-4422-928f-a8d005b79fc6
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Customize the Parameters Pane in a Report (Report Builder)
  Al crear informes paginados con parámetros en el Generador de informes, puede personalizar el panel de parámetros. En la vista de diseño de informe, puede arrastrar un parámetro a una columna y fila específicas del panel de parámetros. Puede agregar y quitar columnas para cambiar el diseño del panel.  
  
 Al arrastrar un parámetro a una columna y fila nuevas del panel, el orden de los parámetros cambiará en el panel **Datos de informe**. Al cambiar el orden de los parámetros en el panel **Datos de informe**, cambia la ubicación de los parámetros en el panel. Para más información sobre por qué es importante el orden de los parámetros, vea [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md).  
  
## Para personalizar el panel de parámetros  
  
1.  En la pestaña **Vista** , seleccione la casilla **Parámetros** para mostrar el panel de parámetros.  
  
     ![Access parameters pane from View tab](../../reporting-services/report-design/media/ssrs-customparameter-accessparameterpanedesignmode.png "Access parameters pane from View tab")  
  
     El panel aparece en la parte superior de la superficie de diseño.  
  
2.  Para agregar un parámetro al panel, siga unos de los siguientes procedimientos.  
  
    -   Haga clic con el botón derecho en una celda vacía del panel de parámetros y después haga clic en **Agregar parámetro**.  
  
         ![Add new parameter from parameters pane](../../reporting-services/report-design/media/ssrs-customizeparameter-addnewparameter.png "Add new parameter from parameters pane")  
  
    -   Haga clic con el botón derecho en **Parámetros** , en el panel **Datos de informe** y después haga clic en **Agregar parámetro**.  
  
3.  Para mover un parámetro a una ubicación nueva del panel de parámetros, arrastre el parámetro a una celda diferente del panel.  
  
     Cuando cambia la ubicación del parámetro en el panel, el orden del parámetro en la lista **Parámetros** del panel **Datos de informe** se cambia automáticamente. Para más información sobre el impacto del orden de los parámetros, vea [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md).  
  
4.  Para acceder a las propiedades de un parámetro, siga unos de los siguientes procedimientos.  
  
    -   Haga clic con el botón derecho en el parámetro del panel de parámetros y después haga clic en **Propiedades del parámetro**.  
  
         ![Access parameter properties from the parameters pane](../../reporting-services/report-design/media/ssrs-customizeparameter-accessparameterproperties-composite.png "Access parameter properties from the parameters pane")  
  
    -   Haga clic con el botón derecho en el parámetro del panel **Datos de informe** y después haga clic en **Propiedades del parámetro**.  
  
5.  Para agregar columnas y filas nuevas al panel, o eliminar columnas y filas existentes, haga clic con el botón derecho en cualquier lugar del panel de parámetros y después haga clic en un comando del menú que aparece.  
  
     ![Add columns and rows to the parameters pane](../../reporting-services/report-design/media/ssrs-customparameter-addcolumnsrows.png "Add columns and rows to the parameters pane")  
  
    > [!IMPORTANT]  
    >  Al eliminar una columna o fila que contiene parámetros, estos se eliminan del informe.  
  
6.  Para eliminar un parámetro del panel y del informe, siga uno de los siguientes procedimientos.  
  
    -   Haga clic con el botón derecho en el parámetro del panel de parámetros y después haga clic en  **Eliminar**.  
  
         ![Delete parameters from the parameters pane](../../reporting-services/report-design/media/ssrs-customparameter-deleteparameter.png "Delete parameters from the parameters pane")  
  
    -   Haga clic con el botón derecho en el panel **Datos de informe** y después haga clic en **Eliminar**.  
  
## Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  