---
title: Cambios de comportamiento en la búsqueda de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
author: rothja
ms.author: jroth
ms.openlocfilehash: cbe807237651bd8bb81fa1c9f028847654b97889
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936186"
---
# <a name="behavior-changes-to-full-text-search"></a>Cambios de comportamiento en la búsqueda de texto completo
  En este tema se describen los cambios de comportamiento en la búsqueda de texto completo. Los cambios de comportamiento afectan al modo en que las características de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] funcionan o interactúan en comparación con las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="behavior-changes-in-full-text-search-in-sssql14"></a>Cambios de comportamiento en la búsqueda de texto completo de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 La información se proporcionará posteriormente.  
  
## <a name="behavior-changes-in-full-text-search-in-sssql11"></a>Cambios de comportamiento en la búsqueda de texto completo de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] instala una versión nueva de los separadores de palabras y los lematizadores para inglés de EE.UU. (LCID 1033) e inglés de Reino Unido (LCID 2057). Aunque puede cambiar a la versión anterior de estos componentes si desea conservar el comportamiento anterior. Para obtener más información, vea [Cambiar el separador de palabras usado para el inglés de Estados Unidos y el del Reino Unido](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>Nuevos separadores de palabras y lematizadores instalados  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] actualiza todos los separadores de palabras y lematizadores que se utilizan en la búsqueda de texto completo y en la búsqueda semántica. Para que haya coherencia entre el contenido de los índices y los resultados de las consultas, se recomienda que vuelva a rellenar los índices de texto completo existentes.  
  
1.  Existen nuevos separadores de palabras para inglés. Si tiene que conservar el comportamiento anterior, vea [Change the Word Breaker Used for US English and UK English](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
2.  Se han reemplazado los separadores de palabras de terceros para danés, polaco y turco que se incluían en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con componentes de [!INCLUDE[msCoName](../includes/msconame-md.md)] . Los componentes nuevos están habilitados de forma predeterminada.  
  
3.  Existen nuevos separadores de palabras para checo y griego. Las versiones anteriores de búsqueda de texto completo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no incluían compatibilidad con estos dos idiomas.  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>Cambios de comportamiento de los nuevos separadores de palabras y lematizadores  
 Es posible que los componentes nuevos devuelvan resultados diferentes a los componentes anteriores cuando se rellenan y consultan índices de texto completo. Las tablas siguientes muestran algunas de las diferencias que se pueden esperar en los resultados en inglés.  
  
 Si tiene que conservar el comportamiento anterior de los separadores de palabras y lematizadores, vea los siguientes temas:  
  
-   [Cambiar el separador de palabras usado para el inglés de Estados Unidos y el del Reino Unido](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [Revertir los separadores de palabras usados por las búsquedas a la versión anterior](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 En algunos casos, los componentes nuevos devuelven *más* resultados:  
  
|**Término**|**Resultados con los separadores de palabras y el lematizador anteriores**|**Resultados con los separadores de palabras y lematizadores**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|gato-perro|cat<br /><br /> perro|cat<br /><br /> gato-perro<br /><br /> perro|  
|cat@dog.com|cat<br /><br /> com<br /><br /> perro|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> perro|  
|12/11/2011<br /><br /> *(donde el término es una fecha)*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 En algunos casos, los componentes nuevos devuelven resultados *similares* :  
  
|**Término**|**Resultados con los separadores de palabras y el lematizador anteriores**|**Resultados con los separadores de palabras y lematizadores**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *(donde el término es una hora)*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 En algunos casos, los componentes nuevos devuelven *menos* resultados o bien, las aplicaciones no esperan los resultados:  
  
|**Término**|**Resultados con los separadores de palabras y el lematizador anteriores**|**Resultados con los separadores de palabras y lematizadores**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jěˊÿｑℭžl<br /><br /> *(donde los términos no son caracteres válidos en español)*|'jěˊÿｑℭžl'|je yq zl|  
|table's|table's<br /><br /> table|table's|  
|gato-|cat<br /><br /> gato-|cat|  
|v-z *(donde v y z son palabras irrelevantes)*|*(sin resultados)*|v-z|  
|$100 000 USD|$100<br /><br /> 000<br /><br /> nn000<br /><br /> nn100$<br /><br /> usd|$100 000 USD<br /><br /> nn100000usd|  
|bonita tierra americana|bonita<br /><br /> tierra<br /><br /> norteamericana<br /><br /> americana|bonita<br /><br /> tierra|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>Cambios de comportamiento en la búsqueda de texto completo en SQL Server 2008  
 En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] y versiones posteriores, el motor de texto completo se integra como un servicio de base de datos en la base de datos relacional como parte de la infraestructura del motor de almacenamiento y la consulta del servidor. La nueva arquitectura de búsqueda de texto completo logra los objetivos siguientes:  
  
-   Administración y almacenamiento integrados: la búsqueda de texto completo ahora se integra directamente con las características de administración y almacenamiento inherentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , y el servicio MSFTESQL ya no existe.  
  
    -   Los índices de texto completo se almacenan en grupos de archivos de base de datos en lugar de hacerlo en el sistema de archivos. Las operaciones administrativas que se llevan a cabo en una base de datos, como la creación de una copia de seguridad, afectan a los índices de texto completo de forma automática.  
  
    -   Un catálogo de texto completo es ahora un objeto virtual que no pertenece a ningún grupo de archivos; es un concepto lógico que hace referencia a un grupo de índices de texto completo. Por tanto, muchas de las características de administración de catálogos se han quedado desusadas, lo que ha provocado cambios de última hora en algunas características. Para obtener más información, vea [características Desusadas motor de base de datos en SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md) y [cambios importantes en la búsqueda de texto completo](breaking-changes-to-full-text-search.md).  
  
        > [!NOTE]  
        >  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]Las [!INCLUDE[tsql](../includes/tsql-md.md)] instrucciones DDL que especifican los catálogos de texto completo funcionan correctamente.  
  
-   Procesamiento de consultas integrado: el nuevo procesador de consultas de búsqueda de texto completo forma parte del Motor de base de datos y está totalmente integrado con el procesador de consultas de SQL Server. Esto significa que, el optimizador de consultas reconoce los predicados de consulta de texto completo y los ejecuta automáticamente de la forma más eficaz posible.  
  
-   Administración mejorada y solución de problemas: la búsqueda de texto completo integrada proporciona herramientas para ayudarle a analizar estructuras de búsqueda como el índice de texto completo, la salida de un separador de palabras determinado, una configuración de palabra irrelevante, etc.  
  
-   Las listas de palabras irrelevantes han reemplazado a los archivos de palabras irrelevantes. Una lista de palabras irrelevantes es un objeto de base de datos que facilita las tareas de administración de las palabras irrelevantes y mejora la integridad entre instancias de servidor y entornos diferentes. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] y versiones posteriores incluyen nuevos separadores de palabras para muchos de los idiomas de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Los únicos separadores de palabras que siguen siendo iguales son los de inglés, coreano, tailandés y chino (tradicional y simplificado). En el caso de otros idiomas, si se importó un catálogo de texto completo cuando una [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] base de datos se actualizó a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o a una versión posterior, es posible que uno o varios de los idiomas usados por los índices de texto completo del catálogo de texto completo estén asociados a nuevos separadores de palabras que podrían comportarse de forma ligeramente diferente a los separadores de palabras importados Para obtener más información sobre cómo garantizar la coherencia entre las consultas y el contenido del índice de texto completo, vea [actualizar la búsqueda de texto completo](../relational-databases/search/upgrade-full-text-search.md).  
  
-   Se ha agregado un nuevo servicio del iniciador del FDHOST (MSSQLFDLauncher). Para obtener más información, consulte Introducción [a la búsqueda de texto completo](../relational-databases/search/get-started-with-full-text-search.md).  
  
-   La indización de texto completo funciona con una columna [FileStream](../relational-databases/blob/filestream-sql-server.md) del mismo modo que con una `varbinary(max)` columna. La tabla FILESTREAM debe tener una columna con la extensión de nombre de archivo para cada BLOB FILESTREAM. Para obtener más información, vea [consultar con búsqueda de texto completo](../relational-databases/search/query-with-full-text-search.md),[configurar y administrar filtros para búsquedas](../relational-databases/search/configure-and-manage-filters-for-search.md)y [Sys. fulltext_document_types &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
     El motor de texto completo indiza el contenido de los BLOB FILESTREAM. Indizar archivos como las imágenes podría no ser útil. Cuando se actualiza un BLOB FILESTREAM, vuelve a indizarse.  
  
## <a name="see-also"></a>Consulte también  
 [Búsqueda de texto completo](../relational-databases/search/full-text-search.md)   
 [Compatibilidad con versiones anteriores de búsqueda de texto completo](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [Actualizar la búsqueda de texto completo](../relational-databases/search/upgrade-full-text-search.md)   
 [Introducción a la búsqueda de texto completo](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
