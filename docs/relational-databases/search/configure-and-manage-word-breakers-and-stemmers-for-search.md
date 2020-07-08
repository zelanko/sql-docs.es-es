---
title: Configuración y administración de separadores de palabras y lematizadores para la búsqueda
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 8ae5dbc9652ed690edc6964db38cc8e0d5536625
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85629526"
---
# <a name="configure--manage-word-breakers--stemmers-for-search-sql-server"></a>Configuración y administración de separadores de palabras y lematizadores para la búsqueda (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
Los separadores de palabras y lematizadores realizan un análisis lingüístico de todos los datos indizados de texto completo. El análisis lingüístico realiza las siguientes dos cosas:

-   **Buscar los límites de palabras (separación de palabras)** . El *separador de palabras* identifica las palabras individuales determinando los límites de palabras en función de las reglas léxicas de ese idioma. Cada palabra (también conocida como *token*) se inserta en el índice de texto completo usando una representación comprimida para reducir su tamaño.

-   **Conjugar verbos (lematización)** . El *lematizador* genera las formas de inflexión de una palabra determinada en función de las reglas de ese idioma (por ejemplo, "corriendo", "corrió" y "corredor" son varias formas de la palabra "carrera").

## <a name="word-breakers-and-stemmers-are-language-specific"></a>Los separadores de palabras y los lematizadores son específicos del idioma

Los separadores de palabras y lematizadores son específicos del idioma, y las reglas para el análisis lingüístico difieren en los diferentes idiomas. Los separadores de palabras específicos del idioma hacen que los términos resultantes sean más precisos para dicho idioma.

Para usar los separadores de palabras y lematizadores proporcionados para todos los idiomas compatibles con SQL Server, normalmente no es necesario realizar ninguna acción.

-   Cuando hay un separador de palabras para la familia de idiomas, pero no para el subidioma específico, se utiliza el del idioma principal. Por ejemplo, el separador de palabras del francés se utiliza en el texto escrito en francés de Canadá.
-   Si no hay ningún separador de palabras disponible para un idioma concreto, se utiliza el separador de palabras neutral. El separador de palabras neutral divide las palabras en caracteres neutrales como espacios y marcas de puntuación.

## <a name="get-the-list-of-supported-languages"></a>Obtener una lista de los idiomas admitidos

Para ver la lista de los idiomas que la búsqueda de texto completo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite, utilice la siguiente instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)]. La presencia de un idioma en esta lista indica que los separadores de palabras se registran para el idioma. 
  
```sql
SELECT * FROM sys.fulltext_languages
```

##  <a name="get-the-list-of-registered-word-breakers"></a><a name="register"></a> Obtener la lista de separadores de palabras registrados

Para que la búsqueda de texto completo use los separadores de palabras para un idioma, deben estar registrados. Con los separadores de palabras registrados, los recursos lingüísticos asociados (lematizadores, palabras irrelevantes y archivos de sinónimos) también están disponibles para las operaciones de indización y consulta de texto completo.

Para ver la lista de componentes de separadores de palabras registrados, utilice la siguiente instrucción.

```sql
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```

Para obtener opciones adicionales y más información, vea [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md).
 
## <a name="if-you-add-or-remove-a-word-breaker"></a>Si agrega o quita un separador de palabras  
Si agrega, quita o modifica un separador de palabras, necesita actualizar la lista de identificadores de configuración regional (LCID) de Microsoft Windows que se admiten para la indización y las consultas de texto completo. Para obtener más información, consulte [ver o cambiar los filtros registrados y separadores de palabras](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="set-the-default-full-text-language-option"></a><a name="default"></a> Establecer la opción Idioma de texto completo predeterminado  
 En las versiones localizadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establece la opción **Idioma de texto completo predeterminado** en el idioma del servidor, si existe una correspondencia apropiada. En el caso de una versión no localizada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el valor de la opción **Idioma de texto completo predeterminado** es Inglés.  
  
 Al crear o modificar un índice de texto completo, puede especificar un idioma diferente para cada columna indizada de texto completo. Si no se especifica ningún idioma para una columna, el valor predeterminado es el de la opción de configuración **Idioma de texto completo predeterminado**.  
  
> [!NOTE]  
>  Todas las columnas de una cláusula de función de consulta de texto completo deben utilizar el mismo idioma, a menos que se especifique la opción LANGUAGE en la consulta. El idioma de la columna indexada de texto completo que se consulta determina el análisis lingüístico realizado en los argumentos de los predicados de la consulta de texto completo ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) y [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) y de las funciones ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) y [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)).  
  
##  <a name="choose-the-language-for-an-indexed-column"></a><a name="lang"></a> Elegir el idioma para una columna indizada  
 Al crear un índice de texto completo, es recomendable que especifique un idioma para cada columna indizada. Si un idioma no se especifica para una columna, el sistema utiliza el idioma predeterminado del sistema. El idioma de una columna determina el separador de palabras y el lematizador que se utilizará para indizar esa columna. Además, las consultas de texto completo de la columna utilizarán el archivo de diccionario de sinónimos del idioma.  
  
 Hay varios aspectos que deben tenerse en cuenta al elegir el idioma de columna cuando se crea un índice de texto completo. Estas consideraciones se refieren al modo en que se acorta el texto y se indiza a continuación mediante el motor de texto completo. Para obtener más información, vea [Elegir un idioma al crear un índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
Para ver el idioma del separador de palabras de determinadas columnas, ejecute la siguiente instrucción.
   
```sql 
SELECT language_id AS 'LCID' FROM sys.fulltext_index_columns;
```  

Para más información y opciones adicionales, vea [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md).

##  <a name="troubleshoot-word-breaking-time-out-errors"></a><a name="tshoot"></a> Solucionar problemas de errores de tiempo de espera en la separación de palabras  
 Se puede producir un error de tiempo de espera en la separación de palabras en diversas situaciones. Para más información sobre estas situaciones y cómo responder en cada situación, vea [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md).

### <a name="info-about-the-mssqlserver_30053-error"></a>Información sobre el error MSSQLSERVER_30053
  
|Propiedad|Value|
|-|-|
|Nombre de producto|SQL Server|  
|Id. de evento|30053|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|Texto del mensaje|Se agotó el tiempo de espera de separación de palabras para la cadena de consulta de texto completo. Esto puede ocurrir si el divisor de palabras tarda mucho tiempo en procesar la cadena de consulta de texto completo, o si se está ejecutando un gran número de consultas en el servidor. Intente ejecutar de nuevo la consulta con menos carga.|  
  
#### <a name="explanation"></a>Explicación  
 Se puede producir un error de tiempo de espera en la separación de palabras en las situaciones siguientes:  
  
-   El separador de palabras para el lenguaje de consultas está configurado incorrectamente; por ejemplo, la configuración del Registro es incorrecta.  
  
-   El separador de palabras no funciona correctamente para una cadena de consulta determinada.  
  
-   El separador de palabras devuelve demasiados datos para una cadena de consulta determinada. Un exceso de datos se trata como un ataque potencial por saturación del búfer y se cierra el proceso de demonio de filtro (fdhost.exe), que hospeda los servicios de separación de palabras.  
  
-   La configuración del proceso de demonio de filtro es incorrecta.  
  
     Los problemas de configuración más comunes son la expiración de las contraseñas o una política de dominio que impide que la cuenta de demonio de filtro inicie sesión.  
  
-   Una carga de trabajo de consulta muy pesada se ejecuta en la instancia del servidor; por ejemplo, el separador de palabras tardó mucho en procesar la cadena de consulta de texto completo o un número grande de consultas se está ejecutando en el servidor. Tenga en cuenta que esta es la causa menos probable.  
  
#### <a name="user-action"></a>Acción del usuario  
 Seleccione la acción del usuario que sea adecuada según la causa probable de tiempo de espera, de la forma siguiente:  
  
|Causa probable|Acción del usuario|  
|--------------------|-----------------|  
|El separador de palabras del lenguaje de consulta está configurado incorrectamente.|Si usa un separador de palabras de otro fabricante, podría estar registrado incorrectamente en el sistema operativo. En este caso, registre de nuevo el separador de palabras. Para más información, vea [Revertir los separadores de palabras usados por las búsquedas a la versión anterior](revert-the-word-breakers-used-by-search-to-the-previous-version.md) (Revertir los separadores de palabras usados por las búsquedas a la versión anterior).|  
|El separador de palabras no funciona correctamente para una cadena de consulta determinada.|Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el separador de palabras, póngase en contacto con el Servicio de atención al cliente y soporte técnico de Microsoft.|  
|El separador de palabras devuelve demasiados datos para una cadena de consulta determinada.|Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el separador de palabras, póngase en contacto con el Servicio de atención al cliente y soporte técnico de Microsoft.|  
|La configuración del proceso de demonio de filtro es incorrecta.|Asegúrese de que está utilizando la contraseña actual y que una directiva de dominio no está evitando que la cuenta de demonio de filtro se registre.|  
|Se está ejecutando un alto volumen de carga de trabajo de consultas en la instancia de servidor.|Intente ejecutar de nuevo la consulta con menos carga.|  

##  <a name="understand-the-impact-of-updated-word-breakers"></a><a name="impact"></a> Descripción del impacto de separadores de palabras actualizados  
 Cada versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente incluye nuevos separadores de palabras que tienen mejores reglas lingüísticas y son más precisos que los anteriores separadores de palabras. Los nuevos separadores de palabras podrían comportarse de manera ligeramente diferente que los separadores de palabras de los índices de texto completo que se importaron de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
Esto es relevante si se importó un catálogo de texto completo cuando una base de datos se actualizó a la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un o varios idiomas que Usen los índices de texto completo del catálogo de texto completo podrían estar asociados ahora a nuevos separadores de palabras. Para obtener más información, vea [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
 
## <a name="see-also"></a>Consulte también  
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)    
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   

