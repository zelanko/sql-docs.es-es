---
title: Introducción a la búsqueda de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fd5ced641ee8fc17f0be7d7b6e19aff17dcb69bd
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011287"
---
# <a name="get-started-with-full-text-search"></a>Introducción a la búsqueda de texto completo
  Las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están habilitadas para texto completo de forma predeterminada. Sin embargo, para usar un índice de texto completo en una tabla, debe configurar la capacidad de indización de texto completo en las columnas de las tablas a las que desea obtener acceso mediante el motor de búsqueda de texto completo.  
  
##  <a name="configure"></a> Configuración de una base de datos para la búsqueda de texto completo  
 En cualquier escenario, un administrador de bases de datos realiza los siguientes pasos básicos para configurar columnas de tabla en una base de datos para la búsqueda de texto completo:  
  
1.  Crear un catálogo de texto completo  
  
2.  En cada tabla en la que se desea buscar, crear un índice de texto completo por:  
  
    1.  Identificar cada columna de texto que se desea incluir en el índice de texto completo.  
  
    2.  Si una columna determinada contiene documentos almacenados como datos binarios (`varbinary(max)`, o `image` datos), debe especificar una columna de tabla (la *columna de tipo*) que identifica el tipo de cada documento en la columna que se va a indizar.  
  
    3.  Especificar el idioma que se desea que utilice la búsqueda de texto completo en los documentos de la columna.  
  
    4.  Elegir el mecanismo del seguimiento de cambios que se desea utilizar en el índice de texto completo para el seguimiento de cambios en la tabla base y sus columnas.  
  
 La búsqueda de texto completo admite varios idiomas a través del uso de los *componentes lingüísticos* siguientes: separadores de palabras y lematizadores, listas de palabras irrelevantes y archivos de diccionarios de sinónimos. Los archivos de diccionario de sinónimos y, en algunos casos, las listas de palabras irrelevantes requieren su configuración por un administrador de la base de datos. Un archivo de diccionario de sinónimos determinado admite todos los índices de texto completo que usen el idioma correspondiente, y una lista de palabras irrelevantes determinada puede estar asociada a tantos índices de texto completo como se desee.  
  
##  <a name="setup"></a> Configurar un catálogo de texto completo y un índice  
 Esto implica la realización de los siguientes pasos básicos:  
  
1.  Crear un catálogo de texto completo para almacenar índices de texto completo.  
  
     Cada índice de texto completo debe pertenecer a un catálogo de texto completo. Puede crear un catálogo de texto independiente para cada índice de texto completo o puede asociar varios índices de texto completo a un catálogo determinado. Un catálogo de texto completo es un objeto virtual y no pertenece a ningún grupo de archivos. El catálogo completo es un concepto lógico que hace referencia a un grupo de índices de texto completo.  
  
2.  Crear un índice de texto completo en la tabla o en la vista indizada.  
  
     Un índice de texto completo es un tipo especial de índice funcional basado en token que crea y mantiene el motor de texto completo. Para crear una búsqueda de texto completo en una tabla o vista, debe haber un índice único de una sola columna que no acepte valores NULL. El motor de búsqueda de texto completo requiere este índice único para asignar cada fila de la tabla a una clave única que se pueda comprimir. Un índice de texto completo puede incluir las columnas `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, `varbinary` y `varbinary(max)` columnas. Para obtener más información, vea [Crear y administrar índices de texto completo](create-and-manage-full-text-indexes.md).  
  
 Antes de aprender a crear índices de texto completo, es importante tener en cuenta en qué se diferencian éstos de los índices normales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En la tabla siguiente, se indican las diferencias.  
  
|Índices de texto completo|Índices normales de SQL Server|  
|------------------------|--------------------------------|  
|Solo se permite un índice de texto completo por cada tabla.|Se permiten varios índices normales por cada tabla.|  
|La adición de datos a los índices de texto completo, operación que recibe el nombre de *rellenado*, puede solicitarse mediante una programación o una solicitud específica, o bien realizarse automáticamente al agregar nuevos datos.|Se actualizan automáticamente cuando se insertan, actualizan o eliminan los datos en los que están basados.|  
|Se agrupan en la misma base de datos en uno o más catálogos de texto completo.|No se agrupan.|  
  
  
##  <a name="options"></a> Elección de las opciones para un índice de texto completo  
 En esta sección, se trata lo siguiente:  
  
-   Elegir el idioma de la columna  
  
-   Elegir un grupo de archivos para un índice de texto completo  
  
-   Asignar el índice de texto completo a un catálogo de texto completo  
  
-   Asociar una lista de palabras irrelevantes con el índice de texto completo  
  
-   Actualizar un índice de texto completo  
  
### <a name="choosing-the-column-language"></a>Elegir el idioma de la columna  
 Para obtener información sobre lo que hay que tener en cuenta para elegir el idioma de columna, vea [Elegir un idioma al crear un índice de texto completo](choose-a-language-when-creating-a-full-text-index.md).  
  
### <a name="choosing-a-filegroup-for-a-full-text-index"></a>Elegir un grupo de archivos para un índice de texto completo  
 El proceso de generar un índice de texto completo requiere un uso bastante intensivo de E/S (en un nivel superior, consiste en leer datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, a continuación, propagar los datos filtrados al índice de texto completo). Como práctica recomendada, busque en el grupo de archivos de bases de datos el índice de texto completo que mejor maximice el rendimiento de E/S o busque los índices de texto completo en un grupo de archivos diferente de otro volumen.  
  
 Si considera importante que la tarea de administración resulte sencilla, le recomendamos que almacene los datos de tabla y todos los catálogos de texto completo asociados en el mismo grupo de archivos. A veces, por razones de rendimiento, es posible que le interese tener los datos de tabla y el índice de texto completo en grupos de archivos diferentes almacenados en volúmenes diferentes para maximizar el paralelismo de E/S.  
  
  
### <a name="assigning-the-full-text-index-to-a-full-text-catalog"></a>Asignar el índice de texto completo a un catálogo de texto completo  
 Es importante planear la colocación de los índices de texto completo para las tablas en los catálogos de texto completo.  
  
 Recomendamos asociar las tablas que tienen las mismas características de actualización (como un número reducido de cambios frente a un número elevado de cambios, o tablas que suelen cambiar durante un período determinado del día) bajo el mismo catálogo de texto completo. Al configurar la programación del rellenado de catálogos de texto completo, los índices de texto completo permanecen sincronizados con las tablas sin que ello afecte negativamente al uso de los recursos del servidor de bases de datos en momentos en los que la actividad de la base de datos es más intensa.  
  
 Cuando asigne una tabla a un catálogo de texto completo, tenga en cuenta las indicaciones siguientes:  
  
-   Seleccione siempre el índice exclusivo más pequeño disponible para la clave exclusiva de texto completo. (Un índice de tipo entero de cuatro bytes es el más apropiado.) Esto reduce significativamente los recursos necesarios para el servicio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search en el sistema de archivos. Si la clave principal es grande (más de 100 bytes), considere la posibilidad de elegir otro índice exclusivo en la tabla (o de crear otro índice exclusivo) como clave exclusiva de texto completo. Si, por el contrario, el tamaño de la clave exclusiva de texto completo supera el tamaño máximo permitido (900 bytes), no se podrá realizar un rellenado de texto.  
  
-   Si indiza una tabla con millones de filas, asigne la tabla a su propio catálogo de texto completo.  
  
-   Tenga en cuenta la cantidad de cambios que se producen en las tablas con índices de texto completo, así como el número total de filas. Si el número total de filas que van a cambiar, junto con el número de filas existentes en la tabla durante el último rellenado de texto, asciende a varios millones, asigne a la tabla su propio catálogo de texto completo.  
  
  
### <a name="associating-a-stoplist-with-the-full-text-index"></a>Asociar una lista de palabras irrelevantes con el índice de texto completo  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] dispone de listas de palabras irrelevantes. Una *lista de palabras irrelevantes* es una lista de palabras sin importancia. Cada índice de texto completo tiene asociada una lista de palabras irrelevantes, y las palabras de dicha lista se aplican a las consultas de texto completo que se realizan en ese índice. De forma predeterminada, a cada índice de texto completo nuevo se asocia la lista de palabras irrelevantes del sistema. Sin embargo, puede crear y usar su propia lista de palabras irrelevantes. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 Por ejemplo, la siguiente instrucción [CREATE FULLTEXT STOPLIST](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql) de [!INCLUDE[tsql](../../../includes/tsql-md.md)] crea una nueva lista de palabras irrelevantes de texto completo denominada myStoplist3; para ello, copia la lista de palabras irrelevantes del sistema:  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 La siguiente instrucción [ALTER FULLTEXT STOPLIST](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] modifica una lista de palabras irrelevantes denominada myStoplist; para ello, agrega la palabra "en", primero para el idioma español y, a continuación, para el francés:  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
  
  
### <a name="updating-a-full-text-index"></a>Actualizar un índice de texto completo  
 Al igual que los índices normales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los índices de texto completo se pueden actualizar automáticamente cuando se modifican los datos de las tablas asociadas. Éste es el comportamiento predeterminado. Como alternativa, puede mantener actualizados los índices de texto completo de forma manual o durante los intervalos programados especificados. Rellenar un índice de texto completo puede consumir mucho tiempo y muchos recursos, por lo que, normalmente, la actualización del índice se realiza como un proceso asincrónico que se ejecuta en segundo plano para mantenerlo al día después de haber llevado a cabo modificaciones en la tabla base. Actualizar un índice de texto completo inmediatamente después de cada cambio realizado en la tabla base puede consumir muchos recursos. Por tanto, si el porcentaje de actualizaciones, inserciones y eliminaciones es muy elevado, es posible que experimente una disminución en el rendimiento de las consultas. Si se da esta situación, plantéese la posibilidad de programar las actualizaciones provocadas por el seguimiento de cambios manual; es decir, en lugar de disputarse los recursos con las consultas, lleve a cabo una actualización de vez en cuando.  
  
 Para supervisar el estado del rellenado, use las funciones FULLTEXTCATALOGPROPERTY u OBJECTPROPERTYEX. Para obtener el estado del rellenado del catálogo, ejecute la instrucción siguiente:  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 Normalmente, si se está realizando un rellenado completo, el resultado devuelto es 1.  
  
  
##  <a name="example"></a> Ejemplo: Configurar la búsqueda de texto completo  
 En el siguiente ejemplo, compuesto por dos partes, se crea un catálogo de texto completo denominado `AdvWksDocFTCat` en la base de datos AdventureWorks y, a continuación, se crea un índice de texto completo en la tabla `Document` de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Esta instrucción creará el catálogo de texto completo en el directorio predeterminado especificado durante la configuración. La carpeta denominada `AdvWksDocFTCat` se encuentra en el directorio predeterminado.  
  
1.  Para crear un catálogo de texto completo denominado `AdvWksDocFTCat`, en el ejemplo se usa una instrucción [CREATE FULLTEXT CATALOG](/sql/t-sql/statements/create-fulltext-catalog-transact-sql):  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  Para crear un índice de texto completo en la tabla Document, antes debe asegurarse de que dicha tabla tiene un índice único, de una sola columna y que no admite valores NULL. La siguiente instrucción [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) crea un índice único, `ui_ukDoc`, en la columna DocumentID de la tabla Document:  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  Después de tener una clave única, puede crear un índice de texto completo en la tabla `Document` mediante la siguiente instrucción [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) .  
  
    ```  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     El elemento TYPE COLUMN definido en este ejemplo especifica la columna de tipo de la tabla que contiene el tipo del documento en cada fila de la columna "Document" (que es del tipo binario). La columna de tipo almacena el archivo proporcionado por el usuario extensión-".doc", ".xls" y así sucesivamente del documento en una fila determinada. El motor de búsqueda de texto completo utiliza la extensión de archivo almacenada en una fila determinada para invocar el filtro adecuado para analizar los datos de esa fila. Después de que el filtro haya analizado los datos binarios de la fila, el separador de palabras especificado analizará el contenido (en este ejemplo, se usa el separador de palabras para inglés del Reino Unido). Tenga en cuenta que el proceso de filtrado solo tiene lugar durante la indización o cuando un usuario inserta o actualiza una columna de la tabla base mientras está habilitado el seguimiento de cambios automático para el índice de texto completo asociado. Para obtener más información, vea [Configurar y administrar filtros para búsquedas](configure-and-manage-filters-for-search.md).  
  
  
##  <a name="tasks"></a> Tareas comunes  
  
### <a name="to-create-a-full-text-catalog"></a>Para crear un catálogo de texto completo  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [Crear y administrar catálogos de texto completo](create-and-manage-full-text-catalogs.md)  
  
### <a name="to-view-the-indexes-of-a-table-or-view"></a>Para ver los índices de una tabla (o vista)  
  
-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
### <a name="to-create-a-unique-index"></a>Para crear un índice único  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [Abrir el Diseñador de tablas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)  
  
### <a name="to-create-a-full-text-index"></a>Para crear un índice de texto completo  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [Crear y administrar índices de texto completo](create-and-manage-full-text-indexes.md)  
  
### <a name="to-view-information-about-a-full-text-index"></a>Para ver información acerca de un índice de texto completo  
  
|Catálogo o vista de administración dinámica|Descripción|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)|Devuelve una fila por cada referencia de catálogo de texto completo a índice de texto completo.|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|Contiene una fila para cada columna que forma parte de un índice de texto completo.|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)|Un índice de texto completo utiliza tablas internas denominadas fragmentos de índice de texto completo para almacenar los datos de índice invertidos. Esta vista se puede utilizar para consultar los metadatos sobre estos fragmentos. Esta vista contiene una fila para cada fragmento de índice de texto completo en cada tabla que contiene un índice de texto completo.|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)|Contiene una fila por índice de texto completo de un objeto tabular.|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)|Devuelve información sobre el contenido de un índice de texto completo para la tabla especificada.|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)|Devuelve información sobre el contenido de nivel de documento de un índice de texto completo para la tabla especificada. Una palabra clave determinada puede aparecer en varios documentos.|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|Devuelve información acerca de los rellenados de índices de texto completo actualmente en progreso.|  
  
  
## <a name="see-also"></a>Vea también  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [Rellenar índices de texto completo](populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)  
  
  
