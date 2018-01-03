---
title: Panel Detalles del Explorador de objetos| Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-objects
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.summary.general.f1
- sql13.swb.summary.report.f1
helpviewer_keywords:
- object search [SQL Server], Object Explorer
- Object Explorer
- object search [SQL Server]
- searching objects [SQL Server]
ms.assetid: b963e3c2-dc9e-4d38-bd28-2e00fe9e0e47
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bf7fdbd0c791ae6302774116769b91fcd4a6ee3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="object-explorer-details-pane"></a>Panel de detalles del Explorador de objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Detalles del Explorador de objetos, un componente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], proporciona una vista tabular de todos los objetos del servidor y presenta una interfaz de usuario para administrarlos. Las funciones del Explorador de objetos varían ligeramente según el tipo de servidor, aunque, por lo general, incluyen características de desarrollo de bases de datos y características de administración de todo tipo de servidores.  
  
El panel Detalles del Explorador de objetos aparece en [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] de forma predeterminada. Si no aparece el Explorador de objetos, en el menú **Ver** , haga clic en **Detalles del Explorador de objetos** o presione **F7**.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] muestra las fechas con el formato de las opciones de configuración regional y de idioma de Microsoft Windows seleccionadas cuando se inició [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] . Reinicie [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] para reflejar la nueva configuración.  
  
## <a name="object-explorer-details"></a>Detalles del Explorador de objetos  
Detalles del Explorador de objetos se puede utilizar para navegar por las carpetas y los objetos de su instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . En sistemas operativos de 32 bits, el Explorador de objetos solamente puede mostrar 64.000 objetos. Se debe seleccionar un icono para tener acceso a más objetos.  
  
Detalles del explorador de objetos incluye una barra de herramientas que contiene los iconos descritos en la siguiente tabla. Los iconos solo están disponibles cuando proceda.  
  
|Icono|Acción|  
|--------|----------|  
|**Atrás**|Se desplaza a los elementos anteriores mostrados en Detalles del Explorador de objetos. Vuelve a ejecutar una búsqueda cuando la presentación previa es el resultado de una operación de búsqueda.|  
|**Adelante**|Se desplaza a la siguiente pantalla después de seleccionar una operación **Atrás** .|  
|**Subir**|Se desplaza al objeto o carpeta principal.|  
|**Sincronizar**|Establece el foco del Explorador de objetos en el objeto seleccionado en Detalles del Explorador de objetos.|  
|**Filter**|Cuando está disponible, muestra un subconjunto de objetos que se puede configurar.|  
|**Actualizar**|Actualiza la presentación en Detalles del Explorador de objetos.|  
|**Buscar**|Proporciona un área donde escribir un término de búsqueda para algunos objetos de la base de datos.|  
  
### <a name="column-header-selections"></a>Selecciones de encabezados de columnas  
Las columnas de Detalles del Explorador de objetos se pueden seleccionar. Puede hacer clic con el botón secundario en cualquier encabezado de columna y buscar los elementos que desea mostrar. Sus selecciones se mantendrán en los distintos objetos por los que navegue. Las selecciones de cada usuario se mantienen al salir de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]y reiniciarlo.  
  
> [!CAUTION]  
> Si se muestran todas las columnas de algunos tipos de objetos, como las bases de datos, se puede reducir ligeramente la velocidad de representación de conjuntos de objetos grandes.  
  
### <a name="sorting"></a>Ordenar  
Al hacer clic una vez en el encabezado de una columna, se ordenará por esa columna. Si vuelve a hacer clic en la misma columna, se clasifica en orden inverso por esa columna. Las selecciones de ordenación se mantienen para cada usuario en los objetos y las carpetas, así como al reiniciar [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] .  
  
### <a name="filtering"></a>Filtrar  
Algunas listas de objetos que se muestran en Detalles del Explorador de objetos se pueden filtrar mediante el icono **Filtro** de la barra de herramientas de Detalles del Explorador de objetos. El icono se habilitará cuando sea posible la operación de filtrado.  
  
### <a name="details-pane"></a>Panel de detalles  
El área inferior de Detalles del Explorador de objetos contiene un panel que muestra algunos detalles del objeto seleccionado. Si se seleccionan varios objetos, solo se muestra su recuento. Cuando seleccione elementos del panel, haga clic en el icono **Copiar** para copiar el texto mostrado en el Portapapeles.  
  
La tecla de flecha hacia abajo mueve la selección al próximo elemento de la lista. La tecla de flecha hacia arriba mueve la selección al elemento anterior de la lista. Mantener presionada la tecla de flecha permite recorrer los elementos rápidamente. La selección se detiene en la parte inferior o superior de la lista de propiedades.  
  
Al escribir el primer carácter del nombre de una propiedad, la selección se mueve a la próxima propiedad que comienza con ese carácter.  
  
Si las propiedades están organizadas en varias columnas, utilice las flechas izquierda y derecha para moverse a las columnas adyacentes.  
  
Para copiar los valores de propiedad en el Portapapeles, utilice las combinaciones de teclas siguientes:  
  
-   Ctrl+C copia el valor de propiedad.  
  
-   Ctrl+Mayús+C copia el nombre de propiedad y su valor con un delimitador de tabulador.  
  
Utilice el menú de acceso directo en el panel de propiedades Detalles del Explorador de objetos para copiar todas las propiedades o todas las propiedades con sus nombres en el Portapapeles.  
  
Para mostrar un valor de propiedad si no se muestra entero en el ancho del campo, desplace el puntero del mouse sobre el valor o establezca el foco de la interfaz de usuario en el valor de propiedad, a fin de activar una información sobre herramientas con el valor de propiedad completo. Los lectores de pantalla de accesibilidad comunicarán el valor de propiedad completo cuando el usuario sitúe el foco en el valor de propiedad largo.  
  
Si el número de propiedades en el panel de propiedades supera la cantidad que cabe en el área de contenido, aparecerá una barra de desplazamiento en el lado derecho del panel. Utilice la barra de desplazamiento para ajustar la vista de los valores de propiedad en el área de contenido.  
  
### <a name="multiple-object-selection"></a>Seleccionar varios objetos  
Detalles del Explorador de objetos admite la selección de varios objetos. Por ejemplo, si selecciona Tablas en el Explorador de objetos, en la ventana de Detalles del Explorador de objetos, si mantiene presionada la tecla **Ctrl** , puede seleccionar diversas tablas. Presione el botón derecho y a continuación seleccione **Eliminar** o **Incluir tabla como** para actuar inmediatamente en todas las tablas seleccionadas. Los comandos de copia estándar copiarán el texto mostrado en el Portapapeles.  
  
## <a name="sql-server-object-search"></a>Buscar objetos de SQL Server  
Caracteres comodín  
  
-   Se admiten los caracteres comodín estándar. Por ejemplo, si se busca **dm_os%counters** , se devuelve tanto dm_os_memory_cache_counters como dm_os_performance_counters. Para más información, consulte [Buscar texto con caracteres comodín](http://msdn.microsoft.com/en-us/449600f8-cc87-4b3f-878a-59c158a88a40).  
  
Ámbito de búsqueda  
  
-   La búsqueda se centra en el foco actual del árbol del Explorador de objetos. Por ejemplo, si el Explorador de objetos se centra en una base de datos, buscar **dm_os%counters** devuelve dm_os_memory_cache_counters y dm_os_performance_counters de esa base de datos. Si el Explorador de objetos se centra en el nodo Bases de datos, se busca en todas las bases de datos y se devuelven varias instancias de las vistas dinámicas.  
  
Grandes conjuntos  
  
-   La realización de búsquedas en conjuntos de objetos grandes puede tardar mucho tiempo y reducir el rendimiento del servidor.  
  
## <a name="see-also"></a>Ver también  
[Ver](../../ssms/object/object-explorer.md)  
  
