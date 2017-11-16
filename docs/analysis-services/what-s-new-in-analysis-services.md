---
title: "¿Qué &#39; s nuevos en Analysis Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
caps.latest.revision: 97
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 212fbb3618bbccc58ea077d59f15dca3c31ca71f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="what39s-new-in-analysis-services"></a>¿Qué &#39; s nuevos en Analysis Services
SQL Server 2016 Analysis Services incluye muchas mejoras nuevas que proporciona un mejor rendimiento, creación de solución más fácil, administración automatizada de la base de datos, procesamiento de particiones, en paralelo relaciones mejoradas con bidireccional entre el filtrado, y mucho más. En el centro de la mayoría de las mejoras de esta versión se encuentra el nuevo nivel de compatibilidad 1200 para bases de datos de modelo tabular.     

## <a name="azure-analysis-services"></a>Azure Analysis Services
Anunciado en la conferencia de SQL PASS de 2016, Analysis Services está ahora disponible en la nube como un servicio de Azure. **Azure Analysis Services** es compatible con los modelos tabulares en los niveles de compatibilidad 1200 y versiones posteriores. Se admiten todas las traducciones, particiones, seguridad de nivel de fila, relaciones bidireccionales y DirectQuery. Para obtener más información y probar esta función de forma gratuita, consulte [Azure Analysis Services](http://azure.microsoft.com/services/analysis-services/). 

## <a name="whats-new-in-sql-server-2016-service-pack-1-sp1-analysis-services"></a>Novedades de SQL Server 2016 Service Pack 1 (SP1) Analysis Services

[Descargar SQL Server 2016 SP1](http://www.microsoft.com/download/details.aspx?id=54276) 

SQL Server 2016 Service SP1 Analysis Services proporciona un rendimiento y una escalabilidad mejorados gracias al reconocimiento de Non-Uniform Memory Access (NUMA) y la asignación de memoria optimizada basada en **Intel Threading Building Blocks** (Intel TBB). Esta nueva funcionalidad ayuda a reducir el costo total de propiedad (TCO) dando cabida a más usuarios en menos servidores empresariales, pero más eficaces. 

En concreto, SQL Server 2016 SP1 Analysis Services incluye mejoras en estas áreas principales:

-   **Reconocimiento de NUMA** : para conseguir una mejor compatibilidad con NUMA, el motor en memoria VertiPaq de Analysis Services ahora mantiene una cola de trabajo independiente en cada nodo NUMA. Esto garantiza que los trabajos de detección de segmentos se ejecuten en el mismo nodo en el que se asigna la memoria para los datos de los segmentos. Tenga en cuenta que el reconocimiento de NUMA solo está habilitado de forma predeterminada en los sistemas que tienen al menos cuatro nodos NUMA. En los sistemas de dos nodos, los costos de acceso a la memoria asignada de forma remota no suelen garantizar los gastos de administración de datos NUMA.
-   **Asignación de memoria** : Analysis Services ahora cuenta con una mayor aceleración gracias a Intel Threading Building Blocks, un asignador escalable que proporciona bloques de memoria independientes para cada núcleo. A medida que aumenta el número de núcleos, el sistema puede escalarse de manera casi lineal.
-   **Fragmentación de montón** : el asignador escalable basado en Intel TBB también ayuda a mitigar los problemas de rendimiento debido a la fragmentación de montón que se produce con el montón de Windows.

Las pruebas de rendimiento y de escalabilidad muestran unas mejoras considerables en el rendimiento de las consultas al ejecutar SQL Server 2016 SP1 Analysis Services en servidores empresariales de varios nodos.


## <a name="whats-new-in-sql-server-2016-analysis-services"></a>Novedades de SQL Server 2016 Analysis Services

Aunque la mayoría de las mejoras de esta versión son específicas de los modelos tabulares, también se han realizado varias mejoras en los modelos multidimensionales, como la optimización ROLAP de recuento distintivo para orígenes de datos como DB2 y Oracle, la compatibilidad de selección múltiple detallada con Excel 2016 y las optimizaciones de consultas de Excel.    

#### <a name="get-the-latest-tools"></a>Obtenga las herramientas más recientes
Para aprovechar al máximo de todas las mejoras en esta versión, asegúrese de instalar las versiones más recientes de SSDT y SSMS.    
- [Descargar SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)    
- [Descargar SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)   

Si tiene una aplicación personalizada que depende de AMO, es posible que tenga que instalar una versión actualizada de AMO. Para obtener instrucciones, vea [Instalar proveedores de datos de Analysis Services &#40;AMO, ADOMD.NET, MSOLAP&#41;](../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md).    

 #### <a name="technet-virtual-labs-sql-server-2016-analysis-services"></a>Laboratorios virtuales de TechNet: SQL Server 2016 Analysis Services
¿Aprende mejor cuando hace las cosas usted mismo? Siga los procedimientos detallados de [What's New in SQL Server 2016 Analysis Services Virtual Lab](http://vlabs.holsystems.com/vlabs/technet?eng=VLabs&auth=none&src=vlabs&altadd=true&labid=23110&lod=true)(Novedades del laboratorio virtual de SQL Server 2016 Analysis Services).
En este laboratorio, creará y supervisará eventos extendidos (xEvents), actualizará un proyecto tabular al nivel de compatibilidad 1200, trabajará con configuraciones de Visual Studio, implementará nuevas funciones de cálculo, implementará nuevas funciones de relación de tabla, configurará carpetas para mostrar, administrará traducciones del modelo, trabajará con el nuevo Tabular Model Scripting Language (TMSL), trabajará con PowerShell y probará las nuevas funciones del modo DirectQuery.

## <a name="modeling"></a>Modelado    
### <a name="improved-modeling-performance-for-tabular-1200-models"></a>Rendimiento de modelado mejorado para los modelos tabulares 1200    
Para los modelos tabulares 1200, las operaciones de metadatos en SSDT se realizan mucho más rápido que para los modelos tabulares 1100 o 1103. Si se compara, en el mismo hardware, la creación de una relación en un modelo establecido en el nivel de compatibilidad de SQL Server 2014 (1103) con 23 tablas tarda 3 segundos, mientras que la misma relación en un modelo creado que se ha establecido en el nivel de compatibilidad 1200 tarda menos de un segundo.    
### <a name="project-templates-added-for-tabular-1200-models-in-ssdt"></a>Plantillas de proyecto agregadas para los modelos tabulares 1200 en SSDT    
Con esta versión, ya no necesita dos versiones de SSDT para generar proyectos BI y relacionales. [SQL Server Data Tools para Visual Studio 2015](http://msdn.microsoft.com/library/mt204009.aspx) agrega plantillas de proyecto para soluciones de Analysis Services, incluidos los **proyectos tabulares de Analysis Services** usados para la creación de modelos en el nivel de compatibilidad 1200. Se incluyen otras plantillas de proyecto de Analysis Services para soluciones de minería de datos y multidimensionales, pero al mismo nivel funcional (1100 o 1103) que en versiones anteriores.    
### <a name="display-folders"></a>Carpetas para mostrar
Ahora hay disponibles carpetas para mostrar para los modelos tabulares 1200. Definidas en SQL Server Data Tools y representadas en aplicaciones cliente como Excel o Power BI Desktop, las carpetas de visualización ayudan organizar grandes cantidades de medidas en carpetas individuales y agregan una jerarquía visual para explorar más fácilmente las listas de campos.
### <a name="bi-directional-cross-filtering"></a>Filtrado cruzado bidireccional
Como novedad de esta versión se ha introducido un enfoque integrado para permitir los filtros cruzados bidireccionales en los modelos tabulares, lo que elimina la necesidad de usar soluciones DAX manuales para propagar el contexto de filtro en las relaciones entre tablas. Los filtros solo se generan automáticamente cuando la dirección se puede establecer con un alto grado de certeza. Si hay ambigüedad en el formulario de varias rutas de consultas en relaciones de tabla, no se creará automáticamente un filtro. Vea [Filtros cruzados bidireccionales para modelos tabulares en SQL Server 2016 Analysis Services](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) para obtener más información.
 ### <a name="translations"></a>Traducciones    
 Ahora puede almacenar metadatos traducidos en un modelo tabular 1200. Los metadatos del modelo incluyen campos para **Culture**, títulos traducidos y descripciones traducidas. Para agregar traducciones, use el comando **Modelo** > **Traducciones** en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Vea [Traducciones en modelos tabulares &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md) para obtener más información.    
 ### <a name="pasted-tables"></a>Tablas pegadas    
 Ahora es posible actualizar un modelo tabular 1100 o 1103 a 1200 cuando el modelo contiene tablas pegadas. Recomendamos para ello usar [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. En SSDT, establezca **CompatibilityLevel** en 1200 y, a continuación, realice la implementación en una instancia [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obtener información detallada, vea [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) .    
 ### <a name="calculated-tables-in-ssdt"></a>Tablas calculadas en SSDT    
Una *tabla calculada* es una construcción de solo modelo basada en una consulta o una expresión de DAX en SSDT. Cuando se implementa en una base de datos, una tabla calculada no se distingue de las tablas normales.    

 Existen varios usos para las tablas calculadas, incluida la creación de nuevas tablas para exponer una tabla existente en un rol específico. El ejemplo clásico es una tabla de fechas que funciona en varios contextos (fecha de pedido, fecha de envío etc.). Mediante la creación de una tabla calculada para un rol determinado, ahora puede activar una relación de tabla para facilitar la interacción de datos o consultas con la tabla calculada. Otro uso de las tablas calculadas es combinar partes de las tablas existentes en una tabla completamente nueva que solo existe en el modelo.  Vea [Crear una tabla calculada &#40;SSAS tabular&#41](../analysis-services/tabular-models/create-a-calculated-table-ssas-tabular.md) para obtener más información.    
 ### <a name="formula-fixup"></a>Corrección de fórmula    
 Con la corrección de fórmula en un modelo tabular 1200, SSDT actualizará automáticamente cualquier medida que haga referencia a una columna o tabla cuyo nombre haya cambiado.    
 ### <a name="support-for-visual-studio-configuration-manager"></a>Compatibilidad con el administrador de configuración de Visual Studio    
 Para admitir varios entornos, como entornos de preproducción y prueba, Visual Studio permite a los desarrolladores crear varias configuraciones de proyecto con el administrador de configuración. Los modelos multidimensionales ya aprovechan esto, pero los modelos tabulares no lo hacían. Con esta versión, ahora puede usar el administrador de configuración para realizar la implementación en servidores diferentes.    

## <a name="instance-management"></a>Administración de instancias    
 ### <a name="administer-tabular-1200-models-in-ssms"></a>Administración de modelos tabulares 1200 en SSMS    
 En esta versión, una instancia de Analysis Services en el modo de servidor tabular puede ejecutar modelos tabulares en cualquier nivel de compatibilidad (1100, 1103 y 1200). La última versión de [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) se ha actualizado para mostrar las propiedades y proporcionar la administración del modelo de base de datos para los modelos tabulares en el nivel de compatibilidad 1200.    
 ### <a name="parallel-processing-for-multiple-table-partitions-in-tabular-models"></a>Procesamiento en paralelo para varias particiones de tabla en los modelos tabulares    
 Esta versión incluye una nueva funcionalidad para el procesamiento en paralelo de las tablas con dos o más particiones, lo que aumenta el rendimiento del procesamiento. No hay valores de configuración para esta característica. Para obtener más información sobre la configuración de particiones y el procesamiento de tablas, vea [Particiones de modelos tabulares &#40;SSAS tabular&#41;](../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md).    
 ### <a name="add-computer-accounts-as-administrators-in-ssms"></a>Adición de cuentas de equipo como administradores en SSMS    
 Los administradores de[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ahora pueden usar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para configurar las cuentas de equipo para que sean miembros del grupo de administradores de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . En el cuadro de diálogo **Seleccionar usuarios o grupos** , establezca **Ubicaciones** para el dominio de equipos y, a continuación, agregue el tipo de objeto **Equipos** . Para obtener más información, vea [Conceder permisos de administrador de servidor (Analysis Services)](../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).    
 ### <a name="dbcc-for-analysis-services"></a>DBCC para Analysis Services.    
 DBCC (Database Consistency Checker, comprobador de coherencia de base de datos) se ejecuta internamente para detectar posibles problemas de errores de datos en la base de datos de carga, pero también se puede ejecutar a petición si sospecha que hay problemas en los datos o el modelo. DBCC ejecuta comprobaciones diferentes dependiendo de si el modelo es tabular o multidimensional. Vea [Comprobador de coherencia de base de datos &#40;DBCC&#41; para bases de datos multidimensionales y tabulares de Analysis Services](../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md) para obtener más información.    
 ### <a name="extended-events-updates"></a>Actualizaciones de eventos extendidos    
 En esta versión se ha agregado una interfaz gráfica de usuario a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para configurar y administrar los eventos extendidos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Puede configurar los flujos de datos en directo para supervisar la actividad del servidor en tiempo real, mantener los datos de sesión cargados en memoria para un análisis más rápido o guardar flujos de datos en un archivo para un análisis sin conexión. Para obtener más información, vea [Supervisar Analysis Services con SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) y la entrada de blog y el vídeo de Guy in Cube con el título [Using extended events with Analysis Services](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx)(Uso de eventos extendidos con Analysis Services).    



## <a name="scripting"></a>Scripting
 ### <a name="powershell-for-tabular-models"></a>PowerShell para modelos tabulares    
 En esta versión se han incluido mejoras de PowerShell para los modelos tabulares en el nivel de compatibilidad 1200. Puede usar todos los cmdlets aplicables y, además, cmdlets específicos del modo tabular, como [Invoke ProcessASDatabase](../analysis-services/powershell/invoke-processasdatabase.md) y el [cmdlet Invoke-ProcessTable](../analysis-services/powershell/invoke-processtable-cmdlet.md).    
 ### <a name="ssms-scripting-database-operations"></a>Operaciones de base de datos de script de SSMS    
 En la última versión de [SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx), el script está ahora habilitado para los comandos de base de datos, que incluyen Create, Alter, Delete, Backup, Restore, Attach y Detach. El resultado es TMSL (Tabular Model Scripting Language, lenguaje de scripting del modelo tabular) en JSON. Vea [Tabular Model Scripting Language &#40;TMSL&#41; Reference](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) (Referencia de Tabular Model Scripting Language [TMSL]) para obtener más información.    
 ### <a name="analysis-services-execute-ddl-task"></a>Tarea Ejecutar DDL de Analysis Services    
 La[tarea Ejecutar DDL de Analysis Services](../integration-services/control-flow/analysis-services-execute-ddl-task.md) ahora acepta también los comandos de Tabular Model Scripting Language (TMSL).     
 ### <a name="ssas-powershell-cmdlet"></a>Cmdlet de PowerShell de SSAS    
 El cmdlet de PowerShell de SSAS **Invoke-ASCmd** ahora acepta comandos de Tabular Model Scripting Language (TMSL). Los demás cmdlets de PowerShell de SSAS podrían actualizarse en una versión futura para usar los nuevos metadatos tabulares (las excepciones se indicarán en las notas de la versión).    
Para obtener información detallada, vea [Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) .    
 ### <a name="tabular-model-scripting-language-tmsl-supported-in-ssms"></a>Tabular Model Scripting Language (TMSL) compatible en SSMS    
  Con la [versión más reciente de SSMS](http://msdn.microsoft.com/library/mt238290.aspx), ahora puede crear scripts para automatizar la mayoría de las tareas administrativas para los modelos tabulares 1200. Actualmente, se pueden crear scripts de las siguientes tareas: proceso en cualquier nivel, además de los comandos CREATE, ALTER y DELETE en el nivel de base de datos.    
    
 Funcionalmente, TMSL es equivalente a la extensión ASSL de XMLA que proporciona las definiciones de objetos multidimensionales, salvo que TMSL usa descriptores como **model**, **table**y **relationship** para describir los metadatos tabulares. Vea [Tabular Model Scripting Language &#40;TMSL&#41; Reference](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) (Referencia de Tabular Model Scripting Language [TMSL]) para obtener más información sobre el esquema.    
    
 Un script basado en JSON generado para un modelo tabular podría ser similar al siguiente:    
    
```    
{    
  "create": {    
    "database": { 
      "name": "AdventureWorksTabular1200",    
      "id": "AdventureWorksTabular1200",    
      "compatibilityLevel": 1200,    
      "readWriteMode": "readWrite",    
      "model": {}    
    }    
  }    
}    
```    

La carga es un documento JSON que puede ser mínimo, como en el ejemplo anterior, o adornarse mucho con el conjunto completo de definiciones de objetos. En [Tabular Model Scripting Language &#40;TMSL&#41; Reference](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) (Referencia de Tabular Model Scripting Language [TMSL]) se describe la sintaxis.

En el nivel de base de datos, los comandos CREATE, ALTER y DELETE darán como resultado un script de TMSL en la ventana de XMLA familiar.  Otros comandos, como PROCESS, también pueden incluirse en scripts en esta versión. En una versión futura podría agregarse compatibilidad con scripts para muchas otras acciones.    

**Comandos con scripts** | **Descripción**
--------------- | ----------------
crear|Permite agregar una base de datos, conexión o partición. El equivalente de ASSL es CREATE.
createOrReplace|Permite actualizar una definición de objeto existente (base de datos, conexión o partición) sobrescribiendo una versión anterior. El equivalente de ASSL es ALTER con AllowOverwrite establecido en true y ObjectDefinition en ExpandFull.
eliminar|Permite quitar una definición de objeto. El equivalente de ASSL es DELETE.
refresh|Procesa el objeto. El equivalente de ASSL es PROCESS.

## <a name="dax"></a>DAX
### <a name="improved-dax-formula-editing"></a>Edición de fórmula DAX mejorada
Las actualizaciones de la barra de fórmulas le ayudarán a escribir fórmulas con más facilidad mediante la diferenciación de funciones, campos y medidas con colores de sintaxis, que proporciona una función inteligente y sugerencias de campo e indica si las partes de la expresión DAX son incorrectas con el error de *subrayado ondulado*. También permite usar varias líneas (Alt + Entrar) y sangría (Tabulador). La barra de fórmulas ahora también le permite escribir comentarios como parte de sus medidas. Solo tiene que escribir "/ /" y todo lo que vaya después de estos caracteres en la misma línea se considerará un comentario.

### <a name="dax-variables"></a>Variables DAX    
En esta versión se incluye compatibilidad con variables en DAX. Ahora, las variables pueden almacenar el resultado de una expresión como una variable con nombre, que se pasa después como argumento a otras expresiones de medida. Una vez que se hayan calculado los valores resultantes para una expresión variable, dichos valores no cambian, incluso si se hace referencia a la variable en otra expresión. Para obtener más información, vea [Función VAR](http://msdn.microsoft.com/library/mt243785.aspx).    
### <a name="new-dax-functions"></a>Funciones DAX nuevas
Con esta versión, DAX presenta más de cincuenta funciones nuevas para admitir cálculos más rápidos y visualizaciones mejoradas en Power BI. Para obtener más información, vea [New DAX Functions](http://msdn.microsoft.com/library/mt704075.aspx)(Funciones DAX nuevas).
### <a name="save-incomplete-measures"></a>Guardado de las medidas incompletas
Ahora puede guardar las medidas DAX incompletas directamente en un proyecto del modelo tabular 1200 y seleccionarlo de nuevo cuando esté listo para continuar.
### <a name="additional-dax-enhancements"></a>Otras mejoras de DAX
- Cálculo de valores no vacíos: reduce el número de detecciones necesarias de valores no vacíos.
- Fusión de medidas: varias medidas de la misma tabla se combinarán en una sola consulta del motor de almacenamiento.
- Conjuntos de agrupamiento: cuando una consulta solicita medidas en varias granularidades (total/año/mes), se envía una sola consulta en el nivel más bajo y el resto de las granularidades se derivan del nivel más bajo.     
- Eliminación de combinación redundante: una sola consulta al motor de almacenamiento devuelve las columnas de dimensión y los valores de medida.
- Evaluación estricta de IF/SWITCH: una rama cuya condición sea false ya no producirá consultas del motor de almacenamiento. Antes, las ramas se evaluaban concienzudamente, pero los resultados se descartaban después.     
    
## <a name="developer"></a>Desarrollador    
 ### <a name="microsoftanalysisservicestabular-namespace-for-tabular-1200-programmability-in-amo"></a>Espacio de nombres Microsoft.AnalysisServices.Tabular para la programación tabular 1200 en AMO
 Los objetos de administración de Analysis Services (AMO) se actualizan para incluir un nuevo espacio de nombres tabular para administrar una instancia del modo tabular de SQL Server 2016 Analysis Services y para proporcionar el lenguaje de definición de datos para la creación o la modificación de modelos tabulares 1200 mediante programación. Visite [Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) para obtener información sobre la API.    
 ### <a name="analysis-services-management-objects-amo-updates"></a>Actualizaciones de objetos de administración de Analysis Services (AMO)
 Se han vuelto a diseñar los [objetos de administración de Analysis Services &#40;AMO&#41;](http://msdn.microsoft.com/library/mt436122.aspx) para incluir un segundo ensamblado, Microsoft.AnalysisServices.Core.dll. El nuevo ensamblado separa las clases comunes como el servidor, la base de datos y la función que tienen una amplia aplicación en Analysis Services, independientemente del modo de servidor.    
    
 Anteriormente, estas clases formaban parte del ensamblado Microsoft.AnalysisServices original. Moverlos a un nuevo ensamblado prepara el terreno para futuras ampliaciones a AMO, con una división clara entre las API genéricas y específicas del contexto.    
    
 Las aplicaciones existentes no se ven afectadas por los nuevos ensamblados. Sin embargo, si decide volver a generar aplicaciones con el nuevo ensamblado AMO por cualquier motivo, asegúrese de agregar una referencia a Microsoft.AnalysisServices.Core.    
    
 De forma similar, los scripts de PowerShell que cargan y llaman a AMO deben cargar ahora Microsoft.AnalysisServices.Core.dll. Asegúrese de actualizar los scripts.  

### <a name="json-editor-for-bim-files"></a>Editor JSON para archivos BIM
La vista Código en Visual Studio 2015 ahora representa el archivo BIM en formato JSON para los modelos tabulares 1200. La versión de Visual Studio determina si el archivo BIM se representa en JSON a través del editor JSON integrado o como texto simple.

Para usar el editor JSON, con la capacidad de expandir y contraer secciones del modelo, necesitará la versión más reciente de SQL Server Data Tools y Visual Studio 2015 (cualquier edición, incluida la edición Community gratis). Para las demás versiones de SSDT o Visual Studio, el archivo BIM se representa en JSON como texto simple.
Como mínimo, un modelo vacío contendrá el siguiente JSON:

    ```    
    {    
      "name": "SemanticModel",
      "id": "SemanticModel",
      "compatibilityLevel": 1200,
      "readWriteMode": "readWrite",
      "model": {}
    }    
    ```    
    
> [!WARNING]    
> Evite la edición directa de JSON. Esto puede dañar el modelo.    
 ### <a name="new-elements-in-ms-csdlbi-20-schema"></a>Nuevos elementos en el esquema de MS-CSDLBI 2.0    
 Se han agregado los siguientes elementos al tipo complejo **TProperty** definido en el esquema de [MS-CSDLBI] 2.0:    
    
|Elemento|Definición|    
|-------------|----------------|    
|DefaultValue|Una propiedad que especifica el valor usado al evaluar la consulta. La propiedad DefaultValue es opcional, pero se selecciona automáticamente si no se pueden agregar los valores del miembro.|    
|Estadísticas|Un conjunto de estadísticas de los datos subyacentes que está asociado a la columna. Estas estadísticas se definen mediante el tipo complejo de TPropertyStatistics y se proporcionan solo si su generación no es cara a nivel computacional, como se describe en la sección 2.1.13.5 del formato de archivo de definición del esquema conceptual con el documento de anotaciones de Business Intelligence.|    
    
## <a name="directquery"></a>DirectQuery    
### <a name="new-directquery-implementation"></a>Nueva implementación de DirectQuery    
En esta versión se incluyen mejoras considerables en DirectQuery para los modelos tabulares 1200. A continuación se muestra un resumen:    
-   DirectQuery genera ahora consultas más sencillas que proporcionan un mejor rendimiento.    
-   Control adicional sobre la definición de conjuntos de datos de ejemplo usados para tareas de prueba y diseño del modelo.    
-   La seguridad de nivel de fila (RLS) es ahora compatible con los modelos tabulares 1200 en el modo DirectQuery. Anteriormente, la presencia de RLS impedía implementar un modelo tabular en el modo DirectQuery.    
-   Ahora se admiten columnas calculadas en los modelos tabulares 1200 en el modo DirectQuery. Anteriormente, la presencia de columnas calculadas impedía implementar un modelo tabular en el modo DirectQuery.    
-   Entre las mejoras de rendimiento se incluye la eliminación de la combinación redundante para VertiPaq y DirectQuery. 

### <a name="new-data-sources-for-directquery-mode"></a>Nuevos orígenes de datos para el modo DirectQuery    
 Orígenes de datos admitidos para los modelos tabulares 1200 en el modo DirectQuery ahora incluyen Oracle, Teradata y Microsoft Analytics Platform (anteriormente conocido como almacenamiento de datos paralelos).    
    
Para obtener más información, vea [Modo DirectQuery &#40;SSAS tabular&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).    

## <a name="see-also"></a>Vea también
[Blog del equipo de Analysis Services](http://blogs.msdn.microsoft.com/analysisservices/)    
[Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)    
     


