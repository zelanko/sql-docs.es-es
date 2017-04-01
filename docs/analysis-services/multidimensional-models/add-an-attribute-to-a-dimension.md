---
title: "Incorporaci&#243;n de un atributo a una dimensi&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "agregar atributos"
  - "creación automática de atributos"
  - "atributos [Analysis Services], crear"
  - "atributos [Analysis Services], agregar"
  - "creación manual de atributos [Analysis Services]"
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Incorporaci&#243;n de un atributo a una dimensi&#243;n
  Puede agregar un atributo a una dimensión automática o manualmente en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para crear un atributo automáticamente, en la pestaña **Estructura de dimensión** del Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione la columna que desea asignar a un atributo y, a continuación, arrastre dicha columna desde el panel **Vista del origen de datos** al panel **Atributos** . De esta forma se crea un atributo que se asigna a la columna, y asigna el mismo nombre al atributo que el nombre de la columna. Si un atributo que utiliza dicho nombre ya existe, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agregará un sufijo de número ordinal que empiece por "1" para el primer nombre duplicado.  
  
 Para crear un atributo manualmente, establezca el panel **Atributos** en la vista de cuadrícula. En la columna de nombre de la última fila de la cuadrícula, haga clic en el elemento **\<nuevo atributo>**. Escriba un nombre para el nuevo atributo. De esta forma se crea un atributo que no se relaciona con una columna y que tiene la configuración predeterminada para todas sus propiedades. Puede establecer la correlación en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] configurando la propiedad **KeyColumns** para el nuevo atributo.  
  
 Para obtener más información, vea [Definir un nuevo atributo automáticamente](../../analysis-services/multidimensional-models/define-a-new-attribute-automatically.md), [Definir un nuevo atributo manualmente](../Topic/Define%20a%20New%20Attribute%20Manually.md), [Enlazar un atributo a una columna de nombre](../../analysis-services/multidimensional-models/bind-an-attribute-to-a-name-column.md) y [Modificar la propiedad KeyColumns de un atributo](../../analysis-services/multidimensional-models/modify-the-keycolumn-property-of-an-attribute.md).  
  
## Vea también  
 [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  