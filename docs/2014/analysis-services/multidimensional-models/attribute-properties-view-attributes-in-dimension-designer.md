---
title: Ver atributos en el Diseñador de dimensiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec86d5e7a910b7fb17397b1601fcc912b46c4d7f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077128"
---
# <a name="view-attributes-in-dimension-designer"></a>Ver atributos en el Diseñador de dimensiones
  Los atributos se crean en objetos de dimensión. Para ver y configurar atributos, use el Diseñador de dimensiones en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El panel **Atributos** de la pestaña **Estructura de dimensión** del Diseñador de dimensiones contiene los atributos presentes en una dimensión. Use este panel para agregar, quitar o configurar atributos. También puede seleccionar atributos para usarlos como un nivel en una jerarquía nueva o para agregarlos como un nivel a una jerarquía existente.  
  
 Para ver los atributos de una dimensión, abra el Diseñador de dimensiones para la dimensión. En el panel **Atributos** de la pestaña **Estructura de dimensión**  del diseñador se muestran los atributos presentes en la dimensión. Puede cambiar entre una vista de lista, árbol o una cuadrícula, seleccione **Mostrar atributos en** en el **dimensión** menú de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y, a continuación, haga clic en uno de los comandos que se muestra en la tabla siguiente.  
  
|Mostrar atributos en|Descripción|  
|------------------------|-----------------|  
|**Lista**|Muestra los atributos con formato de lista.<br /><br /> Haga clic con el botón secundario en un atributo para eliminarlo de la lista, para cambiar su nombre o para cambiar su uso.<br /><br /> Use esta vista para crear jerarquías. La información del atributo y las propiedades de miembro no están visibles.|  
|**Árbol**|Muestra los atributos con formato de árbol, con la dimensión como nodo de nivel superior del árbol. Use esta vista para ver y crear propiedades de miembros. También puede utilizarla para generar jerarquías. Expanda un atributo para ver las relaciones de atributo correspondientes o para crear una nueva relación de atributo, efectuando las siguientes acciones:<br /><br /> Haga clic en la dimensión, un atributo o una propiedad del miembro para ver sus propiedades en la ventana **Propiedades** .<br /><br /> Haga clic con el botón secundario en un atributo o una propiedad del miembro para eliminarlo de la lista, para cambiar su nombre o para cambiar su uso.|  
|**Grid**|Muestra los atributos con formato de cuadrícula. Haga clic en una fila de la cuadrícula para ver las propiedades correspondientes a ese atributo.  Use esta vista para crear y configurar atributos. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre**: muestra el valor de la **nombre** propiedad. Escriba otro nombre para cambiar la configuración.<br /><br /> **Uso**: Especifica si se trata de un atributo Regular, Key, primario o AccountType. Haga clic en un valor de la columna para seleccionar otra opción.<br /><br /> **Tipo**: especifica la categoría de business intelligence para el atributo. Haga clic en esta celda para seleccionar otra opción.<br /><br /> **Columna de clave**: muestra el tipo de datos OLE DB para la **KeyColumn** propiedad del atributo. Esta columna no puede modificarse.<br /><br /> **Columna de nombre**: indica si el **NameColumn** configuración de la propiedad en el atributo es la misma columna que el valor para el **KeyColumn** propiedad. Esta columna no puede modificarse.|  
  
 En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], los iconos que aparecen en la tabla siguiente marcan los atributos según su uso.  
  
|Icono|Uso del atributo|  
|----------|---------------------|  
|![Icono atributo](../media/as-icon-attribute.gif "icono de atributo")|Regular o AccountType|  
|![Icono de atributo clave](../media/as-icon-key-attribute.gif "icono de atributo clave")|Key|  
|![Icono de atributo primario](../media/as-icon-parent-attribute.gif "icono de atributo primario")|Parent|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de las propiedades de los atributos de dimensión](dimension-attribute-properties-reference.md)  
  
  
