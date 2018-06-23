---
title: Ver atributos en el Diseñador de dimensiones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c78e76030fe216df9e610b0e1ab6e6f37a652b30
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107316"
---
# <a name="view-attributes-in-dimension-designer"></a>Ver atributos en el Diseñador de dimensiones
  Los atributos se crean en objetos de dimensión. Para ver y configurar atributos, use el Diseñador de dimensiones en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El panel **Atributos** de la pestaña **Estructura de dimensión** del Diseñador de dimensiones contiene los atributos presentes en una dimensión. Use este panel para agregar, quitar o configurar atributos. También puede seleccionar atributos para usarlos como un nivel en una jerarquía nueva o para agregarlos como un nivel a una jerarquía existente.  
  
 Para ver los atributos de una dimensión, abra el Diseñador de dimensiones para la dimensión. En el panel **Atributos** de la pestaña **Estructura de dimensión**  del diseñador se muestran los atributos presentes en la dimensión. Puede cambiar entre una vista de lista, árbol o una cuadrícula, seleccione **Mostrar atributos en** en el **dimensión** menú de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y, a continuación, haga clic en uno de los comandos que aparecen en la tabla siguiente.  
  
|Mostrar atributos en|Descripción|  
|------------------------|-----------------|  
|**Lista**|Muestra los atributos con formato de lista.<br /><br /> Haga clic con el botón secundario en un atributo para eliminarlo de la lista, para cambiar su nombre o para cambiar su uso.<br /><br /> Use esta vista para crear jerarquías. La información del atributo y las propiedades de miembro no están visibles.|  
|**Árbol**|Muestra los atributos con formato de árbol, con la dimensión como nodo de nivel superior del árbol. Use esta vista para ver y crear propiedades de miembros. También puede utilizarla para generar jerarquías. Expanda un atributo para ver las relaciones de atributo correspondientes o para crear una nueva relación de atributo, efectuando las siguientes acciones:<br /><br /> Haga clic en la dimensión, un atributo o una propiedad del miembro para ver sus propiedades en la ventana **Propiedades** .<br /><br /> Haga clic con el botón secundario en un atributo o una propiedad del miembro para eliminarlo de la lista, para cambiar su nombre o para cambiar su uso.|  
|**Cuadrícula**|Muestra los atributos con formato de cuadrícula. Haga clic en una fila de la cuadrícula para ver las propiedades correspondientes a ese atributo.  Use esta vista para crear y configurar atributos. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre**: muestra el valor de la **nombre** propiedad. Escriba otro nombre para cambiar la configuración.<br /><br /> **Uso**: Especifica si se trata de un atributo Regular, Key, primarios o AccountType. Haga clic en un valor de la columna para seleccionar otra opción.<br /><br /> **Tipo de**: especifica la categoría de business intelligence para el atributo. Haga clic en esta celda para seleccionar otra opción.<br /><br /> **Columna de clave**: muestra el tipo de datos de OLE DB para la **KeyColumn** propiedad del atributo. Esta columna no puede modificarse.<br /><br /> **Columna de nombre**: indica si la **NameColumn** configuración de la propiedad en el atributo es la misma columna que el valor para el **KeyColumn** propiedad. Esta columna no puede modificarse.|  
  
 En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], los iconos que aparecen en la tabla siguiente marcan los atributos según su uso.  
  
|Icono|Uso del atributo|  
|----------|---------------------|  
|![Icono de atributo](../media/as-icon-attribute.gif "icono de atributo")|Regular o AccountType|  
|![Icono de atributo clave](../media/as-icon-key-attribute.gif "icono de atributo clave")|Key|  
|![Icono de atributo primario](../media/as-icon-parent-attribute.gif "icono de atributo primario")|Parent|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de las propiedades de los atributos de dimensión](dimension-attribute-properties-reference.md)  
  
  