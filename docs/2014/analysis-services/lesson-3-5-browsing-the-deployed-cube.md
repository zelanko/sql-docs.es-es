---
title: Examinar el cubo implementado | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 849c6109-1453-4fe4-a892-c49a982cfadb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d958fa21380272aa770a9880e294a86fede29de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "69493984"
---
# <a name="browsing-the-deployed-cube"></a>Examinar el cubo implementado
  En la tarea siguiente, examinará el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Puesto que nuestro análisis compara las medidas en varias dimensiones, usará una tabla dinámica de Excel para examinar los datos. El uso de una tabla dinámica le permite colocar la información de clientes, fechas y productos en diferentes ejes de modo que pueda ver cómo cambian las ventas por Internet cuando se ven en determinados períodos de tiempo, datos demográficos de los clientes y líneas de productos.  
  
### <a name="to-browse-the-deployed-cube"></a>Para examinar el cubo implementado  
  
1.  Para cambiar al diseñador de cubos de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga doble clic en el ** [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo tutorial** de en la carpeta **cubos** del explorador de soluciones.  
  
2.  Abra la pestaña **Explorador** y haga clic en el botón **Volver a conectar** de la barra de herramientas del diseñador.  
  
3.  Haga clic en el icono de Excel para iniciar Excel usando la base de datos del área de trabajo como origen de datos. Cuando se le pida que habilite las conexiones, haga clic en **Habilitar**.  
  
4.  En la lista de campos de la tabla dinámica, expanda **Internet Sales**y arrastre la medida **Sales Amount** hasta el área **Valores** .  
  
5.  En la lista de campos de la tabla dinámica, expanda **Product**.  
  
6.  Arrastre la jerarquía de usuario **Product Model Lines** hasta el área **Columnas** .  
  
7.  En la lista de campos de la tabla dinámica, expanda **Customer**, expanda **Location**y arrastre la jerarquía **Customer Geography** desde la carpeta para mostrar Location de la dimensión Customer hasta el área **Filas** .  
  
8.  En la lista de campos de la tabla dinámica, expanda **Order Date**y arrastre la jerarquía **Order Date.Calendar Date** hasta el área **Filtro de informe** .  
  
9. Haga clic en la flecha que se encuentra a la derecha del filtro **Order Date.Calendar Date** del panel de datos, desactive la casilla del nivel **(All)** , expanda sucesivamente **2006**, **H1 CY 2006**y **Q1 CY 2006**, active la casilla **February 2006**y, después, haga clic en **Aceptar**.  
  
     De este modo, se muestran las ventas realizadas por Internet por región y por línea de productos en el mes de febrero de 2006, como se muestra en la imagen siguiente.  
  
     ![Internet Sales por línea de productos y región](../../2014/tutorials/media/l3-cube-browser-finish.gif "Internet Sales por línea de productos y región")  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Definir propiedades de dimensiones y de atributos avanzados](lesson-4-defining-advanced-attribute-and-dimension-properties.md)  
  
  
