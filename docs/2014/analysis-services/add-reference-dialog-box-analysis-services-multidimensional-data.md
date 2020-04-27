---
title: Cuadro de diálogo Agregar referencia (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.addreference.f1
- sql12.asvs.bidevstudio.assembly.addassembly.f1
helpviewer_keywords:
- Add Reference dialog box
ms.assetid: 457958c4-6baa-474d-99a0-34c195ceba09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 541b7371cdc05ee316e9fb9de9f50affc4f14fc7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062859"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Agregar referencia (Analysis Services - Datos multidimensionales)
  Utilice el cuadro de diálogo **Agregar referencia** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para agregar una referencia a un ensamblado de [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework o a otro proyecto del proyecto de desarrollo. Para abrir el cuadro de diálogo **Agregar referencia** , haga clic con el botón derecho en la carpeta **Ensamblados** de un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el **Explorador de soluciones** y seleccione **Nueva referencia de ensamblado** en el menú contextual.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**.NET**|Seleccione esta pestaña para agregar una referencia a un componente registrado. Esta pestaña muestra una cuadrícula que contiene una lista de componentes .NET Framework registrados. Seleccione uno o varios elementos de la cuadrícula y, a continuación, haga clic en **Agregar** para agregar los componentes .NET seleccionados a **Proyectos y componentes seleccionados**. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre de componente**: nombre completo, o descriptivo, del componente. Seleccione el título para ordenar por nombre de componente.<br /><br /> **Versión**: el número de versión indicado del componente. Seleccione el título para ordenar por versión.<br /><br /> **Runtime**: versión de la .NET Framework en la que se basa el componente. Seleccione el título para ordenar por versión de tiempo de ejecución.<br /><br /> **Ruta de acceso**: nombre de archivo del componente y ruta de acceso donde se encuentra. Seleccione el título para ordenar por ruta de acceso.|  
|**Examinar**|Haga clic para examinar en el sistema de archivos los ensamblados que no aparecen en las pestañas **.NET** o **Reciente** . Esta pestaña muestra las siguientes opciones:<br /><br /> **Buscar en**: Seleccione una carpeta de esta lista desplegable. Al seleccionar una carpeta de la lista, aparece su contenido en el panel principal.<br /><br /> **Ir a la última carpeta visitada**: vuelve a **Buscar en** la ubicación anterior.<br /><br /> **Subir un nivel**: busca la siguiente carpeta superior en la jerarquía.<br /><br /> **Crear nueva carpeta**: Seleccione esta opción para crear una nueva carpeta secundaria bajo la carpeta seleccionada en **Buscar en**.<br /><br /> **Menú Ver**: Seleccione esta información para cambiar la vista de contenido en el panel principal.  Para obtener más información sobre las opciones del **menú Ver**, vea el tema de introducción a la visualización de archivos y carpetas en la documentación de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Están disponibles las siguientes opciones:<br />Miniaturas<br />Iconos<br />Iconos<br />List<br />Detalles<br /><br /> **Panel principal**: muestra el contenido de la carpeta seleccionada en **Buscar en**. Seleccione uno o varios elementos y, a continuación, haga clic en **Agregar** para agregar los archivos seleccionados a los **productos y componentes seleccionados**. Para obtener más información sobre las opciones y el menú contextual del panel principal, vea el tema dedicado a la introducción a la visualización de archivos y carpetas en la documentación de Windows.<br /><br /> **Nombre de archivo**: Utilice esta opción para filtrar los archivos y las carpetas que se muestran. Escriba un nombre completo o parte del mismo para filtrar. Puede usar el asterisco (\*) como carácter comodín. Escriba varios nombres de archivo (cada nombre de archivo debe ir entre comillas dobles (") y delimitado por un espacio) para seleccionar varios archivos. También puede seleccionar archivos revisados anteriormente si selecciona un nombre de archivo de la lista desplegable. Sugerencia: puede buscar servidores web y equipos de red escribiendo una dirección URL o una ruta de acceso de red en **nombre de archivo**. Por ejemplo, "http://mywebsite" muestra los archivos disponibles en la ubicación web "miSitioWeb" y "\\\miServidor\miRecursoCompartido" muestra los archivos disponibles en la ubicación "miRecursoCompartido" en "miServidor".<br /><br /> **Archivos de tipo**: Utilice esta opción para filtrar el contenido de la carpeta o el directorio seleccionado en **Buscar en** para un tipo de archivo determinado.|  
|**Recientes**|Muestra una lista de referencias de componentes agregadas recientemente a proyectos en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Seleccione uno o varios elementos de la cuadrícula y, a continuación, haga clic en **Agregar** para agregar los ensamblados de .NET Framework seleccionados a **Proyectos y componentes seleccionados**. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre de componente**: nombre completo, o descriptivo, del componente. Seleccione el título para ordenar por nombre de componente.<br /><br /> **Versión**: el número de versión indicado del componente. Seleccione el título para ordenar por versión.<br /><br /> **Runtime**: versión de la .NET Framework en la que se basa el componente. Seleccione el título para ordenar por versión de tiempo de ejecución.<br /><br /> **Ruta de acceso**: nombre de archivo del componente y ruta de acceso donde se encuentra. Seleccione el título para ordenar por ruta de acceso.|  
|**Add (Agregar)**|Haga clic para agregar un componente seleccionado en las pestañas **.NET**, **Examinar**o **Reciente** a **Proyectos y componentes seleccionados**.|  
|**Remove**|Haga clic para quitar un componente seleccionado en **Proyectos y componentes seleccionados**.|  
|**Proyectos y componentes seleccionados**|Muestra una lista de referencias de componentes que se agregarán al proyecto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Seleccione uno o varios elementos de la cuadrícula y, a continuación, haga clic en **Quitar** para quitar los componentes seleccionados de la cuadrícula. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre de componente**: nombre completo, o descriptivo, del componente. Seleccione el título para ordenar por nombre de componente.<br /><br /> **Versión**: el número de versión indicado del componente. Seleccione el título para ordenar por versión.<br /><br /> **Runtime**: versión de la .NET Framework en la que se basa el componente. Seleccione el título para ordenar por versión de tiempo de ejecución.<br /><br /> **Ruta de acceso**: nombre de archivo del componente y ruta de acceso donde se encuentra. Seleccione el título para ordenar por ruta de acceso.|  
  
## <a name="see-also"></a>Consulte también  
 [Analysis Services diseñadores y cuadros de diálogo &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Administración de ensamblados de modelos multidimensionales](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
