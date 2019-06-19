---
title: Proyectos relacionados para soluciones de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dc26489a-4c27-4b89-8215-6d245427c350
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af175693a93535b21b399cf4916ca4291fc94dfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082988"
---
# <a name="related-projects-for-data-mining-solutions"></a>Proyectos relacionados en las soluciones de minería de datos
  Lo mínimo que se requiere para una solución de minería de datos es el proyecto de minería de datos, que define los orígenes de datos, las vistas del origen de datos, las estructuras y los modelos de minería de datos. Sin embargo, cuando los modelos de minería de datos se utilizan en la toma de decisiones diaria, es importante que la minería de datos se integre con otra parte de una solución de predicción de análisis, que puede incluir estos procesos y componentes:  
  
-   Preparación y selección de datos y variables. Incluye la limpieza de datos, la administración metadatos y la integración de orígenes de datos, y la conversión, combinación y carga de datos en un almacenamiento de datos.  
  
-   Informes de análisis, presentación de predicciones y auditoría y seguimiento de las actividades de minería de datos.  
  
-   Uso de modelos multidimensionales o modelos tabulares para explorar los hallazgos.  
  
-   Perfeccionamiento de la solución de minería de datos para proporcionar nuevos datos o cambios en la infraestructura de soporte motivados por un análisis actual.  
  
 En este tema se describen otras características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que, a menudo, son parte de una solución de predicción de análisis, ya sea para respaldar los procesos de preparación y de minería de datos o a los usuarios proporcionándoles herramientas para el análisis y la acción.  
  
 [Integration Services](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Data Quality Services](#bkmk_DQSetc)  
  
 [Búsqueda de texto completo](#bkmk_FTSetc)  
  
 [Indización semántica](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a> SQL Server Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona los componentes y las características necesarias para las fases de entrenamiento y de preparación de los datos de un proyecto de minería de datos. Aunque puede realizar numerosas tareas de preparación o de limpieza de datos con otras herramientas, como scripts, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] presenta numerosas ventajas para la minería de datos:  
  
-   Representa las tareas como parte de un flujo de trabajo, que puede repetirse, automatizarse, bifurcarse y ampliarse.  
  
-   Proporciona amplias funciones de auditoría auditar y varias formas de capturar los errores y registrar los eventos.  
  
     Además de capturar el linaje de los datos, puede supervisar los cambios en los datos a través de la canalización de transformación de datos.  
  
     También puede integrar los flujos de trabajo SSIS con las características que admiten la funcionalidad Captura de datos modificados en SQL Server.  
  
-   La minería de datos se puede incorporar en el flujo de trabajo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , para separar de modo inteligente los datos entrantes en varias tablas. Por ejemplo, puede utilizar una consulta de predicción para dividir los nuevos clientes en grupos distintos para los destinatarios de una campaña de correo.  
  
 En las siguientes listas se proporcionan vínculos a los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que más se usan en la minería de datos.  
  
 **Componentes de flujo de control**  
  
-   [Tarea Ejecutar DDL de Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Tarea de procesamiento de Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [Tarea Control CDC](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [Limpieza de datos](../../data-quality-services/data-cleansing.md)  
  
-   [Tarea Consulta de minería de datos](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [Tarea de generación de perfiles de datos](../../integration-services/control-flow/data-profiling-task.md)  
  
 **Componentes de flujo de datos**  
  
-   [Componentes del flujo de CDC](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [Transformación División condicional](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [Transformación Conversión de datos](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [Destino de entrenamiento del modelo de minería de datos](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [Transformación Consulta de minería de datos](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [Transformación Columna derivada](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [Transformación Muestreo de porcentaje](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [Transformación Extracción de términos](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [Transformación Búsqueda de términos](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a> SQL Server Reporting Services  
 Aunque [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se vea normalmente como un componente esencial de las soluciones de minería de datos, proporciona las siguientes características útiles para la presentación de las soluciones de minería de datos.  
  
-   Integración de datos de varios orígenes en informes complejos. Creación de consultas con el contenido de modelos para los analistas e informes que muestran predicciones y tendencias de los usuarios finales.  
  
-   La capacidad de crear un informe que permita a los usuarios realizar consultas directamente en un modelo de minería de datos existente.  
  
-   Integración con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], para permitir la obtención de detalles y la exploración de dimensiones de minería de datos y cubos de minería de datos creados a partir de modelos OLAP.  
  
-   Las características de formato y parametrización están disponibles en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Para obtener más información sobre cómo usar Reporting Services con consultas DMX como origen de datos, vea los siguientes vínculos:  
  
 [Recuperar datos de un modelo de minería de datos &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [Tipo de conexión de Analysis Services para DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 Sin embargo, no es necesario utilizar DMX como origen de datos. Los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para minería de datos también permite guardar los resultados de una consulta de predicción en una base de datos relacional. Si tiene un flujo de trabajo establecido para actualizar los modelos con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], las predicciones de persistencia y otros resultados de consulta de minería de datos en SQL Server le permiten utilizar [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para los informes, así como otras herramientas que no interactúen con DMX.  
  
 Para obtener más información sobre cómo usar Reporting Services como nivel de presentación para los orígenes de datos, vea [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md).  
  
##  <a name="bkmk_DQSetc"></a> Data Quality Services  
 Data Quality Services (DQS) es nuevo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Como los problemas con datos pueden imposibilitar la minería de datos, se espera que los responsables de la minería de datos que realizan análisis repetidos o que trabajan en grandes organizaciones con orígenes de datos complejos encuentren que un proyecto de datos bien planeado que use DQS es una solución más confiable para admitir la minería de datos, en lugar de la limpieza ad hoc de los datos con [!INCLUDE[tsql](../../includes/tsql-md.md)] u otros scripts.  
  
 Las siguientes características de DQS deben considerarse para la preparación y la integridad de los datos en una solución de minería de datos.  
  
 **Un proceso de limpieza de datos asistido por PC que analice los datos de origen y proponga cambios.**  
 DQS puede comparar los datos de un origen con los datos de referencia basados en nube que son mantenidos y garantizados por los proveedores de calidad de los datos.  
  
 DQS también puede analizar los datos de origen sin formato y crear una base de conocimiento a partir de los datos de usuario. Los datos procesados se clasifican y muestran después al usuario para seguir procesándose. El proceso de limpieza es interactivo, lo que significa que el administrador de datos puede aprobar, rechazar o modificar los datos propuestos por el proceso de limpieza de datos asistido por PC.  
  
 El resultado del proceso es una base de conocimiento que puede mejorar continuamente o bien reutilizar en varias fases de mejora de los datos.  
  
 Para más información, consulte [Data Cleansing](../../data-quality-services/data-cleansing.md).  
  
 **Un proceso de correspondencia asistido por PC que analice los datos de origen y proponga cambios.**  
 Para evitar la duplicación de los datos, puede realizar una limpieza adicional del origen de datos, para identificar coincidencias exactas o aproximadas. Estos componentes permiten especificar las reglas de correspondencia y los umbrales en los que aplicarlas.  
  
 Al buscar correspondencias en los datos, puede quitar los duplicados, que pueden constituir un problema para la minería de datos. La no duplicación de los datos no es automática; el administrador de datos o el profesional de TI debe comprobar tanto el conocimiento de la base de conocimiento como los cambios que se realizan en los datos.  
  
 Después de crear el proyecto inicial de DQS, puede automatizar muchas de las tareas mediante los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para más información, consulte [Data Matching](../../data-quality-services/data-matching.md).  
  
 Al realizar las actividades de correspondencia y limpieza en un proyecto de calidad de los datos, puede obtener estadísticas e información en tiempo real de los datos que DQS procesó. Los perfiles de datos le ayudan a evaluar en qué medida la correspondencia o la limpieza de los datos ayudaron a mejorar su calidad y a conocer los cambios realizados. Para obtener información acerca de las notificaciones y de los perfiles de datos, vea [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
 **Una base de conocimiento que representa tres tipos de conocimiento: el conocimiento previo, el generado por el servidor de DQS y el generado por el usuario.**  
 Una vez que haya creado una base de conocimiento, puede utilizarla continuamente para limpiar y comprobar otros datos.  
  
 Puede importar los datos nuevos en los datos de la base de conocimiento de varios orígenes, ya sean los datos limpios conocidos de proveedores de referencia o los datos sin formato que coinciden con los datos existentes en la base de conocimiento.  
  
 Para obtener información detallada acerca de la actividad de limpieza en un proyecto de calidad de datos, vea Limpieza de datos (DQS).  
  
 También puede aplicar el conocimiento de la base de conocimiento a otros orígenes, a fin de realizar la limpieza de los datos dentro de otros procesos. Tal limpieza de datos puede ayudar a identificar los errores provocados por los usuarios al introducirlos, daños durante la transmisión o el almacenamiento, o definiciones de diccionarios de datos no coincidentes.  
  
 Para obtener más información, consulte [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
##  <a name="bkmk_FTSetc"></a> Búsqueda de texto completo  
 La búsqueda de texto completo de SQL Server permite a las aplicaciones y a los usuarios ejecutar consultas de texto completo en datos basados en caracteres en las tablas de SQL Server. Cuando se habilita la búsqueda de texto completo, puede realizar búsquedas en los datos de texto que son mejoradas mediante reglas específicas del idioma acerca de las diversas formas de una palabra o frase. También puede configurar las condiciones de búsqueda, como la distancia entre varios términos, y utilizar funciones para restringir los resultados devueltos por orden de probabilidad.  
  
 Puesto que las consultas de texto completo son una característica que proporciona el motor de SQL Server, puede crear consultas con parámetros, generar conjuntos de datos personalizados o vectores de términos mediante características de búsqueda de texto completo en un origen de datos de texto y utilizar estos orígenes de minería de datos.  
  
 Para más información sobre cómo interactúan las consultas de texto completo con el índice de texto completo, vea [Consultar con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md).  
  
 Una ventaja del uso de las características de búsqueda de texto completo de SQL Server es que puede aprovechar la inteligencia lingüística que se encuentra en los separadores de palabras y los lematizadores proporcionados en todos los idiomas de SQL Server. Mediante el uso de los separadores de palabras y los lematizadores proporcionados, puede asegurarse de que las palabras se separan mediante los caracteres apropiados para cada idioma y de que los sinónimos basados en signos diacríticos o variaciones ortográficas (como los formatos de número, en japonés) no se pasan por alto.  
  
 Además de la inteligencia lingüística que rige los límites de las palabras, los lematizadores de cada idioma pueden reducir las variantes de una palabra un único término, según el conocimiento de las reglas de la conjugación y la variación ortográfica en ese idioma. Las reglas para el análisis lingüístico difieren para cada idioma y se desarrollan en función de una amplia investigación en el corpus de uso real.  
  
 Para obtener más información, vea [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
 La versión de una palabra que se almacena después de una indización de texto completo es un símbolo en formato comprimido. Las consultas posteriores al índice de texto completo generan formas no flexionadas de una palabra determinada según las reglas de ese idioma, para asegurarse de que se realizan todas las coincidencias probables. Por ejemplo, aunque el token que se almacena podría ser "ejecutar", el motor de consultas también busca los términos "running", "corrió" y "corredor", porque son variaciones morfológicas derivadas de la palabra raíz "ejecutar".  
  
 También puede crear y generar un diccionario de sinónimos de usuario para almacenar los sinónimos y habilitar mejores resultados de la búsqueda, o la clasificación de los términos. Al desarrollar un diccionario de sinónimos personalizado para los datos de texto completo, puede ampliar de forma eficaz el ámbito de las consultas de texto completo en esos datos. Para obtener más información, vea [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
 Algunos requisitos para utilizar la búsqueda de texto completo son los siguientes:  
  
-   El administrador de la base de datos debe crear un índice de texto completo en la tabla.  
  
-   Solo se permite un índice de texto completo por cada tabla.  
  
-   Cada columna que se indiza debe tener una clave única.  
  
-   La indización de texto completo solo se admite para las columnas con estos tipos de datos: char, varchar, nchar, nvarchar, text, ntext, image, xml, varbinary y varbinary(max). Si la columna es varbinary, varbinary (max), image o XML, debe especificar la extensión de archivo del documento indizable (.doc, .pdf, .xls, etc.), en una columna de tipo independiente.  
  
##  <a name="bkmk_SemSearch"></a> Indización semántica  
 La búsqueda semántica se basa en las características de búsqueda de texto completo existentes en SQL Server, pero utiliza estadísticas y funciones adicionales para escenarios como la extracción automática de palabras clave y la detección de documentos relacionados. Por ejemplo, puede usar la búsqueda semántica para generar una taxonomía base para una organización u ordenar un corpus de documentos. O bien, podría utilizar la combinación de los términos extraídos y las clasificaciones de similitud de los documentos en los modelos de árbol de decisión o de un clúster.  
  
 Después de habilitar la búsqueda semántica correctamente e indizar sus columnas de datos, puede utilizar las funciones que se proporcionan de modo nativo con la indización semántica para lo siguiente:  
  
-   Devolver las frases con una sola palabra clave con su clasificación.  
  
-   Devolver los documentos que contengan una frase clave especificada.  
  
-   Ejecutar clasificaciones de similitud y los términos que contribuyan a las mismas.  
  
 Para obtener más información, vea [Buscar frases clave en documentos con la búsqueda semántica](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) y [Buscar documentos similares y relacionados con la búsqueda semántica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
 Para más información sobre los objetos de base de datos compatibles con la indexación semántica, vea [Habilitar la búsqueda semántica en tablas y columnas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md).  
  
 Entre los requisitos para utilizar la búsqueda semántica se encuentran los siguientes:  
  
-   La búsqueda de texto completo también está habilitada.  
  
-   La instalación de los componentes de la búsqueda semántica también crea una base de datos de sistema especial, que no se puede cambiar, modificar ni reemplazar.  
  
-   Los documentos que indice mediante el servicio se deben almacenar en SQL Server, en alguno de los objetos de base de datos admitidos en la indización de texto completo, incluidas las tablas y las vistas indizadas.  
  
-   No todos los idiomas de texto completo admiten la indización semántica. Para consultar la lista de idiomas compatibles, vea [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Soluciones de modelos multidimensionales &#40;SSAS&#41;](../multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Soluciones de modelos tabulares &#40;SSAS tabular&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
  
