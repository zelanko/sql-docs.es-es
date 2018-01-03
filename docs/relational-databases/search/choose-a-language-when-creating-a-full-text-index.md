---
title: "Elección de un idioma al crear un índice de texto completo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: database-engine, sql-database
ms.component: search
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- languages [full-text search]
- full-text indexes [SQL Server], languages
- international considerations [full-text search]
- stemmers [full-text search]
- global considerations [full-text search]
- full-text search [SQL Server], international considerations
- languages [SQL Server], full-text indexes
- word breakers [full-text search]
ms.assetid: 670a5181-ab80-436a-be96-d9498fbe2c09
caps.latest.revision: "49"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d70cc0b053c776f56041fbf961de711c4ad5c26
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="choose-a-language-when-creating-a-full-text-index"></a>Elegir un idioma al crear un índice de texto completo

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Al crear un índice de texto completo, tiene que especificar un idioma de columna para la columna indizada. Las consultas de texto completo usarán el [separador de palabras y los lematizadores](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) del idioma especificado en la columna. Hay varios aspectos que deben tenerse en cuenta al elegir el idioma de columna cuando se crea un índice de texto completo. Estas consideraciones se refieren al modo en que se acorta el texto y se indiza a continuación mediante el motor de texto completo.  
  
> [!NOTE]  
>  Para especificar un idioma de columna para una columna de índice de texto completo, use la cláusula LANGUAGE *language_term* al especificar la columna. Para obtener más información, vea [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md) y [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
##  <a name="langsupp"></a> Compatibilidad con idiomas en la búsqueda de texto completo  
 Esta sección proporciona una introducción a los separadores de palabras y lematizadores, y explica cómo usa la búsqueda de texto completo el LCID del idioma de columna.  
  
### <a name="introduction-to-word-breakers-and-stemmers"></a>Introducción a los separadores de palabras y lematizadores  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y las versiones posteriores incluyen una nueva familia completa de separadores de palabras y lematizadores que son significativamente mejores que los que estaban disponibles anteriormente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  El grupo de idiomas naturales de Microsoft, Microsoft Natural Language Group (MS NLG), implementó estos nuevos componentes lingüísticos y los admite.  
  
 Los nuevos separadores de palabras proporcionan las ventajas siguientes:  
  
-   Solidez  
  
     Las pruebas han demostrado que los nuevos separadores de palabras son sólidos en entornos de consulta sometidos a una presión elevada.  
  
-   Seguridad  
  
     Los nuevos separadores de palabras están habilitados de forma predeterminada en SQL Server gracias a las mejoras de seguridad de los componentes lingüísticos. Se recomienda encarecidamente que se firmen los componentes externos, como son los separadores de palabras y los filtros, con el fin de mejorar la seguridad general y la solidez de SQL Server. Puede configurar el texto completo para comprobar que estos componentes se firman de la forma siguiente:  
  
    ```  
    EXEC sp_fulltext_service 'verify_signature';  
    ```  
  
-   Calidad  
  
     Los separadores de palabras se han rediseñado y las pruebas muestran que los nuevos proporcionan una mejor calidad semántica que los anteriores. De esta forma, se incrementa la exactitud de recuperación.  
  
-   Los separadores de palabras, con cobertura de una amplia lista de idiomas, se incluyen en SQL Server directamente y se habilitan de forma predeterminada.  
  
 Para obtener una lista de los idiomas para los que SQL Server incluye un separador de palabras y lematizadores, vea [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
  
### <a name="how-full-text-search-uses-the-name-of-the-column-level-language"></a>Cómo usa la búsqueda de texto completo el nombre del idioma de columna  
 Al crear un índice de texto completo, tiene que especificar un nombre de idioma válido para cada columna. Si un nombre de idioma es válido pero no lo devuelve la vista de catálogo [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) , la búsqueda de texto completo vuelve al nombre de idioma disponible más próximo de la misma familia de idiomas, si lo hubiera. De lo contrario, la búsqueda de texto completo retrocede al separador de palabras neutro. Este comportamiento de retroceso podría afectar a la exactitud de recuperación. Por consiguiente recomendamos encarecidamente que especifique un nombre de idioma válido y disponible para cada columna al crear un índice de texto completo.  
  
> [!NOTE]  
>  El LCID se usa con todos los tipos de datos aptos para la indexación de texto completo (como **char** o **nchar**). Aunque el criterio de ordenación de una columna de tipo **char**, **varchar**o **text** esté establecido en una configuración de idioma distinta del identificado por el LCID, el LCID se usa de todos modos durante la indexación de texto completo y en las consultas de esas columnas.  
  
  
##  <a name="breaking"></a> Separación de palabras  
 Un separador de palabras acorta el texto que se va a indizar en límites de palabras, que son específicas del idioma. Por consiguiente, el comportamiento de separación de palabras difiere entre los diferentes idiomas. Si utiliza un idioma x para indizar varios idiomas {x, y y, z}, parte del comportamiento podría producir resultados inesperados. Por ejemplo un guión (-) o una coma (,) podrían ser elementos separadores de palabras que no se tienen en cuenta en un idioma, pero sí en otro. También, en raras ocasiones, se podría producir un comportamiento de lematización inesperado debido a que una palabra determinada podría derivarse de manera diferente en idiomas distintos. Por ejemplo, en inglés estos límites de palabras suelen ser espacios en blanco o alguna forma de puntuación. En otros idiomas, como el alemán, las palabras o caracteres se pueden combinar. Por consiguiente, el idioma de columna que elija debería representar el idioma que espera que se almacene en las filas de esa columna.  
  
### <a name="western-languages"></a>Idiomas occidentales  
 Para la familia de idiomas occidentales, si duda de qué idiomas se van a almacenar en una columna o espera que se almacene más de uno, una solución alternativa general es utilizar el separador de palabras para el idioma más complejo que pueda almacenarse en la columna. Por ejemplo, imagine que en una columna cree que puede almacenarse contenido en inglés, español y alemán. Estos tres idiomas occidentales poseen patrones de separación de palabras muy similares y los patrones del alemán son los más complejos. Por consiguiente, una buena opción en este caso sería utilizar el separador de palabras alemán, que debería poder procesar correctamente el texto inglés y español. Por el contrario, el separador de palabras inglés no podría procesar perfectamente el texto alemán debido a sus palabras compuestas.  
  
 Tenga en cuenta que al utilizar el separador de palabras del idioma más complejo de una familia de idiomas, no se garantiza una indización perfecta de todos los idiomas de la familia. Podrían darse casos excepcionales en los que el separador de palabras más complejo no pudiera tratar correctamente el texto escrito en otro idioma.  
  
  
### <a name="non-western-languages"></a>Idiomas no occidentales  
 Para los idiomas no occidentales (como el chino, japonés, hindi, etc.) la solución alternativa anterior no funciona necesariamente, por razones lingüísticas. En los idiomas no occidentales, considere una de las soluciones alternativas siguientes:  
  
-   Para idiomas de familias diferentes  
  
     Si una columna puede contener idiomas drásticamente diferentes, por ejemplo, español y japonés, considere almacenar el contenido de los distintos idiomas en columnas independientes. Esto le permitiría utilizar el separador de palabras específico del idioma para cada columna. Si elige esta solución y no conoce el idioma de las consultas en el momento de la consulta, puede que tenga que emitir la consulta en ambas columnas para asegurarse de que encuentra la fila o documento correctos.  
  
-   Para contenido binario (como los documentos de Microsoft Word)  
  
     Cuando el contenido indexado es del tipo **binary** , el filtro de la búsqueda de texto completo que procesa el contenido de texto antes de enviarlo al separador de palabras podría observar las etiquetas del idioma concreto que existan dentro del archivo binario. En este caso, en el momento de la indización, el filtro emitirá el LCID correcto para un documento o sección de un documento. A continuación, el motor de texto completo llamará al separador de palabras del idioma con ese LCID. Sin embargo, después de indizar contenido de varios idiomas, recomendamos que compruebe que la operación se realizó correctamente.  
  
-   Para contenido de texto simple  
  
     Cuando el contenido sea texto simple, puede convertirlo al tipo de datos **xml** y agregar etiquetas de idioma que indiquen el idioma que corresponde a cada documento concreto o sección del documento. Para que esto funcione, sin embargo, tiene que conocer el idioma antes de la indización de texto completo.  
  
  
##  <a name="stemming"></a> Lematización  
 Una consideración adicional al elegir el idioma de columna es la lematización. En las consultas de texto completo, la*lematización* es un proceso de búsqueda de todas las formas con inflexión de una palabra en un idioma determinado. Al utilizar un separador de palabras genérico para procesar varios idiomas, el proceso de lematización solo funciona para el idioma especificado de la columna, no para otros idiomas de la misma. Por ejemplo, los lematizadores de alemán no funcionan para inglés o español (etc.). Esto podría afectar a su recuperación, según el idioma que elija en el momento de la consulta.  
  
  
##  <a name="type"></a> Efecto del tipo de columna en la búsqueda de texto completo  
 Otra consideración en la elección del idioma se refiere al modo en que se representan los datos. En los datos que no se almacenan en la columna **varbinary(max)** , no se realiza ningún proceso de filtro especial. sino que el texto suele pasarse por el componente separador de palabras tal y como es.  
  
 Además, los separadores de palabras se han diseñado principalmente para procesar el texto escrito. Por ello, si el texto contiene algún tipo de marcado (por ejemplo, HTML), es posible que los procesos de indización y búsqueda no se realicen con gran precisión lingüística. En tal caso, tiene dos opciones: el método preferido es almacenar simplemente los datos de texto en la columna **varbinary(max)** , o indicar su tipo de documento para poder filtrarlo. o utilizar el separador de palabras neutral y, si es posible, agregar datos de marcado (como 'br' en HTML) a las listas de palabras irrelevantes.  
  
> [!NOTE]  
>  La lematización basada en el idioma no interviene cuando se especifica el idioma neutral.  
  
  
##  <a name="nondef"></a> Especificar un idioma de columna no predeterminado en una consulta de texto completo  
 De forma predeterminada, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la búsqueda de texto completo analizará los términos de consulta mediante el idioma especificado para cada columna que se incluya en la cláusula de texto completo. Para invalidar este comportamiento, especifique un idioma no predeterminado en el momento de la consulta. Para los idiomas admitidos cuyos recursos estén instalados, se puede usar la cláusula LANGUAGE *language_term* de una consulta [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)o [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) para especificar el idioma que se usa para la separación de palabras, la lematización, el diccionario de sinónimos y el procesamiento de las palabras irrelevantes de los términos de las consultas.  
  
  
## <a name="see-also"></a>Ver también  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Configurar y administrar filtros para búsquedas](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
