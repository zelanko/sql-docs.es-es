---
title: Modificar medidas | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 00b1110e3deba08207cda1c71c75d6603660c019
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-3-1---modifying-measures"></a>Lección 1 de 3: modificar medidas
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]Puede usar el **FormatString** propiedad para definir parámetros de formato que controlan cómo se presentan las medidas a los usuarios. En esta tarea, debe especificar las propiedades de formato para las medidas de moneda y porcentaje del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
### <a name="to-modify-the-measures-of-the-cube"></a>Para modificar las medidas del cubo  
  
1.  Pase a la pestaña **Estructura de cubo** del Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , expanda el grupo de medida **Internet Sales** del panel **Medidas** , haga clic con el botón secundario en **Order Quantity**y haga clic en **Propiedades**.  
  
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
  
7.  En la lista desplegable de la parte superior de la ventana Propiedades (justo debajo de la barra de título), seleccione la medida **Unit Price Discount Pct**y, después, seleccione **Porcentaje** en la lista **FormatString** .  
  
8.  En la ventana Propiedades, cambie la propiedad **Name** de la medida **Unit Price Discount Pct** por **Unit Price Discount Percentage**.  
  
9. En el panel **Medidas** , haga clic en **Tax Amt** y cambie el nombre de esta medida a **Importe de impuesto**.  
  
10. En la ventana Propiedades, haga clic en el icono **Ocultar automáticamente** para ocultar la ventana Propiedades y, a continuación, haga clic en **Mostrar el árbol de medidas** en la barra de herramientas de la pestaña **Estructura de cubo** .  
  
11. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Modificar la dimensión Customer](../analysis-services/lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>Ver también  
[Definir dimensiones de base de datos](../analysis-services/multidimensional-models/define-database-dimensions.md)  
[Configurar propiedades de medidas](../analysis-services/multidimensional-models/configure-measure-properties.md)  
  
  
  
