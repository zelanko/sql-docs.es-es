---
title: "Modificar medidas | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Modificar medidas
Puede usar la propiedad **FormatString** para definir parámetros de formato que controlen cómo se presentan las medidas a los usuarios. En esta tarea, debe especificar las propiedades de formato para las medidas de moneda y porcentaje del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
### Para modificar las medidas del cubo  
  
1.  Pase a la pestaña **Estructura de cubo[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] del Diseñador de cubos para el cubo Tutorial de **, expanda el grupo de medida **Venta por Internet** del panel **Medidas**, haga clic con el botón derecho en **Cantidad de pedido** y haga clic en **Propiedades**.  
  
2.  En la ventana Propiedades, haga clic en el icono de chincheta **Ocultar automáticamente** para anclar la ventana Propiedades y dejarla abierta.  
  
    Es más fácil cambiar las propiedades para varios elementos del cubo cuando la ventana Propiedades permanece abierta.  
  
3.  En la ventana Propiedades, haga clic en la lista **FormatString** y escriba **#,#**.  
  
4.  En la barra de herramientas de la pestaña **Estructura de cubo** , haga clic en el icono **Mostrar la cuadrícula de medidas** situado a la izquierda.  
  
    La vista de cuadrícula permite seleccionar varias medidas al mismo tiempo.  
  
5.  Seleccione una de las medidas siguientes. Para seleccionar varias medidas, haga clic en cada una de ellas mientras mantiene presionada la tecla CTRL:  
  
    -   **Unit Price**  
  
    -   **Extended Amount**  
  
    -   **Discount Amount**  
  
    -   **Product Standard Cost**  
  
    -   **Total Product Cost**  
  
    -   **Sales Amount**  
  
    -   **Tax Amt**  
  
    -   **Freight**  
  
6.  En la ventana Propiedades, en la lista **FormatString** , seleccione **Currency**.  
  
7.  En la lista desplegable de la parte superior de la ventana Propiedades (justo debajo de la barra de título), seleccione la medida **Unit Price Discount Pct** y, después, seleccione **Porcentaje** en la lista **FormatString**.  
  
8.  En la ventana Propiedades, cambie la propiedad **Name** de la medida **Unit Price Discount Pct** por **Unit Price Discount Percentage**.  
  
9. En el panel **Medidas** , haga clic en **Tax Amt** y cambie el nombre de esta medida a **Importe de impuesto**.  
  
10. En la ventana Propiedades, haga clic en el icono **Ocultar automáticamente** para ocultar la ventana Propiedades y, a continuación, haga clic en **Mostrar el árbol de medidas** en la barra de herramientas de la pestaña **Estructura de cubo** .  
  
11. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## Siguiente tarea de la lección  
[Modificar la dimensión Customer](../analysis-services/modifying-the-customer-dimension.md)  
  
## Vea también  
[Definir dimensiones de base de datos](../analysis-services/multidimensional-models/define-database-dimensions.md)  
[Configurar propiedades de medidas](../analysis-services/multidimensional-models/configure-measure-properties.md)  
  
  
  
