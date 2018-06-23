---
title: Comparar soluciones tabulares y multidimensionales (SSAS) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5cfb7c473e16dde04a87a05e3d727d161c62583
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108479"
---
# <a name="comparing-tabular-and-multidimensional-solutions-ssas"></a>Comparar soluciones tabulares y multidimensionales (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona dos enfoques distintos para el modelado de datos: tabular y multidimensional. Aunque existe una superposición significativa entre ellos, también hay diferencias importantes que influirán en su decisión sobre cómo avanzar. En este tema se ofrecen comparaciones de características y se explica cómo cada enfoque aborda los requisitos de proyecto comunes. Por ejemplo, si la compatibilidad de un origen de datos concreto es una consideración fundamental, la sección sobre orígenes de datos puede servirle de guía para tomar la decisión sobre qué enfoque de modelado usar.  
  
 En este tema se incluyen las secciones siguientes:  
  
-   [Información general de modelado en Analysis Services](#bkmk_overview)  
  
-   [Compatibilidad del origen de datos según el tipo de solución](#bkmk_ds)  
  
-   [Características del modelo](#bkmk_models)  
  
-   [Tamaño del modelo](#bkmk_modelsize)  
  
-   [Programabilidad y experiencia del desarrollador](#bkmk_ext)  
  
-   [Compatibilidad con lenguajes de Scripting y consulta](#bkmk_lang)  
  
-   [Compatibilidad con características de seguridad](#bkmk_sec)  
  
-   [Herramientas de diseño](#bkmk_designer)  
  
-   [Cliente y aplicaciones de informes](#bkmk_client)  
  
-   [Plataformas de hospedaje](#bkmk_sharePoint)  
  
-   [Modos de implementación de servidor para las soluciones multidimensionales y tabulares](#bkmk_deploymentmode)  
  
-   [Siguiente paso: Crear una solución](#bkmk_Next)  
  
 Puede encontrar información adicional en este artículo técnico de MSDN: [Choosing a Tabular or Multidimensional Modeling Experience in SQL Server 2012 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=251588).  
  
##  <a name="bkmk_overview"></a> Información general de modelado en Analysis Services  
 Analysis Services proporciona una experiencia de desarrollo de modelo, así como la implementación de modelos a través de base de datos hospedada en una instancia de Analysis Services. Se incluyen los tipos de modelos tabular y multidimensional. Como cabría esperar, el hospedaje de base de datos es compatible con las soluciones tabulares y multidimensionales que cree, pero también incluye PowerPivot para SharePoint.  
  
 PowerPivot para SharePoint es *Analysis Services en modo SharePoint*, donde Analysis Services funciona como un servicio adjuntos a SharePoint, lo que ayuda a alojar y administrar modelos de datos de Excel creados anteriormente en Excel y guardados en SharePoint. La función de Analysis Services en este contexto es cargar el modelo de datos en memoria, actualizar los datos de orígenes de datos externos y ejecutar consultas en el modelo. En esta configuración, Analysis Services funciona en segundo plano. Todas las solicitudes y conexiones a Analysis Services las realiza SharePoint, y sólo cuando un libro de Excel contiene un modelo de datos (los modelos de datos son opcionales en los libros de Excel). Si la creación de un modelo de datos en Excel y el hospedaje en SharePoint, se ajusta a los requisitos del proyecto, consulte [Power Pivot: análisis de datos eficaz y modelado de datos en Excel](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b) y [PowerPivot para SharePoint &#40;SSAS &#41; ](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md) para obtener más información.  
  
> [!NOTE]  
>  Los modelos de datos de Excel y los modelos tabulares son similares en su arquitectura. Puede importar un modelo de datos de Excel en un modelo tabular si necesita admitir grandes cantidades de datos o usar otras características del modelo que no están disponibles en Excel.  
  
 Las soluciones tabulares y multidimensionales se generan con [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] y están diseñados para proyectos BI corporativos que se ejecutan en una independiente [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instancia. Ambas soluciones producen bases de datos analíticas de alto rendimiento que se integran con facilidad con informes de Reporting Services, Excel y otras aplicaciones BI desde aplicaciones de Microsoft y de otros fabricantes. Ambas soluciones como resultado las bases de datos independiente que se pueden utilizar cualquier aplicación cliente compatible con Analysis Services.  
  
 En alto nivel, las diferencias entre los modelos tabulares y multidimensionales se pueden clasificar como sigue:  
  
-   Las soluciones multidimensionales y de minería de datos usan construcciones de modelado OLAP (cubos y dimensiones) y almacenamiento MOLAP, ROLAP u HOLAP que usa el disco como almacenamiento de datos principal para los datos previamente agregados.  
  
-   Las soluciones tabulares usan construcciones de modelado relacional como tablas y relaciones para modelar los datos y el motor de análisis en memoria para almacenarlos y calcularlos. La mayor parte del modelo, si no en su totalidad, se almacena en RAM y suele ser mucho más rápido que su homólogo multidimensional.  
  
 Para los proyectos nuevos, tenga en cuenta en primer lugar el método tabular. Se agiliza el diseño, la prueba y la implementación; y funcionará mejor con las aplicaciones BI de autoservicio más recientes de Microsoft.  
  
##  <a name="bkmk_ds"></a> Compatibilidad del origen de datos según el tipo de solución  
 Los modelos multidimensionales y tabulares usan datos importados de orígenes externos. La mayoría de los desarrolladores usan un almacén de datos, pensado para ser compatible con estructuras de datos para la elaboración de informes, como el origen de datos principal detrás de un modelo. El almacén de datos se suele basar en un esquema de estrella o copo de nieve, y se usa SSIS para cargar datos de soluciones OLTP en el almacén de datos. El modelado es más sencillo cuando se utiliza un almacén de datos como origen de datos back-end.  
  
|**Vínculo**|**Resumen de opciones admitidas**|  
|--------------|--------------------------------------|  
|[Orígenes de datos admitidos &#40;SSAS Multidimensional&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)|Los modelos multidimensionales utilizan datos de orígenes de datos relacionales.|  
|[Orígenes de datos compatibles &#40;SSAS Tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md)|Los modelos tabulares admiten una gama más amplia de orígenes de datos, incluidos archivos sin formato, fuentes de datos y orígenes de datos a los que se obtiene acceso a través de proveedores de datos ODBC.|  
  
 Ambos enfoques de modelado pueden usar datos de varios orígenes de datos en el mismo modelo.  
  
 Si la solución requiere almacenar datos del modelo fuera del modelo en la base de datos relacional (una técnica que se utiliza cuando los requisitos de tamaño de datos son especialmente grandes), el tipo de origen de datos debe ser una base de datos relacional de SQL Server. Tanto el almacenamiento ROLAP para modelos multidimensionales como DirectQuery para modelos tabulares tienen este requisito.  
  
 **Tamaño de los datos**  
  
 Tanto las soluciones tabulares como las multidimensionales usan la compresión de datos que reduce el tamaño de la base de datos de Analysis Services en relación con el almacenamiento de datos desde el que importa los datos. Dado que la compresión real variará en función de las características de los datos subyacentes, no hay ninguna manera de saber con precisión cuánto espacio de memoria y de disco requerirá una solución después de procesar los datos y usarse en consultas. Una estimación que utilizan numerosos desarrolladores de Analysis Services es que el almacenamiento principal de una base de datos multidimensional es aproximadamente de un tercio del tamaño de los datos originales.  
  
 Las bases de datos tabulares puede obtener a veces mayor cantidades de compresión, cerca de una décima de tamaño, especialmente si la mayor parte de los datos se importan de las tablas de hechos. Para las tabulares, los requisitos de memoria serán mayores que el tamaño de los datos en el disco debido a las estructuras de datos adicionales que se crean cuando la base de datos tabular se carga en memoria. Con carga, es previsible que tanto los requisitos de memoria como los de disco para cualquier tipo de solución aumenten mientras Analysis Services almacena en caché los datos, los almacena, los examina y los consulta.  
  
 Para algunos proyectos, los requisitos de datos pueden ser tan grandes que se conviertan en un factor que tener en cuenta al elegir entre los tipos de modelos. Si los datos que necesita cargar tienen un tamaño de muchos terabytes, una solución tabular podría no cumplir los requisitos si la memoria disponible no puede contener los datos. Hay una opción de paginación que intercambia los datos en memoria en el disco, pero si las cantidades de datos son muy grandes se hospedan mejor en soluciones multidimensionales. Las bases de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] más grandes de producción son hoy multidimensionales. Para obtener más información sobre las opciones de paginación de memoria para las soluciones tabulares, vea [propiedades de memoria](server-properties/memory-properties.md). Para obtener más información acerca de cómo escalar una solución multidimensional, vea [Consulta con ampliación horizontal de Analysis Services con bases de datos de solo lectura](http://go.microsoft.com/fwlink/?LinkId=251711).  
  
##  <a name="bkmk_models"></a> Características de modelo  
 En la tabla siguiente se resume la disponibilidad de características en el nivel de modelo. Si ya instaló Analysis Services, puede utilizar esta información para conocer las capacidades del modo de servidor que instaló. Si ya conoce las características de modelo de Analysis Services y sus requisitos empresariales incluyen una o varias de estas características, puede revisar esta lista para asegurarse de que la característica que desea utilizar está disponible en el tipo de modelo que tiene previsto crear.  
  
 Para obtener más información acerca de la comparación de las características según el enfoque de modelado, vea el artículo técnico sobre la [elección de una experiencia tabular o multidimensional de modelado en SQL Server 2012 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=251588) , en MSDN.  
  
> [!NOTE]  
>  El modelado tabular se admite en ediciones concretas de SQL Server. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
||||  
|-|-|-|  
||**Multidimensional**|**Tabular**|  
|Acciones|[Sí](multidimensional-models/actions-in-multidimensional-models.md)|no|  
|Objetos de agregación|[Sí](multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)|no|  
|Medidas calculadas|[Sí](multidimensional-models/create-calculated-members.md)|Sí|  
|Ensamblados personalizados|[Sí](multidimensional-models/multidimensional-model-assemblies-management.md)|no|  
|Resúmenes personalizados|Sí|no|  
|Distinct Count|[Sí](multidimensional-models/use-aggregate-functions.md)|Sí (mediante DAX) *|  
|Obtención de detalles|[Sí](multidimensional-models/actions-in-multidimensional-models.md)|Sí|  
|Jerarquías|[Sí](multidimensional-models/user-defined-hierarchies-create.md)|Sí|  
|KPI|[Sí](multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|Sí|  
|Grupos de medida vinculados|[Sí](multidimensional-models/linked-measure-groups.md)|no|  
|Relaciones varios a varios|[Sí](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)|no|  
|Jerarquías de elementos primarios y secundarios|[Sí](multidimensional-models/parent-child-dimension.md)|Sí (mediante DAX)|  
|Particiones|[Sí](tabular-models/partitions-ssas-tabular.md)|  
|perspectivas|[Sí](multidimensional-models/perspectives-in-multidimensional-models.md)|[Sí](tabular-models/partitions-ssas-tabular.md)|  
|Medidas de suma parcial|[Sí](multidimensional-models/define-semiadditive-behavior.md)|Sí (mediante DAX)|  
|Translations|[Sí](multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|no|  
|Jerarquías definidas por el usuario|[Sí](multidimensional-models/user-defined-hierarchies-create.md)|Sí|  
|Reescritura|[Sí](multidimensional-models/set-partition-writeback.md)|no|  
  
 * Si la solución debe admitir un gran número de recuentos distintivos (por ejemplo, muchos millones de identificadores de cliente), considere la posibilidad de Tabular en primer lugar. Suele tener un mejor rendimiento en esta situación. Vea la sección sobre recuentos distintivos en las notas del producto, [Caso práctico de Analysis Services: uso de modelos tabulares en soluciones comerciales a gran escala](http://msdn.microsoft.com/library/dn751533.aspx).  
  
##  <a name="bkmk_modelsize"></a> Tamaño del modelo  
 El tamaño del modelo, en cuanto al número total de objetos, no varía según el tipo de la solución. Sin embargo, las herramientas de diseño que se usan para compilar cada solución varían en el modo en que se adaptan a trabajar con un gran número de objetos. Un modelo mayor es algo más fácil de crear en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] porque proporciona más funciones para los objetos de diagramas y listas por tipo del Explorador de objetos y el explorador de soluciones.  
  
 Los modelos muy grandes, que constan de muchos cientos de tablas o dimensiones, a menudo se generan mediante programación en Visual Studio y no en las herramientas de diseño. Para obtener más información sobre el número máximo de objetos en un modelo, vea [especificaciones de capacidad máxima &#40;Analysis Services&#41;](multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md).  
  
##  <a name="bkmk_ext"></a> Programabilidad y experiencia del desarrollador  
 Para los modelos tabulares y multidimensionales, hay un modelo de objetos compartido para ambas modalidades. AMO y ADOMD.NET admiten ambos modos. Ninguna de las dos bibliotecas cliente se ha revisado para las construcciones tabulares por lo que deberá entender el modo en que las estructuras multidimensionales y tabulares y las convenciones de nomenclatura se relacionan entre sí. En primer lugar, revise el ejemplo de programación de AMO a tabular para obtener la programación de AMO con un modelo tabular. Para obtener más información, descargue el ejemplo del [sitio web de codeplex](http://go.microsoft.com/fwlink/?LinkID=221036).  
  
 Las soluciones tabulares solo admiten un archivo model.bim por solución, lo que significa que todo el trabajo debe hacerse en un solo archivo. Es posible que los equipos de desarrollo acostumbrados a trabajar con varios proyectos en una única solución tengan que revisar cómo trabajan para generar una solución tabular compartida.  
  
##  <a name="bkmk_lang"></a> Compatibilidad con lenguaje de scripting y consulta  
 Analysis Services incluye MDX, DMX, DAX, XML/A y ASSL. La compatibilidad con estos idiomas varía ligeramente según el tipo de modelo. Si debe tener en cuenta requisitos del lenguaje de scripting y consulta, revise la lista siguiente.  
  
-   Las bases de datos modelo tabulares admiten los cálculos DAX, consultas DAX y consultas MDX.  
  
-   Las bases de datos de modelo multidimensionales admiten los cálculos MDX y las consultas MDX así como ASSL.  
  
-   Los modelos de minería de datos admiten DMX y ASSL.  
  
-   Analysis Services PowerShell se admite para la administración de la base de datos y el servidor. El tipo de modelo (o el modo de servidor) no influye en el uso de los cmdlets de PowerShell.  
  
 Todas las bases de datos admiten XML/A.  
  
##  <a name="bkmk_sec"></a> Compatibilidad con características de seguridad  
 Todas las soluciones de Analysis Services se pueden proteger en la base de datos. Las opciones de seguridad más específicas varían según el modo. Si debe tener en cuenta requisitos de configuración de seguridad específicos en su solución, revise la lista siguiente para asegurarse de que el nivel de seguridad que desea se admite en el tipo de solución que desea crear:  
  
-   Las bases de datos modelo tabulares pueden utilizar la seguridad de nivel de fila, mediante los permisos basados en roles de Analysis Services.  
  
-   Las bases de datos modelo multidimensionales pueden utilizar la seguridad de nivel de celda y dimensión, mediante los permisos basados en roles de Analysis Services.  
  
 Los modelos de datos de Excel pueden restaurarse en un servidor de modo tabular. Una vez que se restaura el archivo, se separa de SharePoint (suponiendo que se ha restaurado desde una ubicación de SharePoint), lo que permite usar casi todas las características tabulares de modelado, incluida la seguridad del nivel de fila. La única característica de modelado tabular que no puede usar en un libro restaurado son las tablas vinculadas.  
  
##  <a name="bkmk_designer"></a> Herramientas de diseño  
 Los conocimientos sobre el modelado de datos y la capacidad técnica pueden variar enormemente según los usuarios encargados de generar modelos analíticos. Si debe tener en cuenta el conocimiento de la herramienta o la experiencia del usuario en su solución, compare las experiencias siguientes para la creación del modelo.  
  
|**Herramienta de modelado**|**Cómo se utiliza**|  
|-----------------------|------------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Se utiliza para crear soluciones tabulares, multidimensionales y de minería de datos. Este entorno de creación utiliza el shell de Visual Studio para proporcionar áreas de trabajo, paneles de propiedades y la navegación de objetos. Los usuarios que ya la utilizan en Visual Studio probablemente preferirán esta herramienta para crear aplicaciones de Business Intelligence. Vea [herramientas y aplicaciones utilizadas en Analysis Services](tools-and-applications-used-in-analysis-services.md) para obtener más información.|  
|Excel 2013 y posterior, con el complemento PowerPivot para Excel|PowerPivot para Excel es una herramienta que se utiliza para editar y mejorar un modelo de datos de Excel. Tiene un área de trabajo de aplicación independiente que se abre sobre Excel, pero utiliza las mismas metáforas visuales (páginas con pestañas, diseño de cuadrícula y barra de fórmulas) que Excel. Los usuarios que suelen ser expertos en Excel preferirán esta herramienta sobre [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Consulte [Power Pivot: análisis de datos eficaz y modelado de datos en Excel](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b).|  
  
##  <a name="bkmk_client"></a> Cliente y aplicaciones de informes  
 En versiones anteriores, la elección del tipo de modelo influía en las aplicaciones cliente que se podían utilizar, pero esta distinción ha disminuido con el tiempo. Los modelos tabulares y multidimensionales ofrecen una compatibilidad prácticamente equivalente con respecto a las aplicaciones cliente que se conectan a datos de Analysis Services. En la tabla siguiente se muestra una lista de las aplicaciones de cliente de Microsoft que pueden utilizarse con modelos de datos de Analysis Services.  
  
|**Aplicación**|**Descripción**|  
|---------------------|---------------------|  
|Informes de tabla dinámica de Excel|La funcionalidad de Excel es la misma para los modelos tabulares y multidimensionales, aunque solo se admite la reescritura (una capacidad de Analysis Services que implementa Excel) en el caso de modelos multidimensionales.|  
|Informes RDL de Reporting Services|Los informes RDL, creados en el Generador de informes o en el Diseñador de informes, pueden utilizar cualquier modelo de Analysis Services, así como modelos de datos de Excel alojados en PowerPivot para SharePoint.|  
|Paneles de PerformancePoint|En SharePoint, los paneles de PerformancePoint pueden conectarse a todas las bases de datos de Analysis Services, incluidos los modelos de datos de Excel. Para obtener más información, vea [Crear conexiones de datos (servicios de PerformancePoint)](http://go.microsoft.com/fwlink/?linkdID=218155).|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] en los sitios Office 365 o Power BI|Sólo modelos tabulares.|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] en SharePoint local|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], como aplicación ClickOnce desde SharePoint, puede utilizar un cubo o un modelo tabular de Analysis Services.|  
  
##  <a name="bkmk_deploymentmode"></a> Modos de implementación de servidor para soluciones multidimensionales y tabulares  
 Una instancia de Analysis Services se instala en uno de los tres modos que establece el contexto operativo del servidor. El modo del servidor que instale determinará el tipo de soluciones que se pueden implementar en ese servidor. La arquitectura de memoria y de almacenamiento constituye la diferencia principal entre los modos, pero hay otras diferencias. Los tres modos de servidor se describen brevemente en la tabla siguiente. Para obtener más información, vea [Determinar el modo de servidor de una instancia de Analysis Services](instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
|Modo de implementación|Descripción|  
|---------------------|-----------------|  
|0: multidimensional y minería de datos|Ejecuta soluciones de minería de datos y multidimensionales que se implementan en una instancia predeterminada de Analysis Services. El modo 0 de implementación es el valor predeterminado para una instalación de Analysis Services. Para obtener más información, consulte [instalar Analysis Services en el modo de minería de datos y Multidimensional](../../2014/sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md).|  
|1: PowerPivot para SharePoint|Analysis Services es un componente interno de SharePoint, lo que permite tener acceso al modelo de datos de Excel. Analysis Services se instala en modo de implementación 1 y acepta solicitudes únicamente de Excel Services en un entorno de SharePoint. Para obtener más información, vea [PowerPivot for SharePoint 2010 Installation](../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).|  
|2: tabular|Ejecuta las soluciones tabulares en una instancia independiente de Analysis Services configurada para el modo 2 de implementación. Para obtener más información, consulte [instalar Analysis Services en modo Tabular](instances/install-windows/install-analysis-services.md).|  
  
 Tenga en cuenta que los modelos de servidor no son intercambiables. Durante la instalación deberá elegir un modo de funcionamiento del servidor. Deberá instalar varias instancias, una para cada modo de servidor, para poder admitir todas las cargas de trabajo.  
  
##  <a name="bkmk_sharePoint"></a> Plataformas de hospedaje  
 Microsoft dispone de varias metodologías disponibles para hospedar datos, aplicaciones, informes y colaboración. En esta sección trataremos la interoperabilidad de Analysis Services con respecto a cada plataforma de hospedaje.  
  
|**Plataforma**|**Descripción**|  
|------------------|---------------------|  
|Microsoft Azure|Puede ejecutar cualquier versión y edición compatibles de Analysis Services en una máquina Virtual de Azure. A diferencia de la base de datos SQL de Azure, que es un servicio de Azure que proporciona prácticamente la misma funcionalidad que un motor de base de datos relacional local, no hay ningún equivalente de Analysis Services en Azure. Instalar, configurar y ejecutar Analysis Services en una VM de Azure son la única opción basada en Azure.|  
|Office 365|Excel Online en Office 365 admite conexiones remotas a modelos tabulares y multidimensionales que se ejecutan en local.|  
|Sitios de Power BI en Office 365|En un sitio de Power BI, los informes de Power View pueden conectarse a modelos de datos tabulares que se ejecutan en local.|  
|Servidores locales (instancias de SQL Server y SharePoint)|Un servidor de base de datos local (es decir, una instancia de SQL Server que tenga instalado Analysis Services) sigue siendo el medio principal de ofrecer disponibilidad de los datos de Analysis Services para informes y aplicaciones cliente. Las soluciones tabulares, multidimensionales y de minería de datos se ejecutan en las instancias de Analysis Services en una red, sin dependencia de SharePoint.<br /><br /> SQL Server se integra con SharePoint agregando compatibilidad para el acceso a datos PowerPivot y el acceso a datos tabulares. La inversión en la integración de SharePoint y SQL Server crece cuando se maximiza el número de características utilizadas de cada producto. Si tiene SharePoint, puede instalar SQL Server PowerPivot para SharePoint para habilitar el acceso a datos PowerPivot y obtener los archivos de conexión .bism de PowerPivot utilizados para tener acceso a las bases de datos tabulares que se ejecutan en una instancia externa de Analysis Services en un servidor de red.<br /><br /> Si tiene SQL Server y SharePoint, puede admitir la siguiente combinación de servicios y aplicaciones:<br /><br /> Modelos de Analysis Services (tabulares o multidimensionales)<br /><br /> Servicios de SharePoint de nivel intermedio (Servicios de Excel, Reporting Services en SharePoint o servicios en PerformancePoint)<br /><br /> Clientes de explorador o clientes avanzados (Excel) para una exploración y análisis más profundos.|  
  
##  <a name="bkmk_Next"></a> Siguiente paso: compilar una solución  
 Ahora que conoce los fundamentos de una comparación de las soluciones, siga los tutoriales para conocer los pasos que permiten crear cada una. Los siguientes vínculos señalan a tutoriales que explican los pasos.  
  
-   Generar un modelo tabular mediante la [Creación de modelos tabulares &#40;tutorial de Adventure Works&#41;](tabular-modeling-adventure-works-tutorial.md).  
  
-   Generar un modelo multidimensional mediante la [Creación de modelos multidimensionales &#40;tutorial de Adventure Works&#41;](multidimensional-modeling-adventure-works-tutorial.md).  
  
-   Generar un modelo de minería de datos utilizando el [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
-   Generar un modelo de PowerPivot mediante el [Tutorial de PowerPivot para Excel](http://go.microsoft.com/fwlink/?LinkId=251135).  
  
## <a name="see-also"></a>Vea también  
 [Administración de una instancia de Analysis Services](instances/analysis-services-instance-management.md)   
 [Novedades de Analysis Services y Business Intelligence](what-s-new-in-analysis-services.md)   
 [' S New &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)   
 [Novedades de PowerPivot](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [Ayuda de PowerPivot para SQL Server 2012](http://go.microsoft.com/fwlink/?LinkID=220946)   
 [Conexión de modelo semántico de BI PowerPivot &#40;.bism&#41;](power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
  