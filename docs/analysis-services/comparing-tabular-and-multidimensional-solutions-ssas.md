---
title: "Comparar soluciones tabulares y multidimensionales (SSAS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 47
---
# Comparar soluciones tabulares y multidimensionales (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona varios métodos para crear un modelo semántico de Business Intelligence: multidimensional, Tabular y PowerPivot.  
  
 El uso de más de un método permite una experiencia de modelado adaptada a los diferentes requisitos empresariales y del usuario. El modelo multidimensional es una tecnología consolidada basada en estándares abiertos que adoptan muchos proveedores de software de BI, pero puede ser difícil de dominar. El modelo tabular ofrece un enfoque de modelado relacional que muchos desarrolladores consideran más intuitivo. El modelo PowerPivot es todavía más sencillo, ya que ofrece el modelado visual de datos en Excel, con compatibilidad de servidor proporcionada a través de SharePoint.  
  
 Todos los modelos se implementan como bases de datos que se ejecutan en una instancia de Analysis Services, a las que tienen acceso las herramientas de cliente mediante un único conjunto de proveedores de datos. Se visualizan en informes interactivos y estáticos a través de Excel, Reporting Services, Power BI y herramientas de BI de otros proveedores.  
  
 Debido a diferencias en la arquitectura de memoria y los metadatos, ninguno de los tipos de modelo son intercambiables, aunque puede actualizar fácilmente de un modelo Tabular 1050-1103 a Tabular 1200, así como importar Power Pivot para crear un modelo completamente nuevo como un proyecto Tabular.  
  
 Las soluciones tabulares y multidimensionales se generan con [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] y se han diseñado para proyectos de BI corporativos que se ejecutan en una instancia independiente de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Ambas soluciones producen bases de datos analíticas de alto rendimiento que se integran fácilmente con los clientes de BI. Con todo, cada solución difiere en cómo se crea, se usa y se implementa. En la mayor parte de este tema se comparan estos dos tipos para que pueda identificar el enfoque correcto para su caso.  
  
 Para los nuevos proyectos de desarrollo, generalmente recomendamos tabular. Se agiliza el diseño, la prueba y la implementación; y funcionará mejor con las aplicaciones BI de autoservicio más recientes y los servicios en la nube de Microsoft.  
  
##  <a name="a-namebkmkoverviewa-overview-of-modeling-types"></a><a name="bkmk_overview"></a> Información general de tipos de modelado  
 ¿No está familiarizado con Analysis Services? En la tabla siguiente se enumeran los diferentes modelos, se resume el enfoque y se identifica el vehículo de lanzamiento inicial.  
  
||||  
|-|-|-|  
|**Tipo**|**Descripción de modelado**|**Publicado**|  
|Multidimensional|Construcciones de modelado OLAP (cubos, dimensiones, medidas).|SQL Server 2000 y posterior|  
|Tabular|Construcciones de modelado relacional (modelo, tablas, columnas).<br /><br /> Internamente, los metadatos se heredan de las construcciones de modelado OLAP (cubos, dimensiones, medidas). El código y los scripts usan metadatos de OLAP.|SQL Server 2012 y posterior (niveles de compatibilidad 1050-1103) <sup>1</sup>|  
|Tabular en SQL Server 2016|Construcciones de modelado relacional (modelo, tablas, columnas) articuladas en definiciones de objetos de metadatos tabulares en scripts y código.|SQL Server 2016 (nivel de compatibilidad 1200)|  
|Power Pivot|Originalmente un complemento, pero ahora totalmente integrado en Excel. Solo modelado visual sobre una infraestructura tabular interna. Puede importar un modelo de Power Pivot en SSDT para crear un nuevo modelo tabular que se ejecute en una instancia de Analysis Services.|A través de Excel y Power Pivot BI Desktop|  
  
 <sup>1</sup> Los niveles de compatibilidad, presentados en SQL Server 2012 son importantes en la versión actual debido a que el nuevo motor de metadatos tabulares y la compatibilidad con las características para habilitar escenarios solo están disponibles en el nivel superior. Entre los avances más destacados se incluyen DirectQuery, scripts y programación. Para obtener información detallada, vea [What's New in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md) .  
  
##  <a name="a-namebkmkmodelsa-model-features"></a><a name="bkmk_models"></a> Características de modelo  
  En la tabla siguiente se resume la disponibilidad de características en el nivel de modelo. Revise esta lista para asegurarse de que la característica que quiere usar está disponible en el tipo de modelo que tiene previsto crear.  
  
|||||  
|-|-|-|-|  
||Multidimensional|Tabular|Power Pivot|  
|Acciones|Sí|No|No|  
|Agregaciones|Sí|No|No|  
|Columna calculada|No|Sí|Sí|  
|Medidas calculadas|Sí|Sí|Sí|  
|Tablas calculadas|No|Sí <sup>1</sup>|No|  
|Ensamblados personalizados|Sí|No|No|  
|Resúmenes personalizados|Sí|No|No|  
|Miembro predeterminado|Sí|No|No|  
|Carpetas para mostrar|Sí|Sí <sup>1</sup>|No|  
|Recuento distinto|Sí|Sí (mediante DAX)|Sí (mediante DAX)|  
|Obtención de detalles|Sí|Sí (los detalles se abren en una hoja de cálculo independiente)|Sí|  
|Jerarquías|Sí|Sí|Sí|  
|KPI|Sí|Sí|Sí|  
|Objetos vinculados|Sí|Sí (tablas vinculadas)|No|  
|Relaciones varios a varios|Sí|No (pero no hay [filtros cruzados bidireccionales](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) en el nivel de compatibilidad 1200)|No|  
|Conjuntos con nombre|Sí|No|No|  
|Jerarquías de elementos primarios y secundarios|Sí|Sí (mediante DAX)|Sí (mediante DAX)|  
|Particiones|Sí|Sí|Sí|  
|Perspectivas|Sí|Sí|Sí|  
|Medidas de suma parcial|Sí|Sí|Sí|  
|Translations|[Sí](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Sí|[Sí](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)|  
|Jerarquías definidas por el usuario|Sí|Sí|Sí|  
|Reescritura|Sí|No|No|  
  
 <sup>1</sup> Vea [Nivel de compatibilidad para modelos tabulares de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) para obtener información sobre las diferencias funcionales dentro de la banda tabular.  
  
##  <a name="a-namebkmkdsa-data-considerations"></a><a name="bkmk_ds"></a> Consideraciones sobre los datos  
 Los modelos tabulares y multidimensionales usan datos importados de orígenes externos. La cantidad y el tipo de datos que necesita importar puede ser una consideración principal a la hora de decidir qué tipo de modelo se adapta mejor a sus datos.  
  
 **Compresión**  
  
 Tanto las soluciones tabulares como las multidimensionales usan la compresión de datos que reduce el tamaño de la base de datos de Analysis Services en relación con el almacenamiento de datos desde el que importa los datos. Dado que la compresión real variará en función de las características de los datos subyacentes, no hay ninguna manera de saber con precisión cuánto espacio de memoria y de disco requerirá una solución después de procesar los datos y usarse en consultas.  
  
 Una estimación que usan numerosos desarrolladores de Analysis Services es que el almacenamiento principal de una base de datos multidimensional es aproximadamente un tercio del tamaño de los datos originales. Las bases de datos tabulares puede obtener a veces mayor cantidades de compresión, cerca de una décima de tamaño, especialmente si la mayor parte de los datos se importan de las tablas de hechos.  
  
 **Tamaño del modelo y diferencia de recursos (en memoria o disco)**  
  
 El tamaño de una base de datos de Analysis Services está limitado solo por los recursos disponibles para ejecutarla. El tipo de modelo y el modo de almacenamiento también desempeñan un papel importante al determinar el tamaño que puede alcanzar la base de datos.  
  
 Las bases de datos tabulares se ejecutan en memoria o en el modo DirectQuery, que descarga la ejecución de consultas en una base de datos externa. Para el análisis en memoria tabular, la base de datos se almacena completamente en la memoria, lo que significa que debe tener memoria suficiente para cargar no solo todos los datos, sino las estructuras de datos adicionales que se crearon para admitir las consultas.  
  
 DirectQuery se ha renovado en esta versión y tiene menos restricciones que antes y un mejor rendimiento. El aprovechamiento de la base de datos relacional de back-end para el almacenamiento y la ejecución de consultas hace que la generación de un modelo tabular a gran escala sea más viable que antes.  
  
 Históricamente, las bases de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] más grandes de producción son multidimensionales, y su procesamiento y cargas de trabajo de consulta se ejecutan de forma independiente en hardware dedicado y optimizado para su uso respectivo.  Las bases de datos tabulares se están poniendo al día rápidamente, y los nuevos avances en DirectQuery ayudarán a salvar distancia todavía más.  
  
 En el caso multidimensional, la descarga del almacenamiento de datos y la ejecución de consultas está disponible a través de ROLAP.   En un servidor de consultas, es posible almacenar en caché conjuntos de filas y paginar los antiguos. El uso eficiente y equilibrado de los recursos de memoria y disco guía suele llevar a los clientes a optar por soluciones multidimensionales.  
  
 Con carga, es previsible que tanto los requisitos de memoria como los de disco para cualquier tipo de solución aumenten mientras Analysis Services almacena en caché los datos, los almacena, los examina y los consulta. Para obtener más información sobre las opciones de paginación de memoria, consulte [Memory Properties](../analysis-services/server-properties/memory-properties.md). Para obtener más información sobre la escala, vea [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 Power Pivot para Excel tiene un límite de tamaño de archivo artificial de 2 gigabytes, impuesto de modo que los libros creados en Power Pivot para Excel se puedan cargar en SharePoint, que establece los límites máximos en el tamaño de carga de archivos. Una de las razones principales para migrar un libro Power Pivot a una solución tabular en una instancia independiente de Analysis Services es sortear la limitación de tamaño del archivo. Para obtener más información sobre cómo configurar el tamaño máximo de carga de archivos, vea [Configuración del tamaño de carga máximo de archivos &#40;PowerPivot para SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Orígenes de datos compatibles**  
  
 Las soluciones multidimensionales pueden importar los datos de orígenes de datos relacionales mediante proveedores administrados y nativos OLE DB.  
  
 Los modelos tabulares pueden importar datos de orígenes de datos relacionales, fuentes de distribución de datos y algunos formatos de documento. También puede usar OLE DB para proveedores de ODBC con modelos tabulares.  
  
 Para ver la lista de orígenes de datos externos que puede importar en cada modelo, vea los siguientes temas.  
  
-   [Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
-   [Orígenes de datos compatibles &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
##  <a name="a-namebkmklanga-query-and-scripting-language-support"></a><a name="bkmk_lang"></a> Compatibilidad con lenguaje de scripting y consulta  
 Analysis Services incluye MDX, DMX, DAX, XML/A, ASSL y TMSL. La compatibilidad con estos idiomas puede variar según el tipo de modelo. Si debe tener en cuenta requisitos del lenguaje de scripting y consulta, revise la lista siguiente.  
  
-   Los libros de PowerPivot usan DAX para los cálculos y DAX o MDX para las consultas.  
  
-   Las bases de datos modelo tabulares admiten los cálculos DAX, consultas DAX y consultas MDX. Esto es cierto en todos los niveles de compatibilidad. Los lenguajes de script son ASSL (en XMLA) para los niveles de compatibilidad 1050-1103 y TMSL (en XMLA) para el nivel de compatibilidad 1200.  
  
-   Las bases de datos de modelo multidimensionales admiten los cálculos MDX y las consultas MDX así como ASSL.  
  
-   Los modelos de minería de datos admiten DMX y ASSL.  
  
-   Analysis Services PowerShell se puede usar con los modelos y bases de datos tabulares y multidimensionales.  
  
 Todas las bases de datos admiten XML/A. Vea [Referencia del lenguaje de expresiones y consultas &#40;Analysis Services&#41;](../Topic/Query%20and%20Expression%20Language%20Reference%20\(Analysis%20Services\).md) y [Guía del desarrollador (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md) para obtener más información.  
  
##  <a name="a-namebkmkseca-security-features"></a><a name="bkmk_sec"></a> Características de seguridad  
 Todas las soluciones de Analysis Services se pueden proteger en la base de datos. Las opciones de seguridad más específicas varían según el modo. Si debe tener en cuenta requisitos de configuración de seguridad específicos en su solución, revise la lista siguiente para asegurarse de que el nivel de seguridad que desea se admite en el tipo de solución que desea crear:  
  
-   Los libros de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] se protegen en el nivel de archivo, con los permisos de SharePoint.  
  
-   Las bases de datos modelo tabulares pueden utilizar la seguridad de nivel de fila, mediante los permisos basados en roles de Analysis Services.  
  
-   Las bases de datos modelo multidimensionales pueden utilizar la seguridad de nivel de celda y dimensión, mediante los permisos basados en roles de Analysis Services.  
  
 Los libros de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] pueden restaurarse en un servidor de modo tabular. Una vez que se restaura el archivo, se separa de SharePoint, lo que hace posible usar todas las características de modelado tabular, incluida la seguridad del nivel de fila.  
  
##  <a name="a-namebkmkdesignera-design-tools"></a><a name="bkmk_designer"></a> Herramientas de diseño  
 Los conocimientos sobre el modelado de datos y la capacidad técnica pueden variar enormemente según los usuarios encargados de generar modelos analíticos. Si debe tener en cuenta el conocimiento de la herramienta o la experiencia del usuario en su solución, compare las experiencias siguientes para la creación del modelo.  
  
|Herramienta de modelado|Cómo se utiliza|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Se utiliza para crear soluciones tabulares, multidimensionales y de minería de datos. Este entorno de creación utiliza el shell de Visual Studio para proporcionar áreas de trabajo, paneles de propiedades y la navegación de objetos. Los usuarios que ya la utilizan en Visual Studio probablemente preferirán esta herramienta para crear aplicaciones de Business Intelligence.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel|Se usa para crear un libro [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que implementará después en una granja de SharePoint que tenga una instalación de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel tiene un área de trabajo de aplicación independiente que se abre con Excel. Utiliza las mismas metáforas visuales (páginas con pestañas, diseño de cuadrícula y barra de fórmulas) que Excel. Los usuarios que sean expertos en Excel preferirán esta herramienta en lugar de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].|  
  
##  <a name="a-namebkmkclienta-client-application-support"></a><a name="bkmk_client"></a> Compatibilidad con aplicaciones de cliente  
 Si utiliza Reporting Services, la disponibilidad de las características de informe varía según las ediciones y los modos de servidor. Por esta razón, el tipo de informe que desea generar puede influir en el modo de servidor que elige instalar.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], una herramienta de creación de Reporting Services que se ejecuta en SharePoint, está disponible en un servidor de informes implementado en una granja de servidores de SharePoint 2010. El único tipo de origen de datos que se puede usar con este informe es una base de datos modelo tabular de Analysis Services o un libro [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Esto significa que debe tener un servidor en modo tabular o un servidor [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint para hospedar el origen de datos que usa este tipo de informe. No puede utilizar un modelo multidimensional como origen de datos para un informe de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . Debe crear una conexión de modelo semántico de BI [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] o un origen de datos compartido de Reporting Services para usarlo como origen de datos en un informe de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] .  
  
 El Generador de informes y el Diseñador de informes pueden usar cualquier base de datos de Analysis Services, incluidos los libros [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que se hospedan en [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint.  
  
 Los informes de tabla dinámica de Excel se admiten en todas las bases de datos de Analysis Services. La funcionalidad de Excel es la misma si usa una base de datos tabular, una base de datos multidimensional o un libro [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , aunque la reescritura se admite solamente en las bases de datos multidimensionales.  
  
 Los paneles de PerformancePoint pueden conectarse a todas las bases de datos de Analysis Services, incluidos los libros [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Para obtener más información, vea [Crear conexiones de datos (servicios de PerformancePoint)](http://go.microsoft.com/fwlink/?linkdID=218155).  
  
##  <a name="a-namebkmkdeploymentmodea-server-deployment-modes-for-multidimensional-and-tabular-solutions"></a><a name="bkmk_deploymentmode"></a> Modos de implementación de servidor para soluciones multidimensionales y tabulares  
 Una instancia de Analysis Services se instala en uno de los tres modos que establece el contexto operativo del servidor. El modo del servidor que instale determinará el tipo de soluciones que se pueden implementar en ese servidor. La arquitectura de memoria y de almacenamiento constituye la diferencia principal entre los modos, pero hay otras diferencias. Los tres modos de servidor se describen brevemente en la tabla siguiente. Para obtener más información, vea [Determinar el modo de servidor de una instancia de Analysis Services](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
|Modo de implementación|Descripción|  
|---------------------|-----------------|  
|0: multidimensional y minería de datos|Ejecuta soluciones de minería de datos y multidimensionales que se implementan en una instancia predeterminada de Analysis Services. El modo 0 de implementación es el valor predeterminado para una instalación de Analysis Services.|  
|1: [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint|Para el acceso a datos [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , Analysis Services es un componente interno de una instalación de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint. Analysis Services se instala en el modo 1 de implementación y lo usan exclusivamente los servicios [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] en un entorno de SharePoint.|  
|2: tabular|Ejecuta las soluciones tabulares en una instancia independiente de Analysis Services configurada para el modo 2 de implementación.|  
  
 Vea [Instalar Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md) para obtener más información.  
  
##  <a name="a-namebkmksharepointa-sharepoint-requirements"></a><a name="bkmk_sharePoint"></a> Requisitos de SharePoint  
 SQL Server se integra con SharePoint agregando compatibilidad para el acceso a datos [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] y el acceso a datos tabulares. La inversión en la integración de SharePoint y SQL Server crece cuando se maximiza el número de características utilizadas de cada producto. Si tiene SharePoint, puede instalar SQL Server [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint para habilitar el acceso a datos [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] y obtener los archivos de conexión .bism de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] usados para tener acceso a las bases de datos tabulares que se ejecutan en una instancia externa de Analysis Services en un servidor de red.  
  
 Los informes Power View, que usan las bases de datos tabulares y [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] como origen de datos, son una característica de SharePoint proporcionada por SQL Server y una característica integrada de Excel. Aunque las bases de datos tabulares se ejecutan en una instancia de Analysis Services fuera de SharePoint, los datos se usan en los informes de Power View que se ejecutan en SharePoint.  
  
 Si no usa SharePoint, aún puede usar [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel para crear libros [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , pero no tendrá una experiencia de visualización de datos coherente. Cada usuario del libro debe descargar y ver cada libro de Excel mediante el complemento [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel para conseguir la interacción y la exploración de datos con segmentaciones, filtros y tablas dinámicas. Si no, la visualización del libro se limita a los datos estáticos tal cual aparecen cuando abre el libro.  
  
 Las soluciones tabulares, multidimensionales y de minería de datos se ejecutan en las instancias de Analysis Services en una red, sin dependencia de SharePoint.  
  
##  <a name="a-namebkmkexta-programmability-and-extensibility-support"></a><a name="bkmk_ext"></a> Compatibilidad con la programación y la extensibilidad  
 Aunque hay compatibilidad para desarrolladores de Power BI, no hay compatibilidad para desarrolladores de libros [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Si usa libros [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], debe usar las aplicaciones cliente y de servidor integradas como parte de la solución. La programación en Excel y en SharePoint son las únicas opciones.  
  
 Para Power BI, consulte [Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/).  
  
 Las soluciones tabulares solo admiten un archivo model.bim por solución, lo que significa que todo el trabajo debe hacerse en un solo archivo. Es posible que los equipos de desarrollo acostumbrados a trabajar con varios proyectos en una única solución tengan que revisar cómo trabajan para generar una solución tabular compartida.  
  
 Las soluciones tabulares del nivel de compatibilidad 1200 se asignan a un nuevo modelo de objetos que usa metadatos tabulares. Los modelos tabulares anteriores y todos los modelos multidimensionales usan metadatos multidimensionales como descriptores. Se recomienda actualizar al nivel de compatibilidad 1200 los modelos tabulares anteriores para poder usar los espacios de nombres tabulares en AMO para código y scripts personalizados.  
  
 Consulte [Guía del desarrollador (Analysis Services)](https://msdn.microsoft.com/library/bb500153.aspx) para obtener más información.  
  
##  <a name="a-namebkmknexta-next-step-build-a-solution"></a><a name="bkmk_Next"></a> Siguiente paso: compilar una solución  
 Ahora que conoce los fundamentos de una comparación de las soluciones, siga los tutoriales para conocer los pasos que permiten crear cada una. Los siguientes vínculos señalan a tutoriales que explican los pasos.  
  
-   Crear un modelo de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]. Consulte [Introducción a Power Pivot en Microsoft Excel](https://support.office.com/article/Get-started-with-Power-Pivot-in-Microsoft-Excel-fdfcf944-7876-424a-8437-1a6c1043a80b).  
  
-   Crear un modelo tabular. Consulte [Creación de modelos tabulares &#40;Tutorial de Adventure Works&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
-   Generar un modelo multidimensional. Consulte [Creación de modelos multidimensionales &#40;Tutorial de Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
-   Generar un modelo de minería de datos. Consulte [Tutorial básico de minería de datos](../Topic/Basic%20Data%20Mining%20Tutorial.md).  
  
## <a name="see-also"></a>Vea también  
 [Administración de una instancia de Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)   
 [Novedades de Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     
 [Novedades de PowerPivot](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [Conexión del modelo semántico de BI de Power Pivot &#40;.bism&#41;](../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md)  
  
  