---
title: Búsqueda de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server]
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d56a6e32818296343b711769ad594bf7cadce57
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011243"
---
# <a name="full-text-search"></a>Búsqueda de texto completo
  La búsqueda de texto completo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] permite a los usuarios y aplicaciones ejecutar consultas de texto completo en datos basados en caracteres en las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para que las consultas de texto completo se puedan ejecutar en una tabla determinada, el administrador de bases de datos debe crear un índice de texto completo en la tabla. El índice de texto completo incluye una o varias columnas de caracteres en la tabla. Estas columnas pueden tener cualquiera de los siguientes tipos de datos: `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml` o `varbinary(max)`, y FILESTREAM. Cada índice de texto completo indiza una o varias columnas de la tabla base y cada columna puede usar un idioma concreto.  
  
 Las consultas de texto completo realizan las búsquedas lingüísticas en los datos de texto de los índices de texto completo sobre palabras y frases basándose en las reglas de un idioma determinado, como inglés o japonés. Las consultas de texto completo pueden contener palabras y frases sencillas, o formas diversas de una palabra o frase. Una consulta de texto completo devuelve todos los documentos que contienen por lo menos una coincidencia (también se conoce como *acierto*). Se produce una coincidencia cuando un documento de destino contiene todas las condiciones especificadas en la consulta de texto completo y cumple cualquier otra condición de búsqueda, como la distancia entre los términos que coinciden.  
  
> [!NOTE]  
>  La búsqueda de texto completo es un componente opcional del motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [instalación de SQL Server 2014](../../database-engine/install-windows/install-sql-server.md).  
  
##  <a name="benefits"></a>¿Qué puedo hacer con la búsqueda de texto completo?  
 La búsqueda de texto completo es aplicable a una amplia gama de escenarios empresariales como, por ejemplo, la búsqueda de elementos en un sitio Web. empresas judiciales: búsqueda de historiales de casos en un repositorio de datos legales; o los departamentos de recursos humanos: descripciones de trabajos coincidentes con currículos almacenados. Las tareas administrativas y de desarrollo básicas de la búsqueda de texto completo son equivalentes independientemente de los escenarios empresariales. Sin embargo, en un escenario empresarial determinado, el índice y las consultas de texto completo se pueden ajustar a los objetivos empresariales. Por ejemplo, para un e-business podría ser más importante la maximización del rendimiento que la clasificación de resultados, la exactitud de la recuperación (cuántas de las coincidencias existentes devuelve realmente una consulta de texto completo) o la admisión de varios idiomas. Para un bufete de abogados, recuperar cada posible acierto (*recuperación total* de información) podría ser la consideración más importante.  
  
 [En este tema](#top)  
  
###  <a name="queries"></a>Consultas de búsqueda de texto completo  
 Una vez agregadas las columnas a un índice de texto completo, los usuarios y aplicaciones pueden ejecutar las consultas de texto completo en el texto de las columnas. Estas consultas pueden buscar cualquiera de lo siguiente:  
  
-   Una o varias palabras o frases específicas (*término simple*)  
  
-   Una palabra o frase cuyas palabras empiezan por un texto determinado (*término de prefijo*)  
  
-   Formas con inflexión de una palabra determinada (*término de generación*)  
  
-   Una palabra o frase que esté cerca de otra palabra o frase (*término de proximidad*)  
  
-   Formas sinónimas de una palabra determinada (*diccionario de sinónimos*)  
  
-   Palabras o frases que usan valores ponderados (*término ponderado*)  
  
 Las consultas de texto completo no distinguen entre mayúsculas y minúsculas. Por ejemplo, la búsqueda de "Aluminio" o "aluminio" devuelve los mismos resultados.  
  
 Las consultas de texto completo usan un pequeño conjunto de predicados [!INCLUDE[tsql](../../../includes/tsql-md.md)] (CONTAINS y FREETEXT) y funciones  (CONTAINSTABLE y FREETEXTTABLE). Sin embargo, los objetivos de la búsqueda en un escenario empresarial determinado influyen en la estructura de las consultas de texto completo. Por ejemplo:  
  
-   e-business: búsqueda de un producto en un sitio web:  
  
    ```  
    SELECT product_id   
    FROM products   
    WHERE CONTAINS(product_description, "Snap Happy 100EZ"  
        OR FORMSOF(THESAURUS,'Snap Happy')  
        OR '100EZ')   
    AND product_cost < 200 ;  
    ```  
  
-   Escenario de contratación de empleados: búsqueda de candidatos para un puesto de trabajo que tengan experiencia en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
    ```  
    SELECT candidate_name,SSN   
    FROM candidates   
    WHERE CONTAINS(candidate_resume,"SQL Server") AND candidate_division = 'DBA';  
    ```  
  
 Para obtener más información, vea [Consultar con búsqueda de texto completo](query-with-full-text-search.md).  
  
 [En este tema](#top)  
  
###  <a name="like"></a>Comparar LIKE con la búsqueda de texto completo  
 A diferencia de la búsqueda de texto completo, el predicado [like](/sql/t-sql/language-elements/like-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] solo funciona en patrones de caracteres. Además, no es posible utilizar el predicado de LIKE para consultar datos binarios con formato. Por otro lado, una consulta LIKE contra una cantidad grande de datos de texto no estructurados es mucho más lenta que una consulta de texto completo equivalente contra los mismos datos. Una consulta LIKE realizada en millones de filas de datos de texto puede tardar minutos en devolver resultados, mientras que una consulta de texto completo en los mismos datos puede tardar únicamente segundos, en función del número de filas que se devuelvan.  
  
 [En este tema](#top)  
  
##  <a name="architecture"></a>Componentes y arquitectura de la búsqueda de texto completo  
 La arquitectura de búsqueda de texto completo consta de los procesos siguientes:  
  
-   Proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (sqlserver.exe).  
  
-   Proceso de host de demonio de filtro (fdhost.exe).  
  
     Por razones de seguridad, los filtros se cargan mediante procesos independientes denominados hosts de demonio de filtro. El servicio iniciador de FDHOST (MSSQLFDLauncher) crea los procesos de fdhost.exe, que se ejecutan con las credenciales de seguridad de la cuenta de servicio del iniciador de FDHOST. Por consiguiente, el servicio iniciador de FDHOST debe estar en ejecución para que la indización de texto completo y la consulta de texto completo funcionen. Para obtener más información sobre cómo configurar la cuenta de servicio para este servicio, vea [Establecer la cuenta del servicio para el selector del demonio de filtro completo](set-the-service-account-for-the-full-text-filter-daemon-launcher.md).  
  
 Estos dos procesos contienen los componentes de la arquitectura de búsqueda de texto completo. Estos componentes y sus relaciones se resumen en la ilustración siguiente. Los componentes se describen después de la ilustración.  
  
 ![arquitectura de la búsqueda de texto completo](../../database-engine/media/ifts-arch.gif "arquitectura de la búsqueda de texto completo")  
  
 [En este tema](#top)  
  
###  <a name="sqlprocess"></a>SQL Server proceso  
 El proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa los componentes siguientes para la búsqueda de texto completo:  
  
-   **Tablas de usuario.** Esta tablas contienen los datos cuyo texto completo se indizará.  
  
-   **Recopilador de texto completo.** El recopilador de texto completo trabaja con los subprocesos de rastreo de texto completo (rellenado). Es responsable de programar y dirigir el rellenado de índices de texto completo, y también de supervisar los catálogos de texto completo.  
  
-   **Archivos de sinónimos.** Estos archivos contienen sinónimos de los términos de búsqueda. Para obtener más información, vea [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Objetos STOPLIST.** Los objetos de listas de palabras irrelevantes contienen una lista de palabras comunes que no son útiles para la búsqueda. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]procesador de consultas.** El procesador de consultas compila y ejecuta consultas SQL. Si una consulta SQL incluye una consulta de búsqueda de texto completo, la consulta se envía al motor de texto completo, durante la compilación y durante la ejecución. El resultado de la consulta se hace coincidir con el índice de texto completo.  
  
-   **Motor de texto completo.** El motor de texto completo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se integra ahora totalmente con el procesador de consultas. El motor de texto completo compila y ejecuta consultas de texto completo. Como parte de la ejecución de consultas, el motor de texto completo puede recibir entradas del diccionario de sinónimos y de la lista de palabras irrelevantes.  
  
-   **Escritor de índices (indizador).** El escritor de índices genera la estructura que se utiliza para almacenar los tokens indizados.  
  
-   **Administrador de demonio de filtro.** El administrador del demonio de filtro es responsable de supervisar el estado del host de demonio de filtro del motor de texto completo.  
  
 [En este tema](#top)  
  
###  <a name="fdhostprocess"></a>Proceso de host de demonio de filtro  
 El host de demonio de filtro es un proceso iniciado por el motor de texto completo. Ejecuta los componentes de búsqueda de texto completo siguientes, que son responsables de obtener acceso a los datos de las tablas, filtrarlos y separar las palabras de esos datos, así como de separar las palabras y lematizar la entrada de la consulta.  
  
 Los componentes del proceso de host de demonio de filtro son los siguientes:  
  
-   **Controlador de protocolo.** Este componente extrae los datos de la memoria para su posterior procesamiento y tiene acceso a los datos de una tabla de usuario de una base de datos especificada. Una de sus responsabilidades es recopilar los datos de las columnas con indización de texto completo y pasarlos al host de demonio de filtro, que aplicará el filtrado y la separación de palabras cuando sea necesario.  
  
-   **Complementa.** Algunos tipos de datos requieren un filtrado para que los datos de un documento puedan indizarse con texto completo, incluso los datos de las columnas `varbinary`, `varbinary(max)`, `image` o `xml`. El filtro utilizado para un documento determinado depende de su tipo de documento. Por ejemplo, se utilizan filtros diferentes para los documentos de Microsoft Word (.doc), de Microsoft Excel (.xls) y XML (.xml). A continuación, el filtro extrae fragmentos de texto del documento, mientras quita el formato incrustado y conserva el texto y, potencialmente, la información sobre la posición del mismo. El resultado es un flujo de información de texto. Para obtener más información, vea [Configurar y administrar filtros para búsquedas](configure-and-manage-filters-for-search.md).  
  
-   **Separadores de palabras y lematizadores.** Un separador de palabras es un componente específico del idioma que busca los límites de palabras según las reglas léxicas de un idioma determinado (*separación de palabras*). Cada separador de palabras está asociado a un componente de lematizador específico del idioma que conjuga los verbos y realiza las expansiones flexionales. Al realizar la indización, el host de demonio de filtro utiliza un separador de palabras y un lematizador para realizar el análisis lingüístico de los datos de texto de una columna de la tabla determinada. El lenguaje asociado a una columna de la tabla en el índice de texto completo determina qué separador de palabras y lematizador se utilizan para indizar la columna. Para obtener más información, vea [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
 [En este tema](#top)  
  
##  <a name="processing"></a>Procesamiento de la búsqueda de texto completo  
 La búsqueda de texto completo se realiza gracias al motor de texto completo. El motor de texto completo desempeña dos roles: la indización y las consultas.  
  
###  <a name="indexing"></a>Proceso de indización de texto completo  
 Cuando se inicia un rellenado de texto completo (también conocido como rastreo), el motor de texto completo inserta lotes grandes de datos en la memoria y lo notifica al host de demonio de filtro. El host filtra y establece separaciones de palabras en los datos, y convierte los datos convertidos en las listas de palabras invertidas. A continuación, la búsqueda de texto completo extrae los datos convertidos de las listas de palabras, procesa los datos para quitar las palabras irrelevantes y conserva las listas de palabras para un lote en uno o varios índices invertidos.  
  
 Al indizar los datos almacenados en `varbinary(max)` una `image` columna o, el filtro, que implementa la interfaz **IFilter** , extrae texto basándose en el formato de archivo especificado para los datos ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] por ejemplo, Word). En algunos casos, los componentes de filtro requieren `varbinary(max)`que los `image` datos de, o se escriban en la carpeta filterdata, en lugar de insertarse en la memoria.  
  
 Como parte del procesamiento, los datos de texto recopilados se pasan a través de un separador de palabras para dividir el texto en tokens o palabras clave individuales. El idioma que se utiliza para la conversión en símbolos (tokens) se especifica en el nivel de columna o bien se identifica en los `varbinary(max)`, `image` o `xml` mediante el componente de filtro.  
  
 Puede llevarse a cabo un procesamiento adicional para quitar las palabras irrelevantes y normalizar los tokens antes de que se almacenen en el índice de texto completo o en un fragmento de índice.  
  
 Cuando se completa un rellenado, se desencadena un proceso de combinación final que combina los fragmentos de índice en un solo índice de texto completo maestro. Esto permite mejorar el rendimiento de las consultas, ya que únicamente es necesario realizar consultas en el índice maestro, en lugar de hacerlo en varios fragmentos de índice, y se pueden utilizar mejores estadísticas de puntuación para obtener la clasificación por relevancia.  
  
 [En este tema](#top)  
  
###  <a name="querying"></a>Proceso de consulta de texto completo  
 El procesador de consultas pasa las partes de texto completo de una consulta al Motor de búsqueda de texto completo para procesarlas. El motor de búsqueda de texto completo realiza la separación de palabras y, opcionalmente, expansiones del diccionario de sinónimos, lematización y procesamiento de las palabras irrelevantes. A continuación, las partes de texto completo de la consulta se representan en forma de operadores de SQL, principalmente como funciones con valores de tabla de transmisión por secuencias (STVF). Durante la ejecución de la consulta, las STVF tienen acceso al índice invertido para recuperar los resultados correctos. Los resultados se devuelven en este punto al cliente o se siguen procesando antes de devolverse al cliente.  
  
 [En este tema](#top)  
  
##  <a name="components"></a>Componentes lingüísticos y compatibilidad con idiomas en la búsqueda de texto completo  
 La búsqueda de texto completo admite casi 50 idiomas distintos, como inglés, español, chino, japonés, árabe, bengalí e hindi. Para obtener una lista completa de los idiomas de texto completo compatibles, vea [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql). Cada una de las columnas incluidas en el índice de texto completo está asociada a un identificador de configuración regional (LCID) de Microsoft Windows que se corresponde con un idioma compatible con la búsqueda de texto completo. Por ejemplo, el LCID 1033 corresponde al inglés de Estados Unido y el LCID 2057 corresponde al inglés de Reino Unido. Para cada idioma de texto completo compatible, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona componentes lingüísticos que permiten indizar y consultar los datos de texto completo almacenados en ese idioma.  
  
 Entre los componentes específicos del idioma se incluyen los siguientes:  
  
-   **Separadores de palabras y lematizadores.** Un separador de palabras busca los límites de palabra en función de las reglas léxicas de un idioma concreto (*separación de palabras*). Cada separador de palabras está asociado a un lematizador que conjuga los verbos para dicho idioma. Para obtener más información, vea [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
-   **Palabras irrelevantes.** Se proporciona una lista de palabras irrelevantes del sistema que contiene un conjunto básico de palabras irrelevantes (denominadas también palabras vacías). Una *palabra irrelevante* es una palabra que no aporta nada a la búsqueda y que se omite en las consultas de texto completo. Por ejemplo, en la configuración regional en inglés, las palabras como "a", "and", "is" y "the" se consideran palabras irrelevantes. Normalmente, tendrá que configurar uno o varios archivos de diccionario de sinónimos y listas de palabras irrelevantes. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **Archivos de sinónimos.** 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala también un archivo de diccionario de sinónimos para cada idioma de texto completo, además de un archivo de diccionario de sinónimos global. Los archivos de diccionario de sinónimos instalados son básicamente archivos vacíos, pero puede modificarlos para definir los sinónimos de un determinado idioma o escenario empresarial. Al desarrollar un diccionario de sinónimos personalizado para los datos de texto completo, puede ampliar de forma eficaz el ámbito de las consultas de texto completo en esos datos. Para obtener más información, vea [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Filtros (iFilters).**  La indización de un documento en una columna de tipo de datos `varbinary(max)`, `image`, o `xml` requiere un filtro que realice el procesamiento adicional. El filtro debe ser específico del tipo de documento (.doc, .pdf, .xls, .xml, etc.). Para obtener más información, vea [Configurar y administrar filtros para búsquedas](configure-and-manage-filters-for-search.md).  
  
 Los separadores de palabras (y lematizadores) y los filtros se ejecutan en el proceso de host de demonio de filtro (fdhost.exe).  
  
 [En este tema](#top)  
  
##  <a name="reltasks"></a> Tareas relacionadas  
  
-   [Introducción a la búsqueda de texto completo](get-started-with-full-text-search.md)  
  
-   Escribir consultas de texto completo  
  
    -   [Consultar con búsqueda de texto completo](query-with-full-text-search.md)  
  
    -   [Buscar palabras cerca de otra palabra con NEAR](search-for-words-close-to-another-word-with-near.md)  
  
    -   [Limitar los resultados de la búsqueda con RANK](limit-search-results-with-rank.md)  
  
    -   [Mejorar el rendimiento de las consultas de texto completo](improve-the-performance-of-full-text-queries.md)  
  
    -   [Buscar propiedades de documento con listas de propiedades de búsqueda](search-document-properties-with-search-property-lists.md)  
  
    -   [Buscar GUID del conjunto de propiedades e identificadores de enteros de propiedad para las propiedades de búsqueda](find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
-   Administrar catálogos e índices  
  
    -   [Crear y administrar catálogos de texto completo](create-and-manage-full-text-catalogs.md)  
  
    -   [Crear y administrar índices de texto completo](create-and-manage-full-text-indexes.md)  
  
    -   [Elegir un idioma al crear un índice de texto completo](choose-a-language-when-creating-a-full-text-index.md)  
  
    -   [Rellenar índices de texto completo](populate-full-text-indexes.md)  
  
    -   [Administrar índices de texto completo](../../database-engine/manage-full-text-indexes.md)  
  
    -   [Mejorar el rendimiento de los índices de texto completo](improve-the-performance-of-full-text-indexes.md)  
  
    -   [Solucionar problemas de indización de texto completo](troubleshoot-full-text-indexing.md)  
  
    -   [Realizar copias de seguridad de los catálogos e índices de texto completo y restaurarlos](back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   Administrar los componentes lingüísticos  
  
    -   [Configurar y administrar filtros para búsquedas](configure-and-manage-filters-for-search.md)  
  
    -   [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
    -   [Ver o cambiar los filtros y separadores de palabras registrados](view-or-change-registered-filters-and-word-breakers.md)  
  
    -   [Revertir los separadores de palabras usados por las búsquedas a la versión anterior](revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
    -   [Cambiar el separador de palabras usado para el inglés de Estados Unidos y el del Reino Unido](change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
    -   [Personalizar el comportamiento de separadores de palabras con un diccionario personalizado](customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)  
  
    -   [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
    -   [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
-   Administrar la búsqueda de texto completo  
  
    -   [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](manage-and-monitor-full-text-search-for-a-server-instance.md)  
  
    -   [Establecer la cuenta del servicio para el selector del demonio de filtro de texto completo](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
  
-   [Actualizar la búsqueda de texto completo](upgrade-full-text-search.md)  
  
 [En este tema](#top)  
  
##  <a name="relcontent"></a> Contenido relacionado  
  
-   [DDL de búsqueda de texto completo, funciones, procedimientos almacenados y vistas](../views/views.md)  
  
 [En este tema](#top)  
  
  
