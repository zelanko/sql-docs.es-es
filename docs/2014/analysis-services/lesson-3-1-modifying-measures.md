---
title: Modificar medidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 663ef21dc9c4d0f3698ae468637fe0a8fd55a16e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078898"
---
# <a name="modifying-measures"></a>Modificar medidas
  Puede usar la propiedad **FormatString** para definir parámetros de formato que controlen cómo se presentan las medidas a los usuarios. En esta tarea, debe especificar las propiedades de formato para las medidas de moneda y porcentaje del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
### <a name="to-modify-the-measures-of-the-cube"></a>Para modificar las medidas del cubo  
  
1.  Pase a la pestaña **Estructura de cubo** del Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , expanda el grupo de medida **Internet Sales** del panel **Medidas** , haga clic con el botón secundario en **Order Quantity**y haga clic en **Propiedades**.  
  
2.  En la ventana Propiedades, haga clic en el icono de chincheta **Ocultar automáticamente** para anclar la ventana Propiedades y dejarla abierta.  
  
     Es más fácil cambiar las propiedades para varios elementos del cubo cuando la ventana Propiedades permanece abierta.  
  
3.  En la ventana Propiedades, haga clic en la lista **FormatString** y escriba **#,#** .  
  
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
  
7.  En la lista desplegable de la parte superior de la ventana Propiedades (justo debajo de la barra de título), seleccione la medida **Unit Price Discount Pct**y, después, seleccione **Porcentaje** en la lista **FormatString** .  
  
8.  En la ventana Propiedades, cambie la **nombre** propiedad para el **Unit Price Discount Pct** medir con `Unit Price Discount Percentage`.  
  
9. En el **medidas** panel, haga clic en **Tax Amt** y cambie el nombre de esta medida a `Tax Amount`.  
  
10. En la ventana Propiedades, haga clic en el icono **Ocultar automáticamente** para ocultar la ventana Propiedades y, a continuación, haga clic en **Mostrar el árbol de medidas** en la barra de herramientas de la pestaña **Estructura de cubo** .  
  
11. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar la dimensión Customer](lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>Vea también  
 [Definir dimensiones de base de datos](multidimensional-models/define-database-dimensions.md)   
 [Configurar propiedades de medidas](multidimensional-models/configure-measure-properties.md)  
  
  
