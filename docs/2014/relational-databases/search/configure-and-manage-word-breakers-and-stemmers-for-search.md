---
title: Configurar y administrar separadores de palabras y lematizadores para la búsqueda | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 88
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4c3bfb07ca9730b8c03cb56f07464355c392bda6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204570"
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>Configurar y administrar separadores de palabras y lematizadores para la búsqueda
  Los separadores de palabras y lematizadores realizan un análisis lingüístico de todos los datos indizados de texto completo. El análisis lingüístico incluye la búsqueda de los límites de las palabras (separación de palabras) y la conjugación de los verbos (lematización). Los separadores de palabras y lematizadores son específicos del idioma, y las reglas para el análisis lingüístico difieren en los diferentes idiomas. Para un idioma determinado, un *separador de palabras* identifica las palabras individuales determinando los límites de palabras en función de las reglas léxicas de ese idioma. Cada palabra (también conocida como *token*) se inserta en el índice de texto completo usando una representación comprimida para reducir su tamaño. El *lematizador* genera las formas de inflexión de una palabra determinada en función de las reglas de ese idioma (por ejemplo, "corriendo", "corrió" y "corredor" son varias formas de la palabra "carrera").  
  
 El uso de separadores de palabras específicos del idioma permite que los términos resultantes sean más precisos para dicho idioma. Cuando hay un separador de palabras para la familia de idiomas, pero no para el subidioma específico, se utiliza el del idioma principal. Por ejemplo, el separador de palabras del francés se utiliza en el texto escrito en francés de Canadá. Si no hay ningún separador de palabras disponible para un idioma concreto, se utiliza el separador de palabras neutral. El separador de palabras neutral divide las palabras en caracteres neutrales como espacios y marcas de puntuación.  
  
##  <a name="register"></a> Registrar separadores de palabras  
 Para usar los separadores de palabras de un idioma, se deben registrar. Con los separadores de palabras registrados, los recursos lingüísticos asociados (lematizadores, palabras irrelevantes y archivos de sinónimos) también están disponibles para las operaciones de indización y consulta de texto completo. Para ver una lista de los idiomas cuyos separadores de palabras están registrados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
 SELECT * FROM sys.fulltext_languages  
  
 Si agrega, quita o modifica un separador de palabras, necesita actualizar la lista de identificadores de configuración regional (LCID) de Microsoft Windows que se admiten para la indización y las consultas de texto completo. Para obtener más información, consulte [View or Change Registered Filters and Word Breakers](view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="default"></a> Establecer la opción Default Full-Text Language  
 Las versiones localizadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación establece la `default full-text language` opción para el idioma del servidor si existe una correspondencia apropiada. Para obtener una versión no localizada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el `default full-text language` opción es el inglés.  
  
 Al crear o modificar un índice de texto completo, puede especificar un idioma diferente para cada columna indizada de texto completo. Si no se especifica ningún idioma para una columna, el valor predeterminado es el de la opción de configuración `default full-text language`.  
  
> [!NOTE]  
>  Todas las columnas de una cláusula de función de consulta de texto completo deben utilizar el mismo idioma, a menos que se especifique la opción LANGUAGE en la consulta. El idioma de la columna indexada de texto completo que se consulta determina el análisis lingüístico realizado en los argumentos de los predicados de la consulta de texto completo ([CONTAINS](/sql/t-sql/queries/contains-transact-sql) y [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)) y de las funciones ([CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) y [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql)).  
  
##  <a name="lang"></a> Elegir el idioma para una columna indizada  
 Al crear un índice de texto completo, es recomendable que especifique un idioma para cada columna indizada. Si un idioma no se especifica para una columna, el sistema utiliza el idioma predeterminado del sistema. El idioma de una columna determina el separador de palabras y el lematizador que se utilizará para indizar esa columna. Además, las consultas de texto completo de la columna utilizarán el archivo de diccionario de sinónimos del idioma.  
  
 Hay varios aspectos que deben tenerse en cuenta al elegir el idioma de columna cuando se crea un índice de texto completo. Estas consideraciones se refieren al modo en que se acorta el texto y se indiza a continuación mediante el motor de texto completo. Para obtener más información, vea [Elegir un idioma al crear un índice de texto completo](choose-a-language-when-creating-a-full-text-index.md).  
  
 **Para ver el idioma del separador de palabras de una columna**  
  
-   [Administrar índices de texto completo](../indexes/indexes.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> Obtener información sobre los separadores de palabras  
 **Ver el resultado de tokenización de una combinación de separador, diccionario de sinónimos y lista de palabras irrelevantes de word**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql).  
  
 **Para devolver información sobre los separadores de palabras registrados**  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="tshoot"></a> Solución de problemas de errores de tiempo de espera de separación de palabras  
 Se puede producir un error de tiempo de espera en la separación de palabras en diversas situaciones. Para obtener más información sobre estas situaciones y cómo responder en cada situación, vea [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md).  
  
##  <a name="impact"></a> Comprensión del impacto de nuevos separadores de palabras  
 Cada versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente incluye nuevos separadores de palabras que tienen mejores reglas lingüísticas y son más precisos que los anteriores separadores de palabras. Los nuevos separadores de palabras podrían comportarse de manera ligeramente diferente que los separadores de palabras de los índices de texto completo que se importaron de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto es relevante si se importó un catálogo de texto completo cuando una base de datos se actualizó a la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un o varios idiomas que Usen los índices de texto completo del catálogo de texto completo podrían estar asociados ahora a nuevos separadores de palabras. Para obtener más información, vea [Actualizar la búsqueda de texto completo](upgrade-full-text-search.md).  
  
 Para obtener una lista completa de todos los separadores de palabras, vea [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Actualizar la búsqueda de texto completo](upgrade-full-text-search.md)  
  
  
