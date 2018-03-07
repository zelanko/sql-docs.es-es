---
title: ALTER FULLTEXT INDEX (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT INDEX
- ALTER_FULLTEXT_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- modifying full-text indexes
- full-text indexes [SQL Server], modifying
- search property lists [SQL Server], associating with full-text indexes
- ALTER FULLTEXT INDEX statement
ms.assetid: b6fbe9e6-3033-4d1b-b6bf-1437baeefec3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 022cec421b1827c525d18d04d42bdd648936d147
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="alter-fulltext-index-transact-sql"></a>ALTER FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cambia las propiedades de un índice de texto completo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER FULLTEXT INDEX ON table_name  
   { ENABLE   
   | DISABLE  
   | SET CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF }  
   | ADD ( column_name   
           [ TYPE COLUMN type_column_name ]   
           [ LANGUAGE language_term ]  
           [ STATISTICAL_SEMANTICS ]  
           [,...n]   
         )  
     [ WITH NO POPULATION ]  
   | ALTER COLUMN column_name  
     { ADD | DROP } STATISTICAL_SEMANTICS  
     [ WITH NO POPULATION ]  
   | DROP ( column_name [,...n] )  
     [ WITH NO POPULATION ]   
   | START { FULL | INCREMENTAL | UPDATE } POPULATION  
   | {STOP | PAUSE | RESUME } POPULATION   
   | SET STOPLIST [ = ] { OFF| SYSTEM | stoplist_name }  
     [ WITH NO POPULATION ]   
   | SET SEARCH PROPERTY LIST [ = ] { OFF | property_list_name }  
     [ WITH NO POPULATION ]   
   }  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 Es el nombre de la tabla o vista indizada que contiene la columna o columnas incluidas en el índice de texto completo. Especificar los nombres de la base de datos y del propietario de la tabla es opcional.  
  
 ENABLE | DISABLE  
 Indica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si debe recopilar texto datos de índice para *table_name*. ENABLE activa el índice de texto completo; DISABLE lo desactiva. La tabla no admitirá las consultas de texto completo mientras esté deshabilitado el índice.  
  
 La deshabilitación de un índice de texto completo permite desactivar el seguimiento de cambios y mantener el índice de texto completo, que puede reactivar en cualquier momento con ENABLE. Cuando se deshabilita el índice de texto completo, los metadatos del índice de texto completo permanecen en las tablas del sistema. Si CHANGE_TRACKING está habilitado (actualización automática o manual) cuando se deshabilita el índice de texto completo, el estado del índice se inmoviliza, los rastreos en curso se detienen y no se mantiene un seguimiento de los nuevos cambios en los datos de la tabla ni se propagan los cambios al índice.  
  
 SET CHANGE_TRACKING {MANUAL | AUTO | OFF}   
 Especifica si los cambios (actualizaciones, eliminaciones o inserciones) realizados en columnas de tabla que están cubiertas por el índice de texto completo se propagarán por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al índice de texto completo. Los cambios realizados en los datos con WRITETEXT y UPDATETEXT no se reflejan en el índice de texto completo y no se recopilan con el seguimiento de cambios.  
  
> [!NOTE]  
>  Para obtener información sobre la interacción del seguimiento de cambios y WITH NO POPULATION, vea "Comentarios", posteriormente en este tema.  
  
 MANUAL  
 Especifica que se propagarán manualmente los cambios controlados mediante una llamada a la instrucción ALTER FULLTEXT INDEX … START UPDATE POPULATION [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción (*rellenado manual*). Puede utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para llamar a esta instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma periódica.  
  
 AUTO  
 Especifica que el seguimiento se propagarán automáticamente cuando se modifican los datos de la tabla base (*rellenado automático*). Aunque los cambios se propagan de forma automática, podrían no reflejarse de inmediato en el índice de texto completo. AUTO es el valor predeterminado.  
  
 OFF  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mantendrá una lista de cambios en los datos indizados.  
  
 AGREGAR | QUITAR *column_name*  
 Especifica las columnas que se agregarán o eliminarán de un índice de texto completo. La columna o columnas deben ser de tipo **char**, **varchar**, **nchar**, **nvarchar**, **texto**, **ntext**, **imagen**, **xml**, **varbinary**, o **varbinary (max)**.  
  
 Utilice la cláusula DROP solamente en columnas que se hayan habilitado previamente para la indización de texto completo.  
  
 Utilice TYPE COLUMN y LANGUAGE con la cláusula ADD para establecer estas propiedades en el *column_name*. Cuando se agrega una columna, el índice de texto completo de la tabla se debe rellenar de nuevo para que funcionen las consultas de texto completo en esta columna.  
  
> [!NOTE]  
>  Que se rellene el índice de texto completo una vez agregada o quitada una columna en un índice de texto completo depende de si está habilitado el seguimiento de cambios y de si se especifica WITH NO POPULATION. Para obtener más información, vea la sección "Comentarios" más adelante en este tema.  
  
 COLUMNA de tipo *type_column_name*  
 Especifica el nombre de una columna de tabla, *type_column_name*, que se usa para contener el tipo de documento para un **varbinary**, **varbinary (max)**, o **imagen** documento. Esta columna, denominada columna de tipo, contiene una extensión de archivo proporcionada por el usuario (.doc, .pdf, .xls, etc.). La columna de tipo debe ser de tipo **char**, **nchar**, **varchar**o **nvarchar**.  
  
 Especificar la columna de tipo *type_column_name* solo si *column_name* especifica un **varbinary**, **varbinary (max)** o  **imagen** columna, en el que los datos se almacenan como datos binarios; en caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error.  
  
> [!NOTE]  
>  Durante la indización, el motor de texto completo utiliza la abreviatura en la columna de tipo de cada fila de la tabla para identificar qué filtro de búsqueda de texto completo que se usará para el documento en *column_name*. El filtro carga el documento como un flujo binario, quita la información del formato y envía el texto del documento al componente de separador de palabras. Para obtener más información, vea [Configurar y administrar filtros para búsquedas](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 IDIOMA *language_term*  
 Es el idioma de los datos almacenados en **column_name**.  
  
 *language_term* es opcional y se puede especificar como una cadena, entero o un valor hexadecimal correspondiente al identificador de configuración regional (LCID) de un idioma. Si *language_term* se especifica, se aplicará el idioma que representa a todos los elementos de la condición de búsqueda. Si no se especifica ningún valor, el idioma de texto completo predeterminado de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usa la instancia.  
  
 Use la **sp_configure** procedimiento almacenado para acceder a información sobre el idioma de texto completo predeterminado de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
 Cuando se especifica como una cadena, *language_term* corresponde a la **alias** valor de columna en la **syslanguages** tabla del sistema. La cadena debe incluirse entre comillas simples, como en '*language_term*'. Cuando se especifica como un entero, *language_term* es el LCID real que identifica el idioma. Cuando se especifica como un valor hexadecimal, *language_term* 0 x seguido del valor hexadecimal del LCID. El valor hexadecimal no puede superar los ocho dígitos, incluidos los ceros a la izquierda.  
  
 Si el valor está en formato DBCS (juego de caracteres de doble byte), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo convertirá a Unicode.  
  
 Recursos, como separadores de palabras y lematizadores, deben estar habilitados para el idioma especificado como *language_term*. Si estos recursos no admiten el idioma especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error.  
  
 Para las columnas no BLOB y no XML que contienen datos de texto en varios idiomas o en los casos en que se desconoce el idioma del texto almacenado en la columna, utilice el recurso de idioma neutro (0x0). Para los documentos almacenados en columnas de tipo XML o BLOB, la codificación de idioma del documento se utilizará en el momento de la indización. Por ejemplo, en las columnas XML, el atributo xml:lang de los documentos XML identifica el idioma. En el momento de la consulta, el valor especificado previamente en *language_term* se convierte en el idioma predeterminado usado para las consultas de texto completo, a menos que *language_term* se especifica como parte de una consulta de texto completo.  
  
 STATISTICAL_SEMANTICS  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Crea los índices adicionales de similitud de documentos y frases clave que forman parte de la indización semántica estadística. Para obtener más información, vea [Búsqueda semántica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 [ **,***...n*]  
 Indica que se pueden especificar varias columnas para las cláusulas ADD, ALTER o DROP. Si se especifican varias columnas, sepárelas con comas.  
  
 WITH NO POPULATION  
 Especifica que el índice de texto completo no se rellenará después de que se realice una de las operaciones de columna ADD y DROP, o una operación SET STOPLIST. El índice se rellenará solamente si el usuario ejecuta un comando START...POPULATION.  
  
 Si se especifica NO POPULATION, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no rellena un índice. El índice se rellena únicamente cuando el usuario usa un comando ALTER FULLTEXT INDEX...START POPULATION. Cuando no se especifica NO POPULATION, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena el índice.  
  
 Si CHANGE_TRACKING está habilitado y se especifica WITH NO POPULATION, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error. Si CHANGE_TRACKING está habilitado y no se especifica WITH NO POPULATION, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza un rellenado completo en el índice.  
  
> [!NOTE]  
>  Para obtener más información acerca de la interacción del seguimiento de cambios y WITH NO POPULATION, vea "Comentarios", más adelante en este tema.  
  
 {ADD | DROP } STATISTICAL_SEMANTICS  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Habilita o deshabilita la indización semántica estadística de las columnas especificadas. Para obtener más información, vea [Búsqueda semántica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 START {FULL|INCREMENTAL|UPDATE} POPULATION  
 Indica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que comience el rellenado del índice de texto completo de *table_name*. Si ya hay un rellenado de índice de texto completo en curso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve una advertencia y no se inicia un nuevo llenado.  
  
 FULL  
 Especifica que se recuperarán todas las filas de la tabla para el indizado de texto completo, incluso si las filas ya se han indizado.  
  
 INCREMENTAL  
 Especifica que solo se recuperarán para el índice de texto completo las filas modificadas desde el último rellenado. INCREMENTAL se puede aplicar únicamente si la tabla tiene una columna de tipo **timestamp**. Si una tabla en el catálogo de texto completo no contiene una columna de tipo **marca de tiempo**, la tabla se somete a un llenado completo.  
  
 UPDATE  
 Especifica el procesamiento de todas las inserciones, actualizaciones o eliminaciones desde la última vez que se actualizó el índice de seguimiento de cambios. Debe estar habilitado el rellenado de seguimiento de cambios en la tabla, pero el índice de actualización en segundo plano o el seguimiento automático de cambios no se deben activar.  
  
 {STOP | PAUSE | RESUME } POPULATION   
 Detiene o pausa cualquier operación de rellenado en curso; o bien detiene o reanuda cualquier operación de rellenado en pausa.  
  
 STOP POPULATION no detiene el seguimiento automático de cambios ni el índice de actualización en segundo plano. Para detener el seguimiento de cambios, utilice SET CHANGE_TRACKING OFF.  
  
 PAUSE POPULATION y RESUME POPULATION solo se pueden usar para operaciones de rellenado completas. No son relevantes para otros tipos de operación de rellenado porque las otras operaciones de rellenado reanudan los rastreos desde el punto en que se detuvieron.  
  
 LISTA DE PALABRAS IRRELEVANTES CONJUNTO {DESACTIVADO | SISTEMA | *stoplist_name* }  
 Cambia la lista de palabras irrelevantes de texto completo asociada al índice, si hay alguna.  
  
 OFF  
 Especifica que no se asocie al índice de texto completo ninguna lista de palabras irrelevantes.  
  
 SYSTEM  
 Especifica que la lista de palabras irrelevantes predeterminada de texto completo del sistema se debe usar para este índice de texto completo.  
  
 *stoplist_name*  
 Especifica el nombre de la lista de palabras irrelevantes que se va a asociar al índice de texto completo.  
  
 Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 LISTA DE PROPIEDADES DE BÚSQUEDA DE CONJUNTO {DESACTIVADO | *property_list_name* } [WITH NO POPULATION]  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Cambia la lista de propiedades de búsqueda asociada al índice, si hay alguna.  
  
 OFF  
 Especifica que no se asocie al índice de texto completo ninguna lista de propiedades. Al desactivar la lista de propiedades de búsqueda de un índice de texto completo (ALTER FULLTEXT INDEX... SET SEARCH PROPERTY LIST OFF), la búsqueda de propiedades en la tabla base ya no es posible.  
  
 De forma predeterminada, cuando se desactiva una lista de propiedades de búsqueda existente, el índice de texto completo se vuelve a rellenar automáticamente. Si se especifica WITH NO POPULATION al desactivar la lista de propiedades de búsqueda, este rellenado automático no sucede. Sin embargo, se recomienda ejecutar, si procede, un rellenado completo del índice de texto completo para mayor comodidad. Al rellenar el índice de texto completo, se eliminan los metadatos específicos de cada propiedad de búsqueda que se haya quitado, con lo que el índice de texto completo resultará más pequeño y eficaz.  
  
 *property_list_name*  
 Especifica el nombre de la lista de propiedades de búsqueda que se va a asociar al índice de texto completo.  
  
 Para agregar una lista de propiedades de búsqueda a un índice de texto completo es preciso rellenar el índice, a fin de indizar las propiedades de búsqueda que se han registrado para la lista de propiedades de búsqueda asociada. Si se especifica WITH NO POPULATION al agregar la lista de propiedades de búsqueda, se deberá ejecutar un rellenado del índice en un momento adecuado.  
  
> [!IMPORTANT]  
>  Si el índice de texto completo estaba asociado previamente a una lista de propiedades de búsqueda diferente, habrá que volver a generar la lista de propiedades para que el índice tenga un estado coherente. El índice se trunca inmediatamente y está vacío hasta que se ejecuta el rellenado completo. Para obtener más información acerca de cuándo las modificaciones realizadas en la lista de propiedades de búsqueda causan una nueva generación, vea "Comentarios", más adelante en este tema.  
  
> [!NOTE]  
>  Puede asociar una lista de propiedades de búsqueda a más de un índice de texto completo en la misma base de datos.  
  
 **Para buscar la propiedad de búsqueda listas en la base de datos actual**  
  
-   [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 Para obtener más información acerca de las listas de propiedades de búsqueda, vea [buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>Interacciones del seguimiento de cambios y del parámetro NO POPULATION  
 Que se rellene el índice de texto completo depende de si el seguimiento de cambios está habilitado y si se especifica WITH NO POPULATION en la instrucción ALTER FULLTEXT INDEX. En la tabla siguiente se resume el resultado de su interacción.  
  
|Seguimiento de cambios|WITH NO POPULATION|Resultado|  
|---------------------|------------------------|------------|  
|No se ha habilitado|No se ha especificado|Se realiza un rellenado completo en el índice.|  
|No se ha habilitado|Specified|No se produce el rellenado del índice hasta que se emite una instrucción ALTER FULLTEXT INDEX...START POPULATION.|  
|Habilitado|Specified|Se produce un error y no se altera el índice.|  
|Habilitado|No se ha especificado|Se realiza un rellenado completo en el índice.|  
  
 Para obtener más información acerca de cómo rellenar índices de texto completo, vea [rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="changing-the-search-property-list-causes-rebuilding-the-index"></a>Cambiar la lista de propiedades de búsqueda provoca un rellenado del índice  
 La primera vez que el índice de texto completo se asocia con una lista de propiedades de búsqueda, el índice debe volver a llenarse para incluir los términos de búsqueda específicos de la propiedad. Los datos del índice existente no se truncan.  
  
 Sin embargo, si se asocia el índice de texto completo con otra lista de propiedades, se vuelve a generar el índice. Una generación inmediata trunca el índice de texto completo y quita todos los datos existentes, de tal forma que el índice se debe volver a llenar. Mientras que la que progresa de rellenado, las consultas de texto completo en la tabla base buscan únicamente en las filas de tabla que ya se han indizado al efectuar el rellenado. Los datos del índice rellenado incluirán metadatos de las propiedades registradas en la lista de propiedades agregada recientemente.  
  
 Los escenarios que provocan una nueva generación son:  
  
-   Cambiar directamente a otra lista de propiedades de búsqueda (vea "Escenario A", más adelante en esta sección).  
  
-   Desactivar la lista de propiedades de lista y asociar después el índice con cualquier lista de propiedades de búsqueda (vea "Escenario B", más adelante en esta sección).  
  
> [!NOTE]  
>  Para obtener más información sobre el funcionamiento de la búsqueda de texto completo con listas de propiedades de búsqueda, vea [buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md). Para obtener información acerca de procesos de rellenado completos, vea [rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
### <a name="scenario-a-switching-directly-to-a-different-search-property-list"></a>Escenario A: cambiar directamente a otra lista de propiedades de búsqueda  
  
1.  Se crea un índice de texto completo en `table_1` con una lista de propiedades de búsqueda `spl_1`:  
  
    ```  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1,   
       CHANGE_TRACKING OFF, NO POPULATION;   
    ```  
  
2.  Se ejecuta un rellenado completo del índice de texto completo:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 START FULL POPULATION;  
    ```  
  
3.  Después, el índice de texto completo se asocia a otra lista de propiedades de búsqueda, `spl_2`, mediante la siguiente instrucción:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_2;  
    ```  
  
     Esta instrucción produce un rellenado completo, el comportamiento predeterminado.  Sin embargo, antes de empezar este rellenado, el motor de texto completo automáticamente trunca el índice.  
  
### <a name="scenario-b-turning-off-the-search-property-list-and-later-associating-the-index-with-any-search-property-list"></a>Escenario B: desactivar la lista de propiedades de búsqueda lista y después asociar el índice con cualquier lista de propiedades de búsqueda  
  
1.  Se crea un índice de texto completo en `table_1` con una lista de propiedades de búsqueda `spl_1`, seguido de un rellenado completo automático (comportamiento predeterminado):  
  
    ```  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1;   
    ```  
  
2.  La lista de propiedades de búsqueda se desactiva, como sigue:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1   
       SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
    ```  
  
3.  El índice de texto completo se asocia de nuevo a la misma lista de propiedades de búsqueda o a otra distinta.  
  
     Por ejemplo la instrucción siguiente vuelve a asociar el índice de texto completo con la lista de propiedades de búsqueda original, `spl_1`:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_1;  
    ```  
  
     Esta instrucción inicia un rellenado completo, el comportamiento predeterminado.  
  
    > [!NOTE]  
    >  La regeneración también se debería realizar para una lista de propiedades de búsqueda diferente, como `spl_2`.  
  
## <a name="permissions"></a>Permissions  
 El usuario debe tener el permiso ALTER en la tabla o vista indizada, o ser miembro de la **sysadmin** fija de servidor sysadmin o el **db_ddladmin** o **db_owner** funciones fijas de base de datos .  
  
 Si se especifica SET STOPLIST, el usuario debe tener el permiso REFERENCES en la lista de palabras irrelevantes. Si se especifica SET SEARCH PROPERTY LIST, el usuario debe tener el permiso REFERENCES para la lista de propiedades de búsqueda. El propietario de la lista de palabras irrelevantes o de la lista de propiedades de búsqueda especificadas puede conceder el permiso REFERENCES, si el propietario tiene permisos ALTER FULLTEXT CATALOG.  
  
> [!NOTE]  
>  Los usuarios tienen el permiso REFERENCES para la lista de palabras irrelevantes predeterminada que se incluye con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-setting-manual-change-tracking"></a>A. Configurar el seguimiento de cambios manual  
 En el ejemplo siguiente se establece el seguimiento de cambios manual en el índice de texto completo en la tabla `JobCandidate`.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate  
   SET CHANGE_TRACKING MANUAL;  
GO  
```  
  
### <a name="b-associating-a-property-list-with-a-full-text-index"></a>B. Asociar una lista de propiedades con un índice de texto completo  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En el ejemplo siguiente se asocia el `DocumentPropertyList` lista de propiedades con el índice de texto completo en el `Production.Document` tabla. Esta instrucción ALTER FULLTEXT INDEX inicia un rellenado completo, que es el comportamiento predeterminado de la cláusula SET SEARCH PROPERTY LIST.  
  
> [!NOTE]  
>  Para obtener un ejemplo que crea el `DocumentPropertyList` lista de propiedades, vea [CREATE SEARCH PROPERTY LIST &#40; Transact-SQL &#41; ](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList;   
GO  
```  
  
### <a name="c-removing-a-search-property-list"></a>C. Quitar una lista de propiedades de búsqueda  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En el siguiente ejemplo, se quita la lista de propiedades `DocumentPropertyList` del índice de texto completo en la tabla `Production.Document`. En este ejemplo, no hay prisa para quitar las propiedades del índice, de modo que se especifica la opción WITH NO POPULATION. Sin embargo, la búsqueda en el nivel de propiedades ya no se permite mediante este índice de texto completo.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
GO  
```  
  
### <a name="d-starting-a-full-population"></a>D. Iniciar un rellenado completo  
 En el ejemplo siguiente se inicia un rellenado completo en el índice de texto completo en el `JobCandidate` tabla.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   START FULL POPULATION;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.fulltext_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [Rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
