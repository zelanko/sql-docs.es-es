---
title: Base de datos del área de trabajo (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: cd6d0a53894bb930c549df7b0e36dab83ed5d63e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938516"
---
# <a name="workspace-database-ssas-tabular"></a>Base de datos del área de trabajo (SSAS tabular)
  La base de datos del área del trabajo de modelos tabulares, utilizada durante la creación de modelos, se crea cuando se crea un nuevo proyecto de modelos tabulares en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. La base de datos del área de trabajo reside en memoria, en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuta en modo tabular (normalmente, en el mismo equipo que [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]).  
  
 Este tema incluye las siguientes secciones:  
  
-   [Información general sobre la base de datos del área de trabajo](#bkmk_overview)  
  
-   [Propiedades de la base de datos del área de trabajo](#bkmk_ws_prop)  
  
-   [Usar SSMS para administrar la base de datos del área de trabajo](#bkmk_use_ssms)  
  
-   [Tareas relacionadas](#bkmk_related_tasks)  
  
##  <a name="workspace-database-overview"></a><a name="bkmk_overview"></a>Información general sobre bases de datos  
 La base de datos del área de trabajo se crea en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , especificada en la propiedad Servidor del área de trabajo, cuando se crea un proyecto de Business Intelligence usando una de las plantillas de proyectos de modelos tabulares de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Cada proyecto de modelos tabulares tendrá su propia base de datos del área de trabajo. Puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver la base de datos del área de trabajo en el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El nombre de la base de datos del área de trabajo incluye el nombre del proyecto seguido de un carácter de subrayado, el nombre de usuario, otro carácter de subrayado y un GUID.  
  
 La base de datos del área de trabajo reside en memoria mientras el proyecto de modelos tabulares está abierto en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Cuando se cierra el proyecto, la base de datos del área de trabajo, bien permanece en memoria, se almacena en disco y se quita de la memoria (valor predeterminado), o se quita de la memoria y no se almacena en disco, según lo que determine la propiedad Retención de área de trabajo. Para obtener más información sobre la propiedad Retención de área de trabajo, vea [Propiedades de la base de datos del área de trabajo](#bkmk_ws_prop) más adelante en este tema.  
  
 Cuando se ven tablas, columnas y datos en el Diseñador de modelos después de haber agregado datos a un proyecto de modelos usando el Asistente para la importación de tablas o con copiar y pegar, lo que se ve en realidad es la base de datos del área de trabajo. Si agrega otras tablas, columnas, relaciones, etc., cambiará la base de datos del área de trabajo.  
  
> [!IMPORTANT]  
>  Si alguna de las tablas del modelo contiene un gran número de filas, considere importar únicamente un subconjunto de los datos durante la creación del modelo. Si importa un subconjunto de los datos, puede reducir el tiempo de procesamiento y el consumo de recursos de servidor de bases de datos del área de trabajo.  
  
> [!NOTE]  
>  La ventana de vista previa de la página Seleccionar tablas y vistas del Asistente para la importación de tablas, el cuadro de diálogo Editar propiedades de tabla y el cuadro de diálogo Administrador de particiones muestran tablas, columnas y filas del origen de datos, pero es posible que no sean las mismas tablas, columnas y filas que las que muestra la base de datos del área de trabajo.  
  
 Cuando se implementa un proyecto de modelos tabulares, la base de datos del modelo implementada, que es básicamente una copia de la base de datos del área de trabajo, se crea en la instancia del servidor de Analysis Services especificada en la propiedad Servidor de implementación. Para más información sobre las propiedades del servidor de implementación, vea [Propiedades del proyecto &#40;SSAS tabular&#41;](properties-ssas-tabular.md).  
  
 La base de datos del área de trabajo del modelo reside normalmente en un host local o en una instancia local con nombre de un servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si lo desea, puede usar una instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para hospedar la base de datos del área de trabajo; sin embargo, no se recomienda usar esta configuración debido a la latencia que se produce durante las consultas de datos y otras restricciones. En condiciones óptimas, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospedará la base de datos del área de trabajo se encuentra en el mismo equipo que [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Crear proyectos de modelos en el mismo equipo en que se encuentra la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda la base de datos del área de trabajo puede mejorar el rendimiento.  
  
 Las bases de datos de área de trabajo remotas tienen las restricciones siguientes:  
  
-   Una latencia potencial durante las consultas.  
  
-   La propiedad Copia de seguridad de datos no se puede establecer en **Hacer copia de seguridad en disco**.  
  
-   No se pueden importar datos de un libro PowerPivot cuando se crea un nuevo proyecto de modelo tabular utilizando la plantilla de proyecto Importar desde PowerPivot.  
  
##  <a name="workspace-database-properties"></a><a name="bkmk_ws_prop"></a>Propiedades de la base de datos  
 Las propiedades de la base de datos del área de trabajo están incluidas entre las propiedades del modelo. Para ver las propiedades del modelo, en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el **Explorador de soluciones**, haga clic en el archivo **Model.bim** . Las propiedades del modelo se pueden configurar usando la ventana **Propiedades** . Entre las propiedades específicas de la base de datos del área de trabajo se encuentran:  
  
> [!NOTE]  
>  Las propiedades **Servidor del área de trabajo**, **Retención del área de trabajo** y **Copia de seguridad de datos** tienen valores predeterminados que se aplican al crear un nuevo proyecto de modelos. Puede cambiar la configuración predeterminada de los nuevos proyectos de modelos en la página **Modelado de datos** de la configuración de **Analysis Server** del cuadro de diálogo Herramientas\Opciones. Estas propiedades, junto con otras, también se pueden establecer para cada proyecto de modelos en la ventana **Propiedades** . Si se cambia la configuración predeterminada, la nueva configuración no se aplicará a los proyectos de modelos creados previamente. Para obtener más información, vea [Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS tabular&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Propiedad|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Base de datos área de trabajo**|El nombre del proyecto seguido de un carácter de subrayado, el nombre de usuario, otro carácter de subrayado y un GUID.|El nombre de la base de datos del área de trabajo usada para almacenar y editar el proyecto de modelos en memoria. Después de crear un proyecto de modelos tabulares, esta base de datos aparecerá en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada en la propiedad **Servidor del área de trabajo** . Esta propiedad no se puede establecer en la ventana Propiedades.|  
|**Retención de área de trabajo**|Descargar de la memoria|Especifica cómo se conserva una base de datos del área de trabajo después de cerrar un proyecto de modelos. Una base de datos del área de trabajo incluye los metadatos del modelo y los datos importados. En algunos casos, la base de datos del área de trabajo puede ser muy grande y usar una gran cantidad de memoria. De forma predeterminada, cuando se cierra un proyecto de modelos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], la base de datos del área de trabajo se descarga de la memoria. Si se cambia este valor, es importante tener en cuenta los recursos de memoria disponibles, así como la frecuencia con que se piensa trabajar en el proyecto de modelos. El valor de esta propiedad tiene las opciones siguientes:<br /><br /> **Mantener en memoria** : especifica que, después de cerrar un proyecto de modelos, es necesario mantener en memoria la base de datos del área de trabajo. Esta opción usará más memoria; sin embargo, al abrir un proyecto de modelos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], se usan menos recursos y la base de datos del área de trabajo se cargará más rápido.<br /><br /> **Descargar de la memoria** : especifica que, después de cerrar un proyecto de modelos, es necesario conservar en el disco la base de datos del área de trabajo, pero no en memoria. Aunque esta opción usa menos memoria, al abrir un proyecto de modelos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], es necesario volver a adjuntar la base de datos del área de trabajo, con lo que se usan recursos adicionales y el proyecto de modelos se carga más lentamente que cuando la base de datos del área de trabajo se mantiene en memoria. Use esta opción cuando los recursos de memoria sean limitados o cuando trabaje en una base de datos de área de trabajo remota.<br /><br /> **Eliminar área de trabajo** : especifica que es necesario eliminar de la memoria la base de datos del área de trabajo y que no hay que mantenerla en el disco después de cerrar el proyecto de modelos. Aunque esta opción usa menos memoria y espacio de almacenamiento, al abrir un proyecto de modelos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], se usan recursos adicionales y el proyecto de modelos se cargará con mayor lentitud que cuando la base de datos del área de trabajo se mantiene en memoria o en disco. Utilice esta opción cuando solo trabaje ocasionalmente con proyectos de modelos.<br /><br /> <br /><br /> La configuración predeterminada para esta propiedad se puede cambiar en la página **modelado de datos** de **Analysis Server** configuración del cuadro de diálogo herramientas\opciones..|  
|**Servidor del área de trabajo**|localhost|Esta propiedad especifica el servidor predeterminado que se usará para hospedar la base de datos del área de trabajo mientras se crea el proyecto de modelos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Todas las instancias disponibles de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecutan en el equipo local se incluyen en el cuadro de lista.<br /><br /> Para especificar un servidor diferente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (que se ejecute en modo tabular), escriba su nombre. El usuario que ha iniciado sesión debe ser administrador del servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> Tenga en cuenta que se recomienda especificar un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] servidor local como servidor del área de trabajo. Para las bases de datos del área de trabajo de un servidor remoto, la importación desde PowerPivot no se admite, no se pueden realizar copias de seguridad de los datos localmente y la interfaz de usuario puede experimentar latencia durante las consultas.<br /><br /> Tenga en cuenta también que el valor predeterminado de esta propiedad se puede cambiar en la página modelado de datos de la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configuración del cuadro de diálogo herramientas\opciones..|  
  
##  <a name="using-ssms-to-manage-the-workspace-database"></a><a name="bkmk_use_ssms"></a> Usar SSMS para administrar la base de datos del área de trabajo  
 Puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) para conectarse con el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda la base de datos del área de trabajo. Por lo general, no es necesaria ninguna administración de la base de datos del área de trabajo; la excepción es cuando hay que separar o eliminar una base de datos del área de trabajo, operación que debe realizarse desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!WARNING]  
>  No utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar la base de datos del área de trabajo mientras el proyecto está abierto en el diseñador de modelos. Si lo hace, podría provocar la pérdida de datos.  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> Tareas relacionadas  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Propiedades del modelo &#40;SSAS tabular&#41;](model-properties-ssas-tabular.md)|Proporciona descripciones y pasos de configuración para las propiedades de base de datos del área de trabajo de un modelo.|  
  
## <a name="see-also"></a>Consulte también  
 [Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS tabular&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Propiedades del proyecto &#40;SSAS tabular&#41;](properties-ssas-tabular.md)  
  
  
