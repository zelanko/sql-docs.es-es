---
title: Herramientas de cálculo (pestaña KPI, diseñador de cubos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpisview.calculationtoolspane.f1
ms.assetid: c030c725-7763-4c23-9988-4b274a88fc31
author: minewiskan
ms.author: owend
ms.openlocfilehash: b26c912791a18d4bbdcf3def6d282e025b5af89b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527611"
---
# <a name="calculation-tools-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Herramientas de cálculo (pestaña KPI, Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Use el panel **Herramientas de cálculo** en la pestaña **KPI** del Diseñador de cubos para explorar metadatos, funciones y plantillas disponibles para usarlas en indicadores clave de rendimiento (KPI).  
  
> [!NOTE]  
>  Este panel solo se muestra en la vista de formulario.  
  
## <a name="options"></a>Opciones  
 **Metadata**  
 Muestra los metadatos del cubo seleccionado.  
  
 Arrastre el elemento seleccionado al panel **Editor de Formulario de KPI** para incluir la sintaxis de Expresiones multidimensionales (MDX) para dicho elemento en la ubicación seleccionada del panel.  
  
 **Funciones**  
 Muestra las funciones disponibles para las expresiones y condiciones.  
  
 Arrastre el elemento seleccionado al panel **Editor de Formulario de KPI** para incluir la sintaxis MDX para dicho elemento en la ubicación seleccionada del panel.  
  
> [!NOTE]  
>  En el modo de proyecto, el cuadro de diálogo **Herramientas de cálculo** lee la información de esta opción desde un archivo XML con el nombre MDXFunctions.xml, incluido en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. En el modo en línea, la información de esta opción se recupera del conjunto de filas del esquema MDSCHEMA_FUNCTIONS para la instancia.  
  
 **Templates** (Plantillas [C++])  
 Muestra las plantillas predeterminadas disponibles para los KPI.  
  
 Arrastre el elemento seleccionado al panel **Editor de Formulario de KPI** para incluir la sintaxis MDX para dicho elemento en la ubicación seleccionada del panel.  
  
## <a name="context-menu"></a>Menú contextual  
 Las siguientes opciones están disponibles en el menú contextual que se muestra al hacer clic con el botón derecho en un elemento del panel **Herramientas de cálculo** :  
  
 **Copiar**  
 Seleccione esta opción para copiar el elemento seleccionado en **Metadatos** o **Funciones** en el Portapapeles.  
  
> [!NOTE]  
>   No se mostrará esta opción si se selecciona **Plantillas** .  
  
> [!NOTE]  
>   Se deshabilitará esta opción si no es posible copiar el miembro seleccionado, al igual que la carpeta **Conjuntos** de una dimensión mostrada en **Metadatos** o la carpeta del grupo de función para una función mostrada en **Funciones**.  
  
 **Filtrar miembros**  
 Seleccione esta opción para mostrar el cuadro de diálogo **Filtrar miembros** y filtrar los miembros del elemento seleccionado en **Metadatos**. Para más información sobre el cuadro de diálogo **Filtrar miembros**, vea [Cuadro de diálogo Filtrar miembros &#40;Analysis Services - Datos multidimensionales&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>   Solo se mostrará esta opción si se selecciona **Metadatos** .  
  
> [!NOTE]  
>   Solo se habilitará esta opción si se selecciona un nivel para un atributo en **Metadatos**.  
  
 **Agregar plantilla**  
 Seleccione esta opción para agregar un nuevo miembro calculado, un conjunto con nombre o un comando de un script en la plantilla seleccionada al script del cubo y mostrar el **Editor de Formulario de KPI** en la vista de formulario.  
  
> [!NOTE]  
>   Solo se mostrará esta opción si se selecciona **Metadatos** .  
  
## <a name="see-also"></a>Consulte también  
 [Diseñador de cubos &#40;Analysis Services de datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [KPI &#40;diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña KPI, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](toolbar-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de KPI &#40;pestaña KPI, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](kpi-organizer-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulario de KPI &#40;pestaña KPI, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](kpi-form-editor-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Explorador de KPI &#40;pestaña KPI, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](kpi-browser-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
