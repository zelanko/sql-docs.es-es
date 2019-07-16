---
title: Proyectos de minería de datos | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f2fd0817aeae714ca1e217b9dc2011df92c4b28
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210100"
---
# <a name="data-mining-projects"></a>Proyectos de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un proyecto de minería de datos forma parte de una solución de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Durante el proceso de diseño, los objetos que crea en este proyecto están disponibles para probarlos y consultarlos como parte de una base de datos del área de trabajo. Cuando desee que los usuarios puedan consultar o examinar los objetos del proyecto, debe implementarlo en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecute en modo multidimensional.  
  
 En este tema se proporciona la información básica necesaria para comprender y crear proyectos de minería de datos.  
  
 [Crear proyectos de minería de datos](#bkmk_Overview)  
  
 [Objetos de proyectos de minería de datos](#bkmk_Objects)  
  
-   [Orígenes de datos](#bkmk_DataSources)  
  
-   [Vistas del origen de datos](#bkmk_DSV)  
  
-   [Estructuras de minería de datos](#bkmk_Structures)  
  
-   [Modelos de minería de datos](#bkmk_Models)  
  
 [Usar el proyecto completado de minería de datos](#bkmk_Complete)  
  
-   [Ver y explorar modelos](#bkmk_ViewExplore)  
  
-   [Probar y validar modelos](#bkmk_Validate)  
  
-   [Crear predicciones](#bkmk_Predict)  
  
 [Acceso a proyectos de minería de datos mediante programación](#bkmk_API)  
  
##  <a name="bkmk_Overview"></a> Crear proyectos de minería de datos  
 En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], los proyectos se crean con la plantilla **Proyecto de minería de datos y OLAP**. También puede crear proyectos de minería de datos mediante programación, mediante AMO. Los objetos individuales de minería de datos pueden crearse usando el lenguaje de scripting de Analysis Services (ASSL). Para obtener más información, vea [Acceso a datos de modelos multidimensionales &#40;Analysis Services: datos multidimensionales&#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md).  
  
 Si crea un proyecto de minería de datos en una solución existente, de forma predeterminada los objetos de minería de datos se implementan en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con el mismo nombre que el archivo de solución. Puede cambiar este nombre y el servidor de destino mediante el cuadro de diálogo **Propiedades del proyecto** . Para obtener más información, vea [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
> [!WARNING]  
>  Para generar e implementar correctamente el proyecto, debe tener acceso a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecute en modo de minería de datos y OLAP. No puede desarrollar ni implementar soluciones de minería de datos en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que admita modelos tabulares, ni puede usar los datos directamente de un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o de un modelo tabular que use el almacén de datos en memoria. Para determinar si la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que tiene admite la minería de datos, vea [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Dentro de cada proyecto de minería de datos que cree, seguirá estos pasos:  
  
1.  Elija un *origen de datos*, como un cubo, una base de datos o incluso archivos de texto o de Excel, que contenga los datos sin formato que utilizará para generar los modelos.  
  
2.  Defina un subconjunto de los datos del origen de datos que se usarán para el análisis y guárdelos como *vista del origen de datos*.  
  
3.  Defina una *estructura de minería de datos* para el modelado.  
  
4.  Agregue *modelos de minería de datos* a la estructura de minería de datos, elija un *algoritmo* y especifique el modo en que el algoritmo controlará los datos.  
  
5.  Entrene los modelos rellenándolos con los datos seleccionados o con un subconjunto filtrado de los datos.  
  
6.  Explore, pruebe y genere modelos.  
  
 Cuando el proyecto esté completo, puede implementarlo para que los usuarios lo examinen o lo consulten, o puede proporcionar acceso mediante programación a los modelos de minería de datos en una aplicación, para permitir las predicciones y el análisis.  
  
  
##  <a name="bkmk_Objects"></a> Objetos de proyectos de minería de datos  
 Todos los proyectos de minería de datos contienen los cuatro tipos siguientes de objetos. Puede tener varios objetos de todos los tipos.  
  
-   Orígenes de datos  
  
-   Vistas del origen de datos  
  
-   Estructuras de minería de datos  
  
-   Modelos de minería de datos  
  
 Por ejemplo, un solo proyecto de minería de datos puede contener una referencia a varios orígenes de datos y cada origen de datos puede admitir varias vistas del origen de datos. A su vez, cada vista del origen de datos puede admitir varias estructuras de minería de datos, cada una con varios modelos de minería de datos relacionados.  
  
 Además, el proyecto puede incluir algoritmos de complemento, ensamblados personalizados o procedimientos almacenados personalizados; sin embargo, estos objetos no se describen aquí. Para obtener más información, vea [Guía del desarrollador (Analysis Services)](../../analysis-services/analysis-services-developer-documentation.md).  
  
  
###  <a name="bkmk_DataSources"></a> Data Sources  
 El origen de datos define la cadena de conexión e información de autenticación que el servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizará para conectarse al origen de datos. El origen de datos puede contener varias varias tablas o vistas; puede ser tan simple como un único libro de Excel o un archivo de texto, o tan complejo como una base de datos de procesamiento analítico en línea (OLAP) o una base de datos relacional grande.  
  
 Un solo proyecto de minería de datos puede hacer referencia a varios orígenes de datos. Aunque un modelo de minería de datos puede utilizar un origen de datos cada vez, el proyecto podría tener varios modelos que dibujen en orígenes de datos diferentes.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite datos de muchos proveedores externos y la minería de datos de SQL Server puede usar tanto los datos relacionales como los datos de cubo como origen de datos. Sin embargo, si desarrolla ambos tipos de proyectos de modelos basados en orígenes relacionales y modelos basados en cubos OLAP-es posible que desee desarrollarlos y administrarlos en proyectos independientes.  
  
-   Normalmente, los modelos que se basaban en un cubo OLAP se deben desarrollar dentro de la solución de diseño OLAP. Una razón es que los modelos basados en un cubo deben procesar el cubo para actualizar los datos. Generalmente, debe utilizar los datos de un cubo solo cuando ese sea el medio principal de almacenamiento y acceso de los datos, o cuando se requieran agregaciones, dimensiones y atributos creados por el proyecto multidimensional.  
  
-   Si el proyecto usa datos relacionales, solo debe crear modelos relacionales en un proyecto independiente, de modo que no vuelva a procesar innecesariamente otros objetos. En muchos casos, la base de datos de ensayo o el almacenamiento de datos utilizado para admitir la creación del cubo ya contiene las vistas que se necesitan para realizar la minería de datos y puede utilizar estas vistas para la minería de datos en lugar de las agregaciones y las dimensiones del cubo.  
  
-   No puede usar los datos en memoria o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] directamente para crear modelos de minería de datos.  
  
 El origen de datos solo identifica el servidor o el proveedor y el tipo general de los datos. Si tiene que cambiar las agregaciones y el formato de los datos, utilice el objeto de vista del origen de datos.  
  
 Para controlar la manera en que los datos del origen de datos se controlan, puede agregar columnas derivadas o cálculo, modificar los agregados o cambiar el nombre de las columnas de datos en la vista del origen de datos. (También puede trabajar con los datos de nivel inferior, modificando las columnas de la estructura de minería de datos o empleando marcas de modelado y filtros en la columna de minería de datos).  
  
 Si se requiere una limpieza de los datos o los datos del almacén de datos deben modificarse para crear variables adicionales, cambiar los tipos de datos o crear agregaciones alternativas, puede que tenga que crear tipos de proyecto adicionales que sirvan para la minería de datos. Para obtener más información sobre estos proyectos relacionados, vea [Proyectos relacionados en las soluciones de minería de datos](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md).  
  
  
###  <a name="bkmk_DSV"></a> Data Source Views  
 Después de definir esta conexión a un origen de datos, crea una vista que identifica los datos concretos pertinentes para el modelo.  
  
 La vista del origen de datos también le permite personalizar la manera en que los datos del origen de datos se proporcionan al modelo de minería de datos. Puede modificar la estructura de los datos para hacerla más pertinente para el proyecto o elegir únicamente ciertos tipos de datos.  
  
 Por ejemplo, mediante el Asistente para vistas del origen de datos, puede:  
  
-   Crear columnas derivadas, como partes, subcadenas, etc.  
  
-   Agregar valores mediante instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] como GROUP BY  
  
-   Restringir los datos temporalmente o los datos de ejemplo  
  
 Para obtener más información sobre cómo puede modificar datos en una vista del origen de datos, vea [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!WARNING]  
>  Si desea filtrar los datos, puede hacerlo en la vista del origen de datos, pero también puede crear filtros en los datos en el nivel del modelo de minería de datos. Dado que la definición del filtro se almacena junto con el modelo de minería de datos, el uso de filtros de modelo facilita más determinar los datos que se utilizaron para entrenar el modelo. Además, puede crear varios modelos relacionados, con diversos criterios de filtro. Para obtener más información, vea [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Observe que la vista del origen de datos que cree puede contener datos adicionales que no se usen directamente para el análisis. Por ejemplo, puede agregar a la vista del origen de datos los datos que se utilizan para las pruebas, las predicciones o para la obtención de detalles. Para obtener más información sobre estos usos, vea [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md) y [Consultas de obtención de detalles (minería de datos)](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
  
###  <a name="bkmk_Structures"></a> Mining Structures  
 Cuando haya creado la vista del origen de datos y el origen de datos, debe seleccionar las columnas de datos que sean más pertinentes para el problema de negocio definiendo *estructuras de minería de datos* dentro del proyecto. Una estructura de minería de datos indica al proyecto qué columnas de datos de la vista del origen de datos se deben utilizar realmente en el modelado, el entrenamiento y las pruebas.  
  
 Para agregar una nueva estructura de minería de datos, inicie el Asistente para minería de datos. El asistente define de forma automática una estructura de minería de datos, le guía por el proceso de elección de los datos y, si lo desea, le permite agregar un modelo de minería de datos inicial a la estructura. En la estructura de minería de datos, elija las tablas y columnas de la vista del origen de datos o de un cubo OLAP, y defina relaciones entre las tablas, si los datos incluyen tablas anidadas.  
  
 La elección de los datos será muy diferente en el Asistente para minería de datos, en función de si utiliza orígenes de datos relacionales o de procesamiento analítico en línea (OLAP).  
  
-   Si elige datos de un origen de datos relacional, la configuración de una estructura de minería de datos es fácil: elija las columnas de datos en la vista del origen de datos y establezca personalizaciones adicionales como alias o defina el modo en que los valores de la columna deberían agruparse o discretizarse. Para obtener más información, vea [Crear una estructura de minería de datos relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md).  
  
-   Si usa los datos de un cubo OLAP, la estructura de minería de datos debe estar en la misma base de datos que la solución OLAP.  Para crear una estructura de minería de datos, puede seleccionar atributos de las dimensiones y las medidas relacionadas en la solución OLAP. Los valores numéricos se encuentran normalmente en las medidas y las variables de categorías en las dimensiones. Para obtener más información, vea [Crear una estructura de minería de datos OLAP](../../analysis-services/data-mining/create-an-olap-mining-structure.md).  
  
-   También puede definir estructuras de minería de datos mediante DMX. Para obtener más información, vea [Instrucciones de definición de datos de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/dmx-statements-data-definition.md).  
  
 Después de crear la estructura de minería de datos inicial, puede copiar, modificar y crear alias de las columnas de la estructura.  
  
 Cada estructura de minería de datos puede contener varios modelos de minería de datos. Por tanto, cuando termine, puede abrir la estructura de minería de datos de nuevo y utilizar [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md) para agregar más modelos de minería de datos a la estructura.  
  
 También tiene la opción de separar los datos en un conjunto de datos de entrenamiento, que se usan para generar modelos y un conjunto de datos de exclusión para usarlos al probar o validar los modelos de minería de datos.  
  
> [!WARNING]  
>  Algunos tipos de modelo, como los modelos de serie temporal, no admiten la creación de conjuntos de datos de exclusión que requieren una serie continua de datos para el entrenamiento. Para más información, consulte [Training and Testing Data Sets](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
  
###  <a name="bkmk_Models"></a> Mining Models  
 El modelo de minería de datos define el algoritmo o método de análisis que utilizará en los datos. Para cada estructura de minería de datos, agrega uno o varios modelos de minería de datos.  
  
 Según sus necesidades, puede combinar varios modelos en un solo proyecto o crear proyectos distintos para cada tipo de tarea analítica o modelo.  
  
 Una vez creada una estructura y un modelo, *procese* cada modelo ejecutando los datos de la vista del origen de datos a través del algoritmo, lo que genera un modelo matemático de los datos. Este proceso también se conoce como *entrenar el modelo*. Para más información, vea [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Una vez procesado el modelo, a continuación puede explorar visualmente el modelo de minería de datos y crear las consultas de predicción con él. Si los datos del proceso de entrenamiento se almacenan en la memoria caché, puede utilizar las consultas de *obtención de detalles* para devolver información detallada sobre los casos que se usan en el modelo.  
  
 Si desea usar un modelo de producción (por ejemplo, para usarlo en la realización de predicciones, o para la exploración de los usuarios en general) puede implementar el modelo en un servidor diferente. Si necesita volver a procesar el modelo en el futuro, también debe exportar la definición de la estructura de minería de datos subyacente (y, necesariamente, la definición del origen de datos y de la vista del origen de datos) al mismo tiempo.  
  
 Al implementar un modelo, también debe asegurarse de que las opciones de procesamiento correctas están establecidas en la estructura y el modelo, y de que los posibles usuarios tienen los permisos que necesitan para realizar consultas, ver modelos u obtener detalles para estructurar o modelar los datos. Para obtener más información, consulte [Información general de Seguridad &#40;minería de datos&#41;](../../analysis-services/data-mining/security-overview-data-mining.md).  
  
  
##  <a name="bkmk_Complete"></a> Usar el proyecto completado de minería de datos  
 En esta sección se resumen las formas en que puede utilizar el proyecto completado de minería de datos. Puede crear gráficos de precisión, explorar y validar los datos, y colocar los modelos de minería de datos a disposición de los usuarios.  
  
> [!WARNING]  
>  Los gráficos, las consultas y las visualizaciones que se utilizan con los modelos de minería de datos no se guardan como parte del proyecto de minería de datos y no se pueden implementar. Si necesita conservar estos objetos, debe guardar el contenido que se muestra o escribirlo tal como se describió para cada objeto.  
  
  
###  <a name="bkmk_ViewExplore"></a> View and Explore Models  
 Después de crear un modelo, puede utilizar herramientas visuales y consultas para explorar los patrones del modelo y para obtener más información sobre los patrones y las estadísticas subyacentes. En la pestaña **Visor de modelos de minería de datos** en el Diseñador de minería de datos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona visores para cada tipo de modelo de minería de datos, que puede utilizar para explorar los modelos.  
  
 Estas visualizaciones son temporales y se cierran sin guardar cuando se cierra la sesión con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por consiguiente, si necesita exportar estas visualizaciones a otra aplicación para mostrarlas o realizar un análisis adicional, utilice los comandos **Copiar** que se proporcionan en cada pestaña o panel de la interfaz del visor.  
  
 Los Complementos de minería de datos de Excel también proporcionan una plantilla de Visio que puede utilizar para representar modelos en un diagrama de Visio y para comentar y modificar el diagrama mediante las herramientas de Visio. Para obtener más información, vea [Complementos de minería de datos de Microsoft SQL Server 2008 para Microsoft Office 2007](http://go.microsoft.com/fwlink/?LinkID=123146).  
  
  
###  <a name="bkmk_Validate"></a> Test and Validate Models  
 Después de crear un modelo, puede investigar los resultados y decidir qué modelos se comportan mejor.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona varios gráficos que puede usar para proporcionar las herramientas que permiten comparar directamente los modelos de minería de datos y elegir el más preciso o útil. Estas herramientas incluyen un gráfico de elevación, un gráfico de beneficios y una matriz de clasificación. Puede generar estos gráficos usando la pestaña **Gráfico de precisión de minería de datos** del Diseñador de minería de datos.  
  
 También puede utilizar el informe de validación cruzada para realizar un submuestreo reiterativo de los datos y determinar si el modelo se inclina a un conjunto determinado de datos. Las estadísticas que el informe proporciona se pueden utilizar para comparar objetivamente los modelos y evalúa la calidad de los datos de entrenamiento.  
  
 Tenga en cuenta que estos informes y gráficos no se almacenan con el proyecto o en la base de datos de , por lo que, si necesita mantener o duplicar los resultados, debe guardar los resultados o escribir los objetos utilizando DMX o AMO. También puede utilizar procedimientos almacenados para la validación cruzada.  
  
 Para obtener más información, vea [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
  
###  <a name="bkmk_Predict"></a> Create Predictions  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ofrece un lenguaje de consulta denominado Extensiones de minería de datos (DMX) que es la base para crear predicciones y es fácilmente convertible en scripts. Para ayudarle a generar consultas de predicción DMX, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un generador de consultas, disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. También hay muchas plantillas DMX para el editor de consultas en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si no está familiarizado con las consultas de predicción, se recomienda utilizar el generador de consultas que se proporciona en el Diseñador de minería de datos y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, consulte [Data Mining Tools](../../analysis-services/data-mining/data-mining-tools.md).  
  
 Las predicciones que cree en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no son persistentes, de modo que si las consultas son complejas o necesita reproducir los resultados, se recomienda que guarde las consultas de predicción en archivos de consulta DMX, los incluya en scripts o inserte las consultas como parte de un paquete de Integration Services.  
  
  
##  <a name="bkmk_API"></a> Acceso a objetos de minería de datos mediante programación  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona varias herramientas que puede usar para trabajar mediante programación con proyectos de minería de datos y con los objetos contenidos en ellas. El lenguaje DMX proporciona instrucciones que puede usar para crear orígenes de datos y vistas del origen de datos, y para crear, entrenar y usar estructuras y modelos de minería de datos. Para obtener más información, vea [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 También puede llevar a cabo estas tareas mediante el Lenguaje de scripting de Analysis Services (ASSL) o bien usando Objetos de administración de análisis (AMO). Para obtener más información, vea [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).  
  
  
## <a name="related-tasks"></a>Related Tasks  
 En los temas siguientes se describe el uso del Asistente para minería de datos para crear un proyecto de minería de datos y sus objetos asociados.  
  
|Tareas|Temas|  
|-----------|------------|  
|Describe cómo trabajar con columnas de estructura de minería de datos|[Crear una estructura de minería de datos relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)|  
|Proporciona más información sobre cómo agregar nuevos modelos de minería de datos y procesar una estructura y los modelos|[Agregar modelos de minería de datos a una estructura &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Proporciona vínculos a recursos que ayudan a personalizar los algoritmos que generan modelos de minería de datos|[Personalizar la estructura y los modelos de minería de datos](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|Proporciona vínculos a información sobre cada uno de los visores de modelos de minería de datos|[Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|Proporciona información sobre cómo crear un gráfico de elevación, un gráfico de beneficios o una matriz de clasificación, o probar una estructura de minería de datos|[Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|Proporciona información sobre los permisos y las opciones de procesamiento|[Procesar objetos de minería de datos](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|Proporciona información acerca de Analysis Services|[Bases de datos de modelo multidimensional](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)|  
  
## <a name="see-also"></a>Vea también  
 [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md)   
 [Crear modelos multidimensionales utilizando las herramientas de datos de SQL Server &#40;SSDT&#41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Base de datos del área de trabajo](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)  
  
  
