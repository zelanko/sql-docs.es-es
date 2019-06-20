---
title: Agregar cuadro de diálogo de referencia (Analysis Services - datos multidimensionales) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062859"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Agregar referencia (Analysis Services - Datos multidimensionales)
  Utilice el cuadro de diálogo **Agregar referencia** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para agregar una referencia a un ensamblado de [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework o a otro proyecto del proyecto de desarrollo. Para abrir el cuadro de diálogo **Agregar referencia**, haga clic con el botón derecho en la carpeta **Ensamblados** de un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el **Explorador de soluciones** y seleccione **Nueva referencia de ensamblado** en el menú contextual.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**.NET**|Seleccione esta pestaña para agregar una referencia a un componente registrado. Esta pestaña muestra una cuadrícula que contiene una lista de componentes .NET Framework registrados. Seleccione uno o varios elementos de la cuadrícula y, a continuación, haga clic en **Agregar** para agregar los componentes .NET seleccionados a **Proyectos y componentes seleccionados**. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre de componente**: Nombre completo, o descriptivo, del componente. Seleccione el título para ordenar por nombre de componente.<br /><br /> **Versión**: Número de versión indicado del componente. Seleccione el título para ordenar por versión.<br /><br /> **Tiempo de ejecución**: Versión de .NET Framework en que se basa el componente. Seleccione el título para ordenar por versión de tiempo de ejecución.<br /><br /> **Ruta de acceso**: Nombre de archivo del componente y ruta de acceso donde se encuentra. Seleccione el título para ordenar por ruta de acceso.|  
|**Examinar**|Haga clic para examinar en el sistema de archivos los ensamblados que no aparecen en las pestañas **.NET** o **Reciente** . Esta pestaña muestra las siguientes opciones:<br /><br /> **Buscar en**: Seleccione una carpeta de la lista desplegable. Al seleccionar una carpeta de la lista, aparece su contenido en el panel principal.<br /><br /> **Ir a la última carpeta visitada**: Devuelve la opción **Buscar en** en la ubicación anterior.<br /><br /> **Subir un nivel**: Localiza la carpeta inmediatamente superior en la jerarquía.<br /><br /> **Crear nueva carpeta**: Seleccione esta opción para crear una nueva carpeta secundaria bajo la carpeta seleccionada en **Buscar en**.<br /><br /> **Menú Ver**: Seleccione esta opción para cambiar la vista de contenido en el panel principal.  Para obtener más información sobre las opciones del **menú Ver**, vea el tema de introducción a la visualización de archivos y carpetas en la documentación de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Las siguientes opciones están disponibles:<br />Vistas en miniatura<br />Mosaicos<br />Iconos<br />Lista<br />Detalles<br /><br /> **Panel principal**: Muestra el contenido de la carpeta seleccionada en **buscar en**. Seleccione uno o varios elementos y, a continuación, haga clic en **agregar** para agregar los archivos seleccionados para **proyectos y componentes seleccionados**. Para obtener más información sobre las opciones y el menú contextual del panel principal, vea el tema dedicado a la introducción a la visualización de archivos y carpetas en la documentación de Windows.<br /><br /> **Nombre de archivo**: Utilice esta opción para filtrar los archivos y las carpetas mostrados. Escriba un nombre completo o parte del mismo para filtrar. Puede usar el asterisco (\*) como carácter comodín. Escriba varios nombres de archivo (cada nombre de archivo debe ir entre comillas dobles (") y delimitado por un espacio) para seleccionar varios archivos. También puede seleccionar archivos revisados anteriormente si selecciona un nombre de archivo de la lista desplegable. Sugerencia: Puede encontrar los servidores Web y equipos de la red mediante la especificación de una ruta de acceso de red o la dirección URL en **nombre de archivo**. Por ejemplo, "http://mywebsite " muestra los archivos disponibles en la ubicación web "miSitioWeb" y "\\ \miServidor\miRecursoCompartido" muestra los archivos disponibles en la ubicación "miRecursoCompartido" en "miServidor".<br /><br /> **Archivos de tipo**: Use esta opción para filtrar el contenido de la carpeta o el directorio seleccionado en **buscar en** para un determinado tipo de archivo.|  
|**Recent**|Muestra una lista de referencias de componentes agregadas recientemente a proyectos en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Seleccione uno o varios elementos de la cuadrícula y, a continuación, haga clic en **Agregar** para agregar los ensamblados de .NET Framework seleccionados a **Proyectos y componentes seleccionados**. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre de componente**: Nombre completo, o descriptivo, del componente. Seleccione el título para ordenar por nombre de componente.<br /><br /> **Versión**: Número de versión indicado del componente. Seleccione el título para ordenar por versión.<br /><br /> **Tiempo de ejecución**: Versión de .NET Framework en que se basa el componente. Seleccione el título para ordenar por versión de tiempo de ejecución.<br /><br /> **Ruta de acceso**: Nombre de archivo del componente y ruta de acceso donde se encuentra. Seleccione el título para ordenar por ruta de acceso.|  
|**Agregar**|Haga clic para agregar un componente seleccionado en las pestañas **.NET**, **Examinar**o **Reciente** a **Proyectos y componentes seleccionados**.|  
|**Quitar**|Haga clic para quitar un componente seleccionado en **Proyectos y componentes seleccionados**.|  
|**Proyectos y componentes seleccionados**|Muestra una lista de referencias de componentes que se agregarán al proyecto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Seleccione uno o varios elementos de la cuadrícula y, a continuación, haga clic en **Quitar** para quitar los componentes seleccionados de la cuadrícula. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nombre de componente**: Nombre completo, o descriptivo, del componente. Seleccione el título para ordenar por nombre de componente.<br /><br /> **Versión**: Número de versión indicado del componente. Seleccione el título para ordenar por versión.<br /><br /> **Tiempo de ejecución**: Versión de .NET Framework en que se basa el componente. Seleccione el título para ordenar por versión de tiempo de ejecución.<br /><br /> **Ruta de acceso**: Nombre de archivo del componente y ruta de acceso donde se encuentra. Seleccione el título para ordenar por ruta de acceso.|  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Administración de ensamblados de modelos multidimensionales](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
