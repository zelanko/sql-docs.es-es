---
title: Agregar un atributo a una dimensión | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 02773eadf282fe9ac25fa96543a86c5d3e77da4c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020613"
---
# <a name="attribute-properties---add-an--attribute-to-a-dimension"></a>Propiedades de atributos: Agregar un atributo a una dimensión
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede agregar un atributo a una dimensión automática o manualmente en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para crear un atributo automáticamente, en la pestaña **Estructura de dimensión** del Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione la columna que desea asignar a un atributo y, a continuación, arrastre dicha columna desde el panel **Vista del origen de datos** al panel **Atributos** . De esta forma se crea un atributo que se asigna a la columna, y asigna el mismo nombre al atributo que el nombre de la columna. Si un atributo que utiliza dicho nombre ya existe, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agregará un sufijo de número ordinal que empiece por "1" para el primer nombre duplicado.  
  
 Para crear un atributo manualmente, establezca el panel **Atributos** en la vista de cuadrícula. En la columna de nombre de la última fila de la cuadrícula, haga clic en el  **\<nuevo atributo >** elemento. Escriba un nombre para el nuevo atributo. De esta forma se crea un atributo que no se relaciona con una columna y que tiene la configuración predeterminada para todas sus propiedades. Puede establecer la correlación en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] configurando la propiedad **KeyColumns** para el nuevo atributo.  
  
 Para obtener más información, vea [Definir un nuevo atributo automáticamente](../../analysis-services/multidimensional-models/attribute-properties-define-a-new-attribute-automatically.md), [Enlazar un atributo a una columna de nombre](../../analysis-services/multidimensional-models/attribute-properties-bind-an-attribute-to-a-name-column.md)y [Modificar la propiedad KeyColumns de un atributo](../../analysis-services/multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
