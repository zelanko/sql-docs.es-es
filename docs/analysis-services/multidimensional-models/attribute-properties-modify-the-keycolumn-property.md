---
title: Modificar la propiedad KeyColumns de un atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4415c5dba3382e636488ac94408f163c8e54dc6f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539029"
---
# <a name="attribute-properties---modify-the-keycolumn-property"></a>Propiedades de atributos: Modificar la propiedad KeyColumns
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede modificar la propiedad **KeyColumns** de un atributo. Por ejemplo, es posible que desee especificar una clave compuesta en lugar de una sola clave como clave del atributo.  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>Para modificar la propiedad KeyColumns de un atributo  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto cuya propiedad **KeyColumns** quiera modificar.  
  
2.  Abra el Diseñador de dimensiones siguiendo uno de estos procedimientos:  
  
    -   En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Dimensiones** y, después, haga clic en **Abrir** o en **Diseñador de vistas**.  
  
         -o bien-  
  
    -   En el Diseñador de cubos, en el **estructura de cubo** , expanda la dimensión de cubo en el **dimensiones** panel y haga clic en **editar \<dimensión >**.  
  
3.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , haga clic en el atributo cuya propiedad **KeyColumns** desee modificar.  
  
4.  En la ventana **Propiedades** , haga clic en el valor de la propiedad **KeyColumns** .  
  
5.  Haga clic en el botón Examinar **(…)** que aparece en la celda de valor del cuadro de propiedades.  
  
     Se abre el cuadro de diálogo **Columnas de clave** .  
  
6.  Para quitar una columna de clave existente, en la lista **Columnas de clave** , seleccione la columna y, después, haga clic en el botón **\<** .  
  
7.  Para agregar una columna de clave, en la lista **Columnas disponibles** , seleccione la columna y, después, haga clic en el botón **>** .  
  
    > [!NOTE]  
    >  Si define varias columnas de clave, el orden en el que esas columnas aparecen en la lista **Columnas de clave** afecta al orden de presentación. Por ejemplo, un atributo de mes tiene dos columnas de clave: mes y año. Si la columna de año aparece en la lista antes de la columna de mes, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ordenarán por año y a continuación por mes. Si la columna de mes aparece en la lista antes de la de año, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ordenarán por mes y a continuación por año.  
  
8.  Para cambiar el orden de las columnas de clave, seleccione una columna y, después, haga clic en el botón **Subir** o **Bajar** .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
