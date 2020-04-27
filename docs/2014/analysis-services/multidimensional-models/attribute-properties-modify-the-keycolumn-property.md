---
title: Modifique la propiedad KeyColumn de un atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c5effed34dda946d3c65028aa5834f4fbddf7cd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077248"
---
# <a name="modify-the-keycolumn-property-of-an-attribute"></a>Modificar la propiedad KeyColumns de un atributo
  Puede modificar la propiedad **KeyColumns** de un atributo. Por ejemplo, es posible que desee especificar una clave compuesta en lugar de una sola clave como clave del atributo.  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>Para modificar la propiedad KeyColumns de un atributo  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto cuya propiedad **KeyColumns** quiera modificar.  
  
2.  Abra el Diseñador de dimensiones siguiendo uno de estos procedimientos:  
  
    -   En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Dimensiones** y, después, haga clic en **Abrir** o en **Diseñador de vistas**.  
  
         o bien  
  
    -   En el diseñador de cubos, en la pestaña **estructura de cubo** , expanda la dimensión de cubo en el panel **dimensiones** y haga clic en ** \<editar>de dimensiones **.  
  
3.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , haga clic en el atributo cuya propiedad **KeyColumns** desee modificar.  
  
4.  En la ventana **Propiedades** , haga clic en el valor de la propiedad **KeyColumns** .  
  
5.  Haga clic en el botón Examinar **(…)** que aparece en la celda de valor del cuadro de propiedades.  
  
     Se abre el cuadro de diálogo **Columnas de clave** .  
  
6.  Para quitar una columna de clave existente, en la lista **Columnas de clave** , seleccione la columna y, después, haga clic en el botón **\<** .  
  
7.  Para agregar una columna de clave, en la lista **Columnas disponibles** , seleccione la columna y, después, haga clic en el botón **>** .  
  
    > [!NOTE]  
    >  Si define varias columnas de clave, el orden en el que esas columnas aparecen en la lista **Columnas de clave** afecta al orden de presentación. Por ejemplo, un atributo de mes tiene dos columnas de clave: mes y año. Si la columna de año aparece en la lista antes de la columna de mes, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ordenarán por año y a continuación por mes. Si la columna de mes aparece en la lista antes de la de año, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ordenarán por mes y a continuación por año.  
  
8.  Para cambiar el orden de las columnas de clave, seleccione una columna y, después, haga clic en el botón **Subir** o **Bajar** .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de las propiedades de los atributos de dimensión](dimension-attribute-properties-reference.md)  
  
  
