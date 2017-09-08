---
title: "Jerarquías | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e3e50e89-f85d-485b-a271-1e0550520212
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ce337737331ecf67332e4f012993a28d59715b0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchies"></a>Jerarquías
  Las jerarquías, en los modelos tabulares, son metadatos que definen las relaciones entre dos o más columnas de una tabla. Las jerarquías pueden aparecer por separado de otras columnas en una lista de campos del cliente de informes, facilitando la navegación de los usuarios del cliente y su inclusión en un informe.  
  
##  <a name="bkmk_benefits"></a> Ventajas  
 Las tablas pueden incluir docenas o incluso centenares de columnas con nombres de columna inusuales sin ningún orden aparente. Esto puede ofrecer un aspecto desordenado en las listas de campos del cliente de informes, dificultando a los usuarios la búsqueda e inclusión de datos en un informe. Las jerarquías pueden proporcionar una vista sencilla e intuitiva de las normalmente complejas estructuras de datos.  
  
 Por ejemplo, en una tabla Fecha puede crear una jerarquía Calendario. Año natural se usa como nivel primario superior, incluyéndose Mes, Semana y Día como niveles secundarios (Año natural->Mes->Semana->Día). Esta jerarquía muestra una relación lógica desde Año natural hasta Día. A continuación, el usuario del cliente puede seleccionar Año natural en una lista de campos para incluir todos los niveles en una tabla dinámica, o expandir la jerarquía y seleccionar solo aquellos niveles que desea incluir en la tabla dinámica.  
  
 Puesto que cada nivel de una jerarquía es una representación de una columna de una tabla, se puede cambiar de nombre de nivel. Aunque no es algo exclusivo de las jerarquías (se puede cambiar el nombre de cualquier columna de un modelo tabular), el cambio de nombre de los niveles de jerarquía puede facilitar a los usuarios la búsqueda e inclusión de niveles en un informe. Al cambiar el nombre de un nivel no se cambiará el nombre de la columna a la que hace referencia; simplemente se facilitará la identificación del nivel. Por ejemplo, en la jerarquía Año natural, en la vista de datos de la tabla Fecha, se cambió el nombre de las columnas CalendarYear, CalendarMonth, CalendarWeek y CalendarDay a Calendar Year, Month, Week y Day para facilitar su identificación. El cambio de nombre de los niveles tiene la ventaja adicional de proporcionar coherencia en los informes, puesto que así será menos probable que los usuarios necesiten cambiar los nombres de las columnas para que sean más legibles en las tablas dinámicas, los gráficos, etc.  
  
 Es posible incluir jerarquías en perspectivas. Las perspectivas definen subconjuntos visibles de un modelo que ofrecen puntos de vista centrados, específicos del negocio o específicos de la aplicación del modelo. Por ejemplo, una perspectiva puede ofrecer a los usuarios una lista visible (jerarquía) que contiene solo los elementos de datos necesarios para sus requisitos específicos de informes. Para obtener más información, consulte [perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
 Las jerarquías no están diseñadas para usarse como mecanismo de seguridad, sino como una herramienta para proporcionar una mejor experiencia para el usuario. Toda la seguridad de una determinada jerarquía se hereda del modelo subyacente. Las jerarquías no pueden proporcionar acceso a objetos del modelo a los que el usuario no tiene acceso. La seguridad de la base de datos del modelo se debe resolver antes de tener acceso a los objetos del modelo mediante una jerarquía. Los roles de seguridad se pueden usar para proteger los datos y los metadatos de los modelos. Para obtener más información, consulte [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
##  <a name="bkmk_define"></a> Defining hierarchies  
 Las jerarquías se crean y administran en la vista de diagrama del diseñador de modelos. La creación y administración de jerarquías no se admite en la vista de datos del diseñador de modelos. Para ver el diseñador de modelos en la Vista Diagrama, haga clic en el menú **Modelo** , a continuación seleccione **Vista de modelo**y haga clic en **Vista Diagrama**.  
  
 Para crear una jerarquía, haga clic con el botón derecho en la columna que quiera especificar como nivel primario y, después, haga clic en **Crear jerarquía**. Puede seleccionar e incluir varias columnas (en una única tabla), o puede agregarlas posteriormente como niveles secundarios haciendo clic y arrastrándolas al nivel primario. Cuando se seleccionan varias columnas, estas se colocan automáticamente en un orden basado en la cardinalidad. Puede cambiar este orden haciendo clic y arrastrando una columna (nivel) a un orden diferente o usando los controles de navegación Subir y Bajar del menú contextual. Al agregar una columna como nivel secundario, puede usar la detección automática arrastrando y colocando las columnas en el nivel primario.  
  
 Una columna puede aparecer en varias jerarquías. Las jerarquías no pueden incluir objetos que no sean columnas, como medidas o KPI. Una jerarquía puede estar basada solo en columnas de una única tabla. Si selecciona varias medidas junto con una o más columnas, o si selecciona columnas de varias tablas, el comando **Crear jerarquía** estará deshabilitado en el menú contextual. Para agregar una columna de otra tabla diferente, use la función DAX RELATED para agregar una columna calculada que haga referencia a la columna de la tabla relacionada. La función emplea la sintaxis siguiente: `=RELATED(TableName[ColumnName])`. Para obtener más información, vea la función RELATED.  
  
 De forma predeterminada, las nuevas jerarquías se denominan Jerarquía 1, Jerarquía 2, etc. Debe cambiar los nombres de las jerarquías para que reflejen la naturaleza de la relación de los elementos primarios y secundarios, facilitando su identificación a los usuarios.  
  
 Una vez creadas las jerarquías, puede probar su eficacia mediante la característica Analizar en Excel. Para obtener más información, consulte [analizar en Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Tareas relacionadas  
  
|Tarea|Description|  
|----------|-----------------|  
|[Crear y administrar jerarquías](../../analysis-services/tabular-models/create-and-manage-hierarchies-ssas-tabular.md)|Describe cómo crear y administrar jerarquías mediante la vista de diagrama del diseñador de modelos.|  
  
## <a name="see-also"></a>Vea también  
 [Diseñador de modelos tabulares](../../analysis-services/tabular-models/tabular-model-designer-ssas.md)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
