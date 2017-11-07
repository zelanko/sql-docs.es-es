---
title: Comparar soluciones tabulares y multidimensionales (SSAS) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 06/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dba56641beaa8c22bc1bc0552d51737b81f4128d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="comparing-tabular-and-multidimensional-solutions"></a>Comparar soluciones tabulares y multidimensionales
  SQL Server Analysis Services proporciona varios enfoques para crear un modelo semántico de business intelligence: Tabular, Multidimensional y Power Pivot para SharePoint.
  
 El uso de más de un método permite una experiencia de modelado adaptada a los diferentes requisitos empresariales y del usuario. El modelo multidimensional es una tecnología consolidada basada en estándares abiertos que adoptan muchos proveedores de software de BI, pero puede ser difícil de dominar. El modelo tabular ofrece un enfoque de modelado relacional que muchos desarrolladores consideran más intuitivo. El modelo PowerPivot es todavía más sencillo, ya que ofrece el modelado visual de datos en Excel, con compatibilidad de servidor proporcionada a través de SharePoint.  
  
 Todos los modelos se implementan como bases de datos que se ejecutan en una instancia de Analysis Services, a las que tienen acceso las herramientas de cliente mediante un único conjunto de proveedores de datos. Se visualizan en informes interactivos y estáticos a través de Excel, Reporting Services, Power BI y herramientas de BI de otros proveedores.  
  
 Soluciones tabulares y multidimensionales se generan con SSDT y están diseñadas para proyectos BI corporativos que se ejecutan en una independiente [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instancia local y para los modelos tabulares, una [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) server en el en la nube. Ambas soluciones producen bases de datos analíticas de alto rendimiento que se integran fácilmente con los clientes de BI. Con todo, cada solución difiere en cómo se crea, se usa y se implementa. En la mayor parte de este tema se comparan estos dos tipos para que pueda identificar el enfoque correcto para su caso.  
  
 Para los nuevos proyectos, generalmente recomendamos los modelos tabulares. Los modelos tabulares son más rápidos diseñar, probar e implementar; y trabajar mejor con las aplicaciones de BI de autoservicio más recientes y los servicios de Microsoft en la nube.  
  
##  <a name="bkmk_overview"></a> Información general de tipos de modelado  
 ¿No está familiarizado con Analysis Services? En la tabla siguiente se enumeran los diferentes modelos, se resume el enfoque y se identifica el vehículo de lanzamiento inicial.  
 
 > [!NOTE]  
>  **Azure Analysis Services** es compatible con los modelos tabulares en los niveles de compatibilidad 1200 y versiones posteriores. Sin embargo, no toda la funcionalidad de creación de modelos tabulares que se describe en este tema se admite en los servicios de análisis de Azure. Al crear e implementar los modelos tabulares a los servicios de análisis de Azure es muy parecida a las ya que es local, es importante comprender las diferencias. Para obtener más información, consulte [¿qué es Azure Analysis Services?](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
  
||||  
|-|-|-|  
|**Tipo**|**Descripción de modelado**|**Publicado**|  
|Tabular|Construcciones de modelado relacional (modelo, tablas, columnas). Internamente, los metadatos se heredan de las construcciones de modelado OLAP (cubos, dimensiones, medidas). El código y los scripts usan metadatos de OLAP.|SQL Server 2012 y posterior (niveles de compatibilidad 1050-1103) <sup>1</sup>|  
|Tabular en SQL Server 2016|Construcciones (modelo, tablas, columnas), articuladas en definiciones de objetos de metadatos tabulares de modelado relacional [Tabular Model Scripting Language (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) y [el modelo de objeto Tabular (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) código.|SQL Server 2016 (nivel de compatibilidad 1200)| 
|Tabular en SQL Server de 2017|Construcciones (modelo, tablas, columnas), articuladas en definiciones de objetos de metadatos tabulares de modelado relacional [Tabular Model Scripting Language (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) y [el modelo de objeto Tabular (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) código.|SQL Server 2017 (nivel de compatibilidad 1400)| 
|Multidimensional|Construcciones de modelado OLAP (cubos, dimensiones, medidas).|SQL Server 2000 y posterior|  
|Power Pivot|Originalmente un complemento, pero ahora totalmente integrado en Excel. Solo modelado visual sobre una infraestructura tabular interna. Puede importar un modelo de Power Pivot en SSDT para crear un nuevo modelo tabular que se ejecute en una instancia de Analysis Services.|A través de Excel y Power Pivot BI Desktop|  
  
 <sup>1</sup> niveles de compatibilidad son significativos en la versión actual debido al motor de metadatos tabulares y soporte técnico para habilitar escenarios características disponibles solo en el nivel superior. Las versiones posteriores admiten niveles de compatibilidad inferiores, pero se recomienda crear nuevos modelos o actualizar los modelos existentes en el nivel más alto de compatibilidad admitido por la versión del servidor.
  
##  <a name="bkmk_models"></a> Características de modelo  
  En la tabla siguiente se resume la disponibilidad de características en el nivel de modelo. Revise esta lista para asegurarse de que la característica que quiere usar está disponible en el tipo de modelo que tiene previsto crear.  
  
|||| 
|-|-|-|
||Multidimensional|Tabular|
|Acciones|Sí|No|
|Agregaciones|Sí|No|
|Columna calculada|No|Sí|  
|Medidas calculadas|Sí|Sí| 
|Tablas calculadas|No|Sí<sup>1</sup>|  
|Ensamblados personalizados|Sí|No|
|Resúmenes personalizados|Sí|No| 
|Miembro predeterminado|Sí|No|  
|Carpetas para mostrar|Sí|Sí<sup>1</sup>|  
|Distinct Count|Sí|Sí (mediante DAX)|
|Obtención de detalles|Sí|Sí (depende de la aplicación cliente)|
|Jerarquías|Sí|Sí|
|KPI|Sí|Sí| 
|Objetos vinculados|Sí|Sí (tablas vinculadas)|
|Expresiones de M|No|Sí<sup>1</sup>|
|Relaciones varios a varios|Sí|No (pero no hay [bidireccional filtros cruzados](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) en niveles de compatibilidad 1200 y versiones posteriores)| 
|Conjuntos con nombre|Sí|No| 
|Jerarquías desiguales|Sí|Sí<sup>1</sup>|  
|Jerarquías de elementos primarios y secundarios|Sí|Sí (mediante DAX)|
|Particiones|Sí|Sí| 
|Perspectivas|Sí|Sí|
|Seguridad de filas|Sí|Sí| 
|Seguridad de nivel de objeto|Sí|Sí<sup>1</sup>|
|Medidas de suma parcial|Sí|Sí| 
|Translations|[Sí](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Sí| 
|Jerarquías definidas por el usuario|Sí|Sí|
|Reescritura|Sí|No| 
  
 <sup>1</sup> vea [Compatibility Level for Tabular los modelos de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) para obtener información sobre las diferencias funcionales entre los niveles de compatibilidad.  
  
##  <a name="bkmk_ds"></a> Consideraciones sobre los datos  
 Los modelos tabulares y multidimensionales usan datos importados de orígenes externos. La cantidad y el tipo de datos que necesita importar puede ser una consideración principal a la hora de decidir qué tipo de modelo se adapta mejor a sus datos.  
  
 **Compresión**  
  
 Tanto las soluciones tabulares como las multidimensionales usan la compresión de datos que reduce el tamaño de la base de datos de Analysis Services en relación con el almacenamiento de datos desde el que importa los datos. Dado que la compresión real variará en función de las características de los datos subyacentes, no hay ninguna manera de saber con precisión cuánto espacio de memoria y de disco requerirá una solución después de procesar los datos y usarse en consultas.  
  
 Una estimación que utilizan numerosos desarrolladores de Analysis Services es que el almacenamiento principal de una base de datos multidimensional es aproximadamente de un tercio del tamaño de los datos originales. Las bases de datos tabulares puede obtener a veces mayor cantidades de compresión, cerca de una décima de tamaño, especialmente si la mayor parte de los datos se importan de las tablas de hechos.  
  
 **Tamaño del modelo y diferencia de recursos (en memoria o disco)**  
  
 El tamaño de una base de datos de Analysis Services está limitado solo por los recursos disponibles para ejecutarla. El tipo de modelo y el modo de almacenamiento también desempeñan un papel importante al determinar el tamaño que puede alcanzar la base de datos.  
  
 Las bases de datos tabulares se ejecutan en memoria o en el modo DirectQuery, que descarga la ejecución de consultas en una base de datos externa. Para realizar análisis en memoria tabular, la base de datos se almacena completamente en la memoria, lo que significa que debe tener suficiente memoria no sólo para cargar todos los datos, sino también estructuras de datos adicionales que se crearon para admitir las consultas.  
  
 DirectQuery se ha renovado en SQL Server 2016, tiene menos restricciones que antes y un mejor rendimiento. El aprovechamiento de la base de datos relacional de back-end para el almacenamiento y la ejecución de consultas hace que la generación de un modelo tabular a gran escala sea más viable que antes.  
  
 Históricamente, las bases de datos más grandes en producción son multidimensionales, con cargas de trabajo de procesamiento y consulta ejecuta de forma independiente en un hardware dedicado, cada uno optimizado para su uso respectivo.  Las bases de datos tabulares se están poniendo al día rápidamente, y los nuevos avances en DirectQuery ayudarán a salvar distancia todavía más.  
  
 Para la consulta y el almacenamiento de datos multidimensional descarga ejecución está disponible a través de ROLAP.   En un servidor de consultas, es posible almacenar en caché conjuntos de filas y paginar los antiguos. El uso eficiente y equilibrado de los recursos de memoria y disco guía suele llevar a los clientes a optar por soluciones multidimensionales.  
  
 Con carga, es previsible que tanto los requisitos de memoria como los de disco para cualquier tipo de solución aumenten mientras Analysis Services almacena en caché los datos, los almacena, los examina y los consulta. Para obtener más información sobre las opciones de paginación de memoria, consulte [Memory Properties](../analysis-services/server-properties/memory-properties.md). Para obtener más información sobre la escala, vea [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 Power Pivot para Excel tiene un límite de tamaño de archivo artificial de 2 gigabytes, impuesto de modo que los libros creados en Power Pivot para Excel se puedan cargar en SharePoint, que establece los límites máximos en el tamaño de carga de archivos. Una de las razones principales para migrar un libro Power Pivot a una solución tabular en una instancia independiente de Analysis Services es sortear la limitación de tamaño del archivo. Para obtener más información sobre cómo configurar el tamaño máximo de carga de archivos, vea [Configuración del tamaño de carga máximo de archivos &#40;PowerPivot para SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Orígenes de datos compatibles**  
  
 Los modelos tabulares pueden importar datos de orígenes de datos relacionales, fuentes de distribución de datos y algunos formatos de documento. También puede usar OLE DB para proveedores de ODBC con modelos tabulares. Los modelos tabulares en el nivel de compatibilidad de 1400 ofrecen un aumento significativo en la gran variedad de orígenes de datos desde el que puede importar desde. Esto es debido a la incorporación de los datos modernos obtener datos de consulta y características en SSDT utilizando el lenguaje de fórmulas de consulta M de importación.   

  Las soluciones multidimensionales pueden importar los datos de orígenes de datos relacionales mediante proveedores administrados y nativos OLE DB.  
  
 Para ver la lista de orígenes de datos externos que puede importar en cada modelo, vea los siguientes temas.  
  
-   [Orígenes de datos compatibles &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  

-   [Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  

  
##  <a name="bkmk_lang"></a> Compatibilidad con lenguaje de scripting y consulta  
 Analysis Services incluye MDX, DMX, DAX, XML/A, ASSL y TMSL. La compatibilidad con estos idiomas puede variar según el tipo de modelo. Si debe tener en cuenta requisitos del lenguaje de scripting y consulta, revise la lista siguiente.  

-   Las bases de datos modelo tabulares admiten los cálculos DAX, consultas DAX y consultas MDX. Esto es cierto en todos los niveles de compatibilidad. Lenguajes de script son ASSL (a través de XMLA) para los niveles de compatibilidad 1050-1103 y TMSL (en XMLA) para el nivel de compatibilidad 1200 y versiones posterior. 

-   Los libros de PowerPivot usan DAX para los cálculos y DAX o MDX para las consultas.  
  
-   Bases de datos de modelo multidimensionales admiten cálculos MDX, consultas MDX, consultas DAX y ASSL. 
  
-   Los modelos de minería de datos admiten DMX y ASSL.  
  
-   Analysis Services PowerShell se puede usar con los modelos y bases de datos tabulares y multidimensionales.  
  
 Todas las bases de datos admiten XML/A. Vea [Referencia del lenguaje de expresiones y consultas &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527) y [Guía del desarrollador (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md) para obtener más información.  
  
##  <a name="bkmk_sec"></a> Características de seguridad  
 Todas las soluciones de Analysis Services se pueden proteger en la base de datos. Las opciones de seguridad más específicas varían según el modo. Si debe tener en cuenta requisitos de configuración de seguridad específicos en su solución, revise la lista siguiente para asegurarse de que el nivel de seguridad que desea se admite en el tipo de solución que desea crear:  

  
-   Las bases de datos de modelo tabular pueden usar seguridad de nivel de fila, con permisos basados en rol.  
  
-   Dimensión y la seguridad de nivel de celda, con permisos basados en rol, pueden utilizar las bases de datos de modelo multidimensional.  

-   Los libros de[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] se protegen en el nivel de archivo, con los permisos de SharePoint.  
  
 Los libros de[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] pueden restaurarse en un servidor de modo tabular. Una vez restaurado el archivo, se separa de SharePoint, lo que le permite usar todas las características de modelado tabular, incluida la seguridad de nivel de fila.  
  
##  <a name="bkmk_designer"></a> Herramientas de diseño  
 Los conocimientos sobre el modelado de datos y la capacidad técnica pueden variar enormemente según los usuarios encargados de generar modelos analíticos. Si debe tener en cuenta el conocimiento de la herramienta o la experiencia del usuario en su solución, compare las experiencias siguientes para la creación del modelo.  
  
|Herramienta de modelado|Cómo se utiliza|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Utilícelo para crear tabulares, multidimensionales y soluciones de minería de datos. Este entorno de creación utiliza el shell de Visual Studio para proporcionar áreas de trabajo, paneles de propiedades y la navegación de objetos. Los usuarios que ya la utilizan en Visual Studio probablemente preferirán esta herramienta para crear aplicaciones de Business Intelligence.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel|Se usa para crear un libro [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que implementará después en una granja de SharePoint que tenga una instalación de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel tiene un área de trabajo de aplicación independiente que se abre con Excel. Utiliza las mismas metáforas visuales (páginas con pestañas, diseño de cuadrícula y barra de fórmulas) que Excel. Los usuarios que sean expertos en Excel preferirán esta herramienta en lugar de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].|  
  
##  <a name="bkmk_client"></a> Compatibilidad con aplicaciones de cliente  
 Las soluciones en general, tabulares y multidimensionales admiten aplicaciones de cliente mediante una o varias de las bibliotecas de cliente de Analysis Services (MSOLAP, AMOMD, ADOMD). Por ejemplo, Excel, Power BI Desktop y aplicaciones personalizadas.   
 
 Si utiliza Reporting Services, la disponibilidad de las características de informe varía según las ediciones y los modos de servidor. Por esta razón, el tipo de informe que desea generar puede influir en el modo de servidor que elige instalar.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], una herramienta de creación de Reporting Services que se ejecuta en SharePoint, está disponible en un servidor de informes implementado en una granja de servidores de SharePoint 2010. El único tipo de origen de datos que se puede usar con este informe es una base de datos modelo tabular de Analysis Services o un libro [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Esto significa que debe tener un servidor en modo tabular o un servidor [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint para hospedar el origen de datos que usa este tipo de informe. No puede utilizar un modelo multidimensional como origen de datos para un informe de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . Debe crear una conexión de modelo semántico de BI [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] o un origen de datos compartido de Reporting Services para usarlo como origen de datos en un informe de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] .  
  
 El Generador de informes y el Diseñador de informes pueden usar cualquier base de datos de Analysis Services, incluidos los libros [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que se hospedan en [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint.  
  
 Los informes de tabla dinámica de Excel se admiten en todas las bases de datos de Analysis Services. La funcionalidad de Excel es la misma si usa una base de datos tabular, una base de datos multidimensional o un libro [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , aunque la reescritura se admite solamente en las bases de datos multidimensionales.  
 
  
  
## <a name="see-also"></a>Vea también  
 [Administración de una instancia de Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)   
 [Novedades de Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     

  
  

