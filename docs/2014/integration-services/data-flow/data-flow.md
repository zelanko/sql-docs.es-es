---
title: Flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- output data [Integration Services]
- data flow [Integration Services], elements
- input data [Integration Services]
- external metadata [Integration Services]
- data flow [Integration Services]
- errors [Integration Services], data flow outputs
ms.assetid: 7a50de3c-4ca0-4922-8028-fdddeb47e5b0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76c4f0d89e26e620b8c557383bd130bc8940b168
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828003"
---
# <a name="data-flow"></a>Flujo de datos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona tres tipos de componentes de flujo de datos: orígenes, transformaciones y destinos. Los orígenes extraen datos de almacenes de datos tales como tablas y vistas en bases de datos relacionales, archivos y bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Las transformaciones modifican, resumen y limpian datos. Los destinos cargan datos en almacenes de datos o crean conjuntos de datos almacenados en la memoria.  
  
> [!NOTE]  
>  Cuando utiliza proveedores personalizados, necesita actualizar el archivo ProviderDescriptors.xml con los valores de la columna de metadatos.  
  
 Además, [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona rutas que conectan la salida de un componente con la entrada de otro componente. Las rutas definen la secuencia de los componentes y permiten agregar anotaciones en el flujo de datos o ver el origen de la columna.  
  
 Los componentes de flujo de datos se conectan conectando la salida de orígenes y destinos con la entrada de transformaciones y destinos. Al generar un flujo de datos normalmente se conecta el segundo componente y los componentes subsiguientes a medida que se agregan al flujo de datos. Después de conectar el componente, las columnas de entrada están disponibles para su uso en la configuración del componente. Cuando no hay columnas de entrada disponibles, tiene que completar la configuración del componente después de conectarse al flujo de datos. Para más información, vea [Rutas de Integration Services](integration-services-paths.md) y [Conectar componentes con rutas de acceso](../connect-components-with-paths.md).  
  
 El siguiente diagrama muestra un flujo de datos que tiene un origen, una transformación con una entrada y una salida, y un destino. El diagrama incluye las entradas, salidas y salidas de error además de las columnas de entrada, salida y externas.  
  
 ![Componentes de flujo de datos y sus entradas y salidas](../media/mw-dts-dataflow.gif "Data flow components and their inputs and outputs")  
  
## <a name="data-flow-implementation"></a>Implementación de flujo de datos  
 Agregar una tarea Flujo de datos al flujo de control de un paquete es el primer paso en la implementación de un flujo de datos en un paquete. Un paquete puede incluir varias tareas Flujo de datos, cada una de las cuales tiene su propio flujo de datos. Por ejemplo, si un paquete requiere que los flujos de datos se ejecuten en un orden especificado, o que se realicen otras tareas entre los flujos de datos, debe utilizar una tarea Flujo de datos independiente para cada flujo de datos.  
  
 Una vez el flujo de control incluye una tarea Flujo de datos, puede empezar a generar el flujo de datos que usa un paquete. Para más información, vea [Tarea Flujo de datos](../control-flow/data-flow-task.md).  
  
 Crear un flujo de datos incluye las siguientes tareas:  
  
-   Agregar uno o más orígenes para extraer datos de archivos y bases de datos, y agregar administradores de conexión para conectarse a los orígenes.  
  
-   Agregar las transformaciones que satisfacen los requisitos empresariales del paquete. No es obligatorio que un flujo de datos incluya transformaciones.  
  
     Algunas transformaciones requieren un administrador de conexiones. Por ejemplo, la transformación Búsqueda usa un administrador de conexión para conectarse a la base de datos que contiene los datos de búsqueda.  
  
-   Conectar componentes de flujo de datos conectando la salida de orígenes y transformaciones con la entrada de transformaciones y destinos.  
  
-   Agregar uno o varios destinos para cargar datos en almacenes de datos tales como archivos y bases de datos, y agregar administradores de conexiones para conectarse a los orígenes de datos.  
  
-   Configurar salidas de error en componentes para controlar problemas.  
  
     En el tiempo de ejecución, pueden generarse errores de nivel de fila cuando los componentes de flujo de datos convierten datos, realizan una búsqueda o evalúan expresiones. Por ejemplo, una columna de datos con un valor de cadena no puede convertirse en un número entero, o una expresión intenta dividirse por cero. Ambas operaciones generan errores, y las filas que contienen los errores se pueden procesar independientemente mediante un flujo de errores. Para más información sobre cómo usar los flujos de errores en el flujo de datos de paquetes, vea [Control de errores en los datos](error-handling-in-data.md).  
  
-   Incluir anotaciones para que el flujo de datos se autodocumente. Para más información, vea [Usar anotaciones en paquetes](../use-annotations-in-packages.md).  
  
> [!NOTE]  
>  Al crear un paquete nuevo, también puede utilizar un asistente para ayudarle a configurar correctamente los administradores de conexiones, los orígenes y los destinos. Para más información, consulte [Create Packages in SQL Server Data Tools](../create-packages-in-sql-server-data-tools.md).  
  
 Cuando la pestaña **Flujo de datos** está activa, el cuadro de herramientas contiene orígenes, transformaciones y destinos que se pueden agregar al flujo de datos.  
  
## <a name="expressions"></a>Expresiones  
 Algunos de los componentes de flujo de datos (orígenes, transformaciones y destinos) admiten el uso de expresiones de propiedad en algunas de sus propiedades. Una expresión de propiedad es una expresión que reemplaza el valor de la propiedad cuando se carga el paquete. El paquete utiliza los valores actualizados de las propiedades en tiempo de ejecución. Las expresiones de propiedad se generan con la sintaxis de expresiones de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] y pueden incluir funciones, operadores, identificadores y variables de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md) y [Usar expresiones de propiedad en paquetes](../expressions/use-property-expressions-in-packages.md).  
  
 Si genera un paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], las propiedades de todos los componentes de flujo de datos que admiten expresiones de propiedad se muestran en la tarea Flujo de datos a la que pertenecen. Para agregar, cambiar y quitar las expresiones de propiedad de componentes de flujo de datos, haga clic en la tarea Flujo de datos y, a continuación, utilice la ventana Propiedades o el editor de la tarea a fin de agregar, cambiar o eliminar expresiones de propiedad. Las expresiones de propiedad de la tarea Flujo de datos en sí se administran en la ventana Propiedades.  
  
 Si el flujo de datos contiene componentes que usan expresiones, estas expresiones se exponen también en la ventana Propiedades. Para ver las expresiones, seleccione la tarea Flujo de datos a la que pertenece el componente. Puede ver las propiedades por categoría o en orden alfabético. Si utiliza la vista por categorías de la ventana Propiedades, las expresiones que no se usan en ninguna propiedad específica se enumeran en la categoría **Varios** . Si utiliza la vista alfabética, las expresiones se enumeran en orden por el nombre del componente de flujo de datos.  
  
## <a name="sources"></a>Orígenes  
 En [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], un origen es el componente de flujo de datos que pone datos de diferentes orígenes de datos externos a disposición de los demás componentes en el flujo de datos. Puede extraer datos de archivos planos, archivos XML, libros de Microsoft Excel y archivos que contienen datos sin formato. También puede extraer datos obteniendo acceso a las tablas y vistas en las bases de datos y ejecutando consultas.  
  
 Un flujo de datos puede incluir un solo origen o varios orígenes.  
  
 El origen de un flujo de datos normalmente tiene una salida normal. La salida normal contiene columnas de salida, que son columnas que el origen agrega al flujo de datos.  
  
 La salida normal hace referencia a las columnas externas. Una columna externa es una columna en el origen. Por ejemplo, la columna **MadeFlag** en la tabla **Producto** de la base de datos **AdventureWorks** es una columna externa que se puede agregar a la salida normal. Los metadatos para las columnas externas incluyen información tal como el nombre, tipo de datos y longitud de la columna de origen.  
  
 Una salida de error para un origen contiene las mismas columnas que la salida normal y dos columnas adicionales que proporcionan información sobre errores. El modelo de objetos de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no restringe la cantidad de salidas normales y las salidas de error que pueden tener los orígenes. La mayoría de los orígenes que incluye [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , salvo el componente de script, tienen una salida normal y muchos de los orígenes tienen una salida de error. Los orígenes personalizados se pueden codificar para implementar varias salidas normales y salidas de error.  
  
 Todas las columnas de salida están disponibles como columnas de entrada para el siguiente componente de flujo de datos en el flujo de datos.  
  
 También puede escribir orígenes personalizados. Para más información, vea [Desarrollar un componente de flujo de datos personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) y [Desarrollar tipos específicos de componentes de flujo de datos](../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md).  
  
 Los siguientes orígenes tienen propiedades que se pueden actualizar a través de expresiones de propiedad:  
  
-   [Origen ADO NET](ado-net-source.md)  
  
-   [Origen XML](xml-source.md)  
  
### <a name="sources-available-for-download"></a>Orígenes disponibles para la descarga  
 En la tabla siguiente se indican otros orígenes que puede descargar del sitio web de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .  
  
|Source|Descripción|  
|------------|-----------------|  
|Origen de Oracle|El origen de Oracle es el componente de origen de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para Oracle de Attunity. El Conector de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para Oracle por Attunity incluye también un administrador de conexiones y un destino. Para obtener más información, vea la página de descarga, [Conectores de Microsoft para Oracle y Teradata de Attunity](https://go.microsoft.com/fwlink/?LinkId=254963).|  
|Origen de SAP BI|El origen de SAP BI es el componente de origen de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector for SAP BI. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector for SAP BI incluye también un administrador de conexiones y un destino. Para obtener más información, vea la página de descarga, [Feature Pack de Microsoft SQL Server 2008](https://www.microsoft.com/download/details.aspx?id=16978).|  
|Origen de Teradata|El origen de Teradata es el componente de origen del Conector de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para Teradata por Attunity. El Conector de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para Teradata por Attunity incluye también un administrador de conexiones y un destino. Para obtener más información, vea la página de descarga de [Conectores de Microsoft para Oracle y Teradata de Attunity](https://go.microsoft.com/fwlink/?LinkId=254963).|  
  
 Para obtener una demostración de cómo aprovechar las mejoras de rendimiento de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para Oracle de Attunity, vea [Rendimiento de Microsoft Connector para Oracle de Attunity (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkID=210369).  
  
## <a name="transformations"></a>Transformaciones  
 Las capacidades de las transformaciones presentan amplias variaciones. Las transformaciones pueden realizar tareas tales como actualizar, resumir, limpiar, combinar y distribuir datos. Puede modificar valores en columnas, buscar valores en tablas, limpiar datos y agregar valores de columna.  
  
 Las entradas y salidas de una transformación definen las columnas de datos de entrada y salida. Según la operación realizada con los datos, algunas transformaciones tienen una sola entrada y varias salidas, mientras que otras transformaciones tienen varias entradas y una sola salida. Las transformaciones también pueden incluir salidas de error, que proporcionan información sobre el error que se ha producido, junto con los datos que no se pudo: por ejemplo, datos de cadena que no se pueden convertir en un tipo de datos entero. El modelo de objetos de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no restringe la cantidad de entradas, salidas normales y salidas de error que pueden contener las transformaciones. Puede crear transformaciones personalizadas que implementan cualquier combinación de varias entradas, salidas normales y salidas de error.  
  
 La entrada de una transformación se define como una o más columnas de entrada. Algunas transformaciones de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] también pueden hacer referencia a columnas externas como entrada. Por ejemplo, la entrada de la transformación Comando de OLE DB incluye columnas externas. Una columna de salida es una columna que la transformación agrega al flujo de datos. Tanto las salidas normales como las salidas de error contienen columnas de salida. Estas columnas de salida a su vez funcionan como columnas de entrada para el siguiente componente en el flujo de datos, ya sea otra transformación o un destino.  
  
 Las siguientes transformaciones tienen propiedades que se pueden actualizar a través de expresiones de propiedad:  
  
-   [Transformación División condicional](transformations/conditional-split-transformation.md)  
  
-   [Transformación Columna derivada](transformations/derived-column-transformation.md)  
  
-   [Transformación Agrupación aproximada](transformations/fuzzy-grouping-transformation.md)  
  
-   [Transformación Búsqueda aproximada](transformations/lookup-transformation.md)  
  
-   [Transformación Comando de OLE DB](transformations/ole-db-command-transformation.md)  
  
-   [Transformación Muestreo de porcentaje](transformations/percentage-sampling-transformation.md)  
  
-   [Transformación dinámica](transformations/pivot-transformation.md)  
  
-   [Transformación Muestreo de fila](transformations/row-sampling-transformation.md)  
  
-   [Transformación Ordenar](transformations/sort-transformation.md)  
  
-   [Transformación Anulación de dinamización](transformations/unpivot-transformation.md)  
  
 Para más información, consulte [Integration Services Transformations](transformations/integration-services-transformations.md).  
  
## <a name="destinations"></a>Destinos  
 Un destino es el componente de flujo de datos que escribe los datos desde un flujo de datos en un almacén de datos específico, o crea un conjunto de datos almacenado en la memoria. Puede cargar datos en archivos planos, procesar objetos analíticos y proporcionar datos a otros procesos. También puede cargar datos obteniendo acceso a las tablas y vistas en las bases de datos y ejecutando consultas.  
  
 Un flujo de datos puede incluir varios destinos que cargan datos en diferentes almacenes de datos.  
  
 Un destino de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] debe tener por lo menos una entrada. La entrada contiene columnas de entrada, que proceden de otro componente de flujo de datos. Las columnas de entrada se asignan a columnas en el destino.  
  
 Muchos destinos también tienen una salida de error. La salida de error de un destino contiene columnas de salida, que normalmente contienen información sobre errores que se producen mientras se escriben datos en el almacén de datos de destino. Los errores se producen por muchos motivos diferentes. Por ejemplo, una columna puede contener un valor NULL, mientras que la columna de destino no puede establecerse como NULL.  
  
 El modelo de objetos de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no limita la cantidad de entradas regulares y salidas de error que los destinos pueden tener, y se pueden crear destinos personalizados que implementan varias entradas y salidas de error.  
  
 También puede escribir destinos personalizados. Para más información, vea [Desarrollar un componente de flujo de datos personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) y [Desarrollar tipos específicos de componentes de flujo de datos](../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md).  
  
 Los siguientes destinos tienen propiedades que se pueden actualizar a través de expresiones de propiedad:  
  
-   [Destino de archivo plano](flat-file-destination.md)  
  
-   [Destino de SQL Server Compact Edition](sql-server-compact-edition-destination.md)  
  
### <a name="destinations-available-for-download"></a>Destinos disponibles para descarga  
 En la tabla siguiente se indican otros destinos que puede descargar del sitio web de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .  
  
|Source|Descripción|  
|------------|-----------------|  
|Destino de Oracle|El destino de Oracle es el componente de destino de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para Oracle de Attunity. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para Oracle de Attunity incluye también un administrador de conexiones y un origen. Para obtener más información, vea la página de descarga de [Conectores de Microsoft para Oracle y Teradata de Attunity](https://go.microsoft.com/fwlink/?LinkId=254963).|  
|Destino de SAP BI|El destino de SAP BI es el componente de destino de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para SAP BI. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para SAP BI incluye también un administrador de conexiones y un origen. Para obtener más información, vea la página de descarga, [Feature Pack de Microsoft SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=110393).|  
|Destino de Teradata|El destino de Teradata es el componente de destino de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para Teradata de Attunity. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para Teradata de Attunity incluye también un administrador de conexiones y un origen. Para obtener más información, vea la página de descarga, [Conectores de Microsoft para Oracle y Teradata de Attunity](https://go.microsoft.com/fwlink/?LinkId=254963).|  
  
 Para obtener una demostración de cómo aprovechar las mejoras de rendimiento de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Connector para Oracle de Attunity, vea [Rendimiento de Microsoft Connector para Oracle de Attunity (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkID=210369).  
  
## <a name="connection-managers"></a>Administradores de conexión  
 Muchos componentes de flujo de datos se conectan a orígenes de datos, y se deben agregar al paquete los administradores de conexión que necesitan los componentes antes de que el componente se pueda configurar correctamente. Puede agregar los administradores de conexión a medida que genera el flujo de datos o antes de empezar a generar el flujo de datos. Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../connection-manager/integration-services-ssis-connections.md) y [Crear administradores de conexiones](../create-connection-managers.md).  
  
## <a name="external-metadata"></a>Metadatos externos  
 Al crear un flujo de datos en un paquete mediante el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , los metadatos de los orígenes y destinos se copian en las columnas externas en orígenes y destinos, actuando como una instantánea del esquema. Cuando [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] valida el paquete, el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] compara esta instantánea con el esquema del origen o destino y expone errores y advertencias, según las modificaciones.  
  
 El proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona un modo sin conexión. Cuando se trabaja sin conexión, no se realizan conexiones a los orígenes o destinos que usa el paquete y los metadatos de las columnas externas no se actualizan.  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 Los orígenes tienen salidas, los destinos tienen entradas, y las transformaciones tienen ambos. Además, muchos componentes de flujo de datos se pueden configurar para usar una salida de error.  
  
### <a name="inputs"></a>Entradas  
 Los destinos y las transformaciones tienen entradas. Una entrada contiene una o más columnas de entrada, que pueden hacer referencia a las columnas externas si el componente de flujo de datos se ha configurado para usarlas. Las entradas se pueden configurar para supervisar y controlar el flujo de datos: por ejemplo, puede especificar si el componente debe generar un error en respuesta a un error, omitir los errores o redirigir las filas de errores a la salida de error. También puede asignar una descripción a la salida o actualizar el nombre de entrada. En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , las entradas se configuran mediante el cuadro de diálogo **Editor avanzado** . Para obtener más información acerca del **Editor avanzado** , vea [Integration Services User Interface](../integration-services-user-interface.md).  
  
### <a name="outputs"></a>Resultados  
 Los orígenes y las transformaciones siempre tienen salidas. Una salida contiene una o más columnas de salida, que pueden hacer referencia a las columnas externas si el componente de flujo de datos se ha configurado para usarlas. Las salidas se pueden configurar para proporcionar información útil para el procesamiento en dirección descendente de los datos. Por ejemplo, puede indicar si se ordena la salida. También puede proporcionar una descripción para la salida o actualizar el nombre de la salida. En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , las salidas se configuran mediante el cuadro de diálogo **Editor avanzado** .  
  
### <a name="error-outputs"></a>Salidas de error  
 Los orígenes, destinos y transformaciones pueden incluir salidas de error. Puede especificar de qué manera el componente de flujo de datos responde ante los errores en cada entrada o columna mediante el cuadro de diálogo **Configurar la salida de errores** . Si se produce un error o truncamiento de datos en el tiempo de ejecución y el componente de flujo de datos se configura para redirigir filas, las filas de datos con el error se envían a la salida de error. La salida de error se puede conectar a las transformaciones que aplican transformaciones adicionales o datos directos a un destino diferente. De forma predeterminada, una salida de error contiene las columnas de salida y dos columnas de error: **ErrorCode** y **ErrorColumn**. Las columnas de salida contienen los datos de la fila que generó el error, **ErrorCode** proporciona el código de error y **ErrorColumn** identifica la columna que genera el error.  
  
 Para más información, vea [Control de errores en los datos](error-handling-in-data.md).  
  
### <a name="columns"></a>Columnas  
 Las entradas, salidas y salidas de error son colecciones de columnas. Cada columna es configurable y, según el tipo de columna (de entrada, de salida o externa), [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona otras propiedades para la columna. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona tres formas diferentes de establecer las propiedades de las columnas: mediante programación, mediante cuadros de diálogo específicos del componente o mediante el cuadro de diálogo **Editor avanzado**.  
  
## <a name="paths"></a>Rutas  
 Las rutas conectan componentes de flujo de datos. En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , puede ver y modificar las propiedades de ruta, ver los metadatos de salida para el punto de inicio de la ruta y adjuntar visores de datos a una ruta.  
  
 Para obtener más información, consulte [Integration Services Paths](integration-services-paths.md) y [Debugging Data Flow](../troubleshooting/debugging-data-flow.md).  
  
## <a name="configuration-of-data-flow-components"></a>Configurar los componentes de flujo de datos  
 Los componentes de flujo de datos se pueden configurar a nivel de componente, en los niveles de entrada, salida y salida de error, y en el nivel de columna.  
  
-   En el nivel de componente, se configuran propiedades que son comunes para todos los componentes y las propiedades personalizadas del componente.  
  
-   En los niveles de entrada, salida y salida de error, se configuran las propiedades comunes de entradas, salidas y la salida de error. Si el componente admite varias salidas, puede agregar salidas.  
  
-   En el nivel de columna, se establecen las propiedades que son comunes a todas las columnas, además de cualquier propiedad personalizada que el componente proporcione para las columnas. Si el componente admite la adición de columnas de salida, puede agregar columnas a las salidas.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación. En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , puede configurar propiedades de los elementos mediante los cuadros de diálogo proporcionados para cada tipo de elemento, o mediante la ventana Propiedades o el cuadro de diálogo **Editor avanzado** .  
  
 Para más información sobre cómo establecer propiedades mediante el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , vea [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Agregar o eliminar un componente en un flujo de datos](add-or-delete-a-component-in-a-data-flow.md)  
  
-   [Conectar componentes de un flujo de datos](connect-components-in-a-data-flow.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Vídeo, [Rendimiento de Microsoft Connector para Oracle de Attunity (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkID=210369), en technet.microsoft.com.  
  
 Respuesta seleccionada, [cómo crear una cadena de conexión dinámica en SSIS](https://kevine323.blogspot.com/2012/04/dynamic-connection-strings-in-ssis.html).  
  
  
