---
title: Agregar un atributo a una dimensión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25bbd679cd27aafd2fb71986aac1991556b3c890
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237765"
---
# <a name="add-an--attribute-to-a-dimension"></a>Incorporación de un atributo a una dimensión
  Puede agregar un atributo a una dimensión automática o manualmente en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para crear un atributo automáticamente, en la pestaña **Estructura de dimensión** del Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione la columna que desea asignar a un atributo y, a continuación, arrastre dicha columna desde el panel **Vista del origen de datos** al panel **Atributos** . De esta forma se crea un atributo que se asigna a la columna, y asigna el mismo nombre al atributo que el nombre de la columna. Si un atributo que utiliza dicho nombre ya existe, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agregará un sufijo de número ordinal que empiece por "1" para el primer nombre duplicado.  
  
 Para crear un atributo manualmente, establezca el panel **Atributos** en la vista de cuadrícula. En la columna de nombre de la última fila de la cuadrícula, haga clic en el  **\<nuevo atributo >** elemento. Escriba un nombre para el nuevo atributo. De esta forma se crea un atributo que no se relaciona con una columna y que tiene la configuración predeterminada para todas sus propiedades. Puede establecer la correlación en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] configurando la propiedad **KeyColumns** para el nuevo atributo.  
  
 Para obtener más información, vea [Definir un nuevo atributo automáticamente](attribute-properties-define-a-new-attribute-automatically.md), [Definir un nuevo atributo manualmente](../define-a-new-attribute-manually.md), [Enlazar un atributo a una columna de nombre](attribute-properties-bind-an-attribute-to-a-name-column.md)y [Modificar la propiedad KeyColumns de un atributo](attribute-properties-modify-the-keycolumn-property.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de las propiedades de los atributos de dimensión](dimension-attribute-properties-reference.md)  
  
  
