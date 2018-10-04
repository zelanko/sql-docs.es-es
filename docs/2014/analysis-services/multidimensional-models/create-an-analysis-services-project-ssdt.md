---
title: Crear un proyecto de Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- templates [Analysis Services]
- templates [Analysis Services], projects
- projects [Analysis Services], creating
- projects [Analysis Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, defining projects [Analysis Services]
- items [Analysis Services]
ms.assetid: d00913b0-cd6d-4de0-a1e7-4ce86fcc078d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 22df70966fe1bac4f9a825a97c7998d6900af02a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168105"
---
# <a name="create-an-analysis-services-project-ssdt"></a>Crear un proyecto de Analysis Services (SSDT)
  Puede definir un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando la plantilla de proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o el Asistente para importar bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a fin de leer el contenido de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si no hay ninguna solución cargada en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], la creación de un nuevo proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea automáticamente una nueva solución. De lo contrario, el nuevo proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se agregará a la solución existente. Las prácticas recomendadas para el desarrollo de soluciones pasan por crear proyectos distintos para diferentes tipos de datos de aplicación, usando una única solución si los proyectos están relacionados. Por ejemplo, puede tener una solución que contiene proyectos distintos para los paquetes de Integration Services, las bases de datos de Analysis Services y los informes de Reporting Services que usa la misma aplicación empresarial.  
  
 Un proyecto de Analysis Services contiene objetos que se usan en una única base de datos de Analysis Services. Las propiedades de implementación del proyecto especifican el nombre del servidor y de la base de datos mediante los que se implementarán los metadatos del proyecto como objetos con instancias.  
  
 Este tema contiene las siguientes secciones:  
  
 [Crear un nuevo proyecto mediante la plantilla de proyecto de Analysis Services](#bkmk_NewUsingTemplate)  
  
 [Crear un nuevo proyecto usando una base de datos existente de Analysis Services](#bkmk_NewUsingWizard)  
  
 [Agregar un proyecto de Analysis Services a una solución existente](#bkmk_AddtoExistingSolution)  
  
 [Generar e implementar la solución](#bkmk_buildDeploy)  
  
 [Carpetas de proyecto de Analysis Services](#bkmk_ProjectFolders)  
  
 [Tipos de archivo de Analysis Services](#bkmk_FileTypes)  
  
 [Plantillas de elementos de Analysis Services](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> Crear un nuevo proyecto mediante la plantilla de proyecto de Analysis Services  
 Siga estas instrucciones para crear un proyecto vacío en el que se definirán objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se podrán implementar a continuación como una nueva base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en **Archivo**, seleccione **Nuevo**y haga clic en **Proyecto**. En el cuadro de diálogo **Nuevo proyecto** , en el panel **Tipos de proyecto** , seleccione **Proyectos de Business Intelligence**.  
  
2.  En el cuadro de diálogo **Nuevo proyecto** , en la categoría **Plantillas instaladas de Visual Studio** , seleccione **Proyecto de Analysis Services**.  
  
3.  En el cuadro de texto **Nombre** , escriba el nombre del proyecto. El nombre que especifique se usará como el nombre predeterminado de la base de datos.  
  
4.  En la lista desplegable **Ubicación** , escriba o seleccione la carpeta en la que almacenar los archivos del proyecto o haga clic en **Examinar** para seleccionar una carpeta.  
  
5.  Para agregar el proyecto nuevo a la solución existente, en la lista desplegable **Solución** , seleccione **Agregar a solución**.  
  
     O bien  
  
     Para crear una nueva solución, en la lista desplegable **Solución** , seleccione **Crear nueva solución**. Para crear una nueva carpeta para la nueva solución, seleccione **Crear directorio para la solución**. En **Nombre de la solución**, escriba el nombre de la nueva solución.  
  
6.  Haga clic en **Aceptar**.  
  
##  <a name="bkmk_NewUsingWizard"></a> Crear un nuevo proyecto usando una base de datos existente de Analysis Services  
 Use el Asistente para importar bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para crear un proyecto basado en los objetos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente. Cuando se define un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] basado en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente, los metadatos de dicha base de datos se abrirán en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A continuación, estos objetos se pueden modificar en el proyecto, sin que lo objetos originales se vean afectados, y se pueden implementar en la misma base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si las propiedades de implantación así lo especifican, o en otra recién creada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para llevar a cabo pruebas comparativas. Hasta que se implementen los cambios, no tendrá efecto ningún cambio en la base de datos existente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 También puede usar la plantilla Importar base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para crear un proyecto a partir de una base de datos de producción en la que se han realizado cambios directamente desde que se implementó el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] original.  
  
 Antes de procesar o implementar el proyecto, es posible que necesite cambiar el proveedor de datos especificado en los orígenes de datos. Si el software de SQL Server que usa es más reciente que el usado para crear la base de datos, es posible que el proveedor de datos especificado en el proyecto no se pueda instalar en el equipo. Durante el procesamiento, se usará la cuenta de servicio para recuperar los datos de la base de datos de Analysis Services. Si la base de datos se encuentra en un servidor remoto, compruebe si el servicio local tiene permisos de procesamiento y de lectura en dicho servidor.  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en **Archivo**, seleccione **Nuevo**y haga clic en **Proyecto**. En el cuadro de diálogo **Nuevo proyecto** , en el panel **Tipos de proyecto** , seleccione **Proyectos de Business Intelligence**.  
  
2.  En el cuadro de diálogo **Nuevo proyecto** , en la categoría **Plantillas instaladas de Visual Studio** , seleccione **Importar base de datos de Analysis Services**.  
  
3.  Escriba la información de propiedades del proyecto y la solución, incluyendo el nombre de los archivos y su ubicación. Haga clic en **Aceptar**.  
  
4.  En la página de inicio del **Asistente para importar bases de datos de Analysis Services** , haga clic en **Siguiente**.  
  
5.  En la página **Base de datos de origen** , especifique el servidor y la base de datos de los que el asistente va a extraer el contenido y a crear el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, a continuación, haga clic en **Siguiente**.  
  
     Entre las bases de datos compatibles se incluyen las creadas en las versiones siguientes de Analysis Services: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     Puede escribir el nombre de la base de datos o hacer una consulta en el servidor para ver las bases de datos que contiene. Si la base de datos se encuentra en un servidor remoto o en un servidor de producción, puede que tenga que solicitar permiso para leerla. La configuración del firewall puede restringir aún más el acceso a una base de datos. Si obtiene un error al intentar conectarse a la base de datos, compruebe en primer lugar los permisos y la configuración del firewall.  
  
6.  Cuando el asistente termine de extraer el contenido de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , haga clic en **Finalizar** en la página **Finalización del asistente** .  
  
7.  Abra el Explorador de soluciones para ver el contenido del proyecto.  
  
##  <a name="bkmk_AddtoExistingSolution"></a> Agregar un proyecto de Analysis Services a una solución existente  
 Si ya dispone de una solución que contiene todos los archivos de origen de una aplicación empresarial, puede agregar un nuevo proyecto de Analysis Services a dicha solución.  
  
 La adición de un proyecto existente a una solución asocia el proyecto a la solución, pero no lo copia en esta. Si el proyecto de Analysis Services se creó en otra solución, los archivos de proyecto permanecen con la solución original en la que se crearon. Esto significa que los cambios realizados en el proyecto mediante cualquiera de las soluciones se aplicarán al mismo conjunto de archivos de origen. Si este comportamiento no es el deseado, en primer lugar deberá copiar o mover los archivos de proyecto a la carpeta de la nueva solución y, a continuación, agregar el proyecto a la solución.  
  
1.  Abra la solución en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. En el Explorador de soluciones, haga clic con el botón derecho en la solución, seleccione **Agregar**y, luego, haga clic en **Proyecto existente** para seleccionar el proyecto que quiere agregar.  
  
2.  Seleccione el archivo .dwproj que desea agregar a la solución.  
  
##  <a name="bkmk_buildDeploy"></a> Generar e implementar la solución  
 De manera predeterminada, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] implementa un proyecto en la instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el equipo local. Puede cambiar este destino de implementación con el cuadro de diálogo **Páginas de propiedades** del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para cambiar la propiedad de configuración **Server** .  
  
> [!NOTE]  
>  De forma predeterminada, cuando se implementa una solución, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] procesa solamente los objetos que el script de implementación ha cambiado, así como los objetos dependientes. Puede cambiar esta función con el cuadro de diálogo **Páginas de propiedades** del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para cambiar la propiedad de configuración Processing Option.  
  
 Compile e implemente la solución en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con propósitos de prueba. Al crear una solución se validan las definiciones y dependencias de los objetos en el proyecto y se genera un script de implementación. Cuando se implementa la solución se usa el motor de implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para enviar el script de implementación a la instancia especificada.  
  
 Una vez implementado el proyecto, revise y pruebe la base de datos implementada. A continuación, podrá modificar, generar e implementar de nuevo las definiciones de objetos hasta que se complete el proyecto.  
  
 Cuando se complete el proyecto, puede usar el Asistente para la implementación para implementar el script de implementación, generado al crear la solución, en las instancias de destino para las pruebas, los ensayos y la implementación final.  
  
##  <a name="bkmk_ProjectFolders"></a> Carpetas de proyecto de Analysis Services  
 Un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiene las siguientes carpetas, que se usan para organizar los elementos incluidos en el proyecto.  
  
|Carpeta|Descripción|  
|------------|-----------------|  
|Orígenes de datos|Contiene los orígenes de datos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear estos objetos con el Asistente para orígenes de datos y editarlos en el Diseñador de origen de datos.|  
|Vistas del origen de datos|Contiene las vistas del origen de datos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear estos objetos con el Asistente para orígenes de datos y editarlos en el Diseñador de vistas del origen de datos.|  
|Cubos|Contiene los cubos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear estos objetos con el Asistente para cubos y editarlos en el Diseñador de cubos.|  
|Dimensions|Contiene las dimensiones de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear estos objetos con el Asistente para dimensiones y editarlos en el Diseñador de dimensiones.|  
|Estructuras de minería de datos|Contiene las estructuras de minería de datos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear estos objetos con el Asistente para minería de datos y editarlos en el Diseñador de modelos de minería de datos.|  
|Roles|Contiene los roles de base de datos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear y administrar los roles en el Diseñador de roles.|  
|Ensamblados|Contiene referencias a las bibliotecas COM y los ensamblados de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede crear referencias con el cuadro de diálogo **Agregar referencia** .|  
|Varios|Contiene cualquier tipo de archivo excepto los de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Use esta carpeta para agregar archivos varios, como archivos de texto que contengan notas del proyecto.|  
  
##  <a name="bkmk_FileTypes"></a> Tipos de archivo de Analysis Services  
 Una solución de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] puede contener varios tipos de archivos, dependiendo de qué proyectos se incluyeron en la solución y qué elementos se incluyeron en cada proyecto. Por lo general, los archivos de cada proyecto de una solución de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] se almacenan en la carpeta de la solución, dentro de una carpeta independiente para cada proyecto.  
  
> [!NOTE]  
>  Cuando se copia un objeto a una carpeta de proyecto, el objeto no se agrega al proyecto. Se debe usar el comando **Agregar** del menú contextual del proyecto de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para agregar una definición de objeto existente al proyecto.  
  
 La carpeta de proyecto de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede contener los tipos de archivos que aparecen en la siguiente tabla.  
  
|Tipo de archivo|Descripción|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivo de definición de proyecto (.dwproj)|Contiene metadatos sobre los elementos, las configuraciones y las referencias de ensamblado definidos e incluidos en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configuración de usuario de proyecto (.dwproj.user)|Contiene información de configuración del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para un usuario específico.|  
|Archivo de origen de datos (.ds)|Contiene elementos ASSL (Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) que definen los metadatos de un origen de datos.|  
|Archivo de vista del origen de datos (.dsv)|Contiene elementos ASSL que definen los metadatos de una vista del origen de datos.|  
|Archivo de cubo (.cube)|Contiene elementos ASSL que definen los metadatos de un cubo, incluyendo grupos de medida, medidas y dimensiones de cubo.|  
|Archivo de partición (.partitions)|Contiene elementos ASSL que definen los metadatos de las particiones de un cubo especificado.|  
|Archivo de dimensión (.dim)|Contiene elementos ASSL que definen los metadatos de una dimensión de base de datos.|  
|Archivo de estructura de minería de datos (.dmm)|Contiene elementos ASSL que definen los metadatos de una estructura de minería de datos y los modelos de minería de datos asociados.|  
|Archivo de base de datos (.database)|Contiene elementos ASSL que definen los metadatos de una base de datos, incluyendo tipos de cuenta, traducciones y permisos de la base de datos.|  
|Archivo de rol de base de datos (.role)|Contiene elementos ASSL que definen los metadatos de un rol de base de datos, incluyendo miembros de roles.|  
  
##  <a name="bkmk_ItemTemplates"></a> Plantillas de elementos de Analysis Services  
 Si usa el cuadro de diálogo **Agregar nuevo elemento** para agregar nuevos elementos a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede usar una plantilla de elementos, es decir, una instrucción o script predefinido que muestra cómo realizar una determinada acción.  
  
 Las plantillas de elementos, que aparecen en la tabla siguiente, están disponibles en la categoría Elementos de proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , en el cuadro de diálogo **Agregar nuevo elemento** .  
  
|Categoría|Plantilla de elementos|Descripción|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Elementos de un proyecto|Cube|Inicia el Asistente para cubos para agregar un nuevo cubo al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Origen de datos|Inicia el Asistente para orígenes de datos para agregar un nuevo origen de datos al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Vista del origen de datos|Inicia el Asistente para vistas del origen de datos para agregar una nueva vista del origen de datos al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Rol de base de datos|Agrega un nuevo rol de base de datos al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, a continuación, muestra el Diseñador de roles para el nuevo rol de base de datos.|  
||Dimensión|Inicia el Asistente para dimensiones para agregar una nueva dimensión de base de datos al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
||Estructura de minería de datos|Inicia el Asistente para minería de datos para agregar una nueva estructura de minería de datos y el modelo de minería de datos asociado al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades de proyecto de Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)   
 [Compilar proyectos de Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)   
 [Implementar proyectos de Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
