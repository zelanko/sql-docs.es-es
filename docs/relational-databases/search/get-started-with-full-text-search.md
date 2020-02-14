---
title: Introducción a la búsqueda de texto completo | Microsoft Docs
ms.date: 08/22/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 349e00b7734ed8e8176585c55018b7565649cc1f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "72903828"
---
# <a name="get-started-with-full-text-search"></a>Introducción a la búsqueda de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Las bases de datos de SQL Server están habilitadas para texto completo de manera predeterminada. Pero para poder ejecutar consultas de texto completo debe crear primero un catálogo de texto completo y un índice de texto completo en las vistas indexadas o tablas en las que quiere realizar una búsqueda.

## <a name="set-up-full-text-search-in-two-steps"></a>Configurar una búsqueda de texto completo en dos pasos
Existen dos pasos básicos para configurar una búsqueda de texto completo:  
1.  Crear un catálogo de texto completo  
2.  Cree un índice de texto completo en las tablas o en la vista indizada en la que desea realizar una búsqueda. 

Cada índice de texto completo debe pertenecer a un catálogo de texto completo. Puede crear un catálogo de texto independiente para cada índice de texto completo o puede asociar varios índices de texto completo a un catálogo determinado. Un catálogo de texto completo es un objeto virtual y no pertenece a ningún grupo de archivos. El catálogo completo es un concepto lógico que hace referencia a un grupo de índices de texto completo.

> [!NOTE]
> En estos pasos se presupone que se han instalado los componentes opcionales de búsqueda de texto completo al instalar SQL Server. Si no es así, tiene que ejecutar de nuevo el programa de instalación de SQL Server para agregarlos.  

## <a name="set-up-full-text-search-with-a-wizard"></a>Configurar una búsqueda de texto completo con un asistente 
 
Para configurar una búsqueda de texto completo con un asistente, vea [Usar el Asistente para indización de texto completo](../../relational-databases/search/use-the-full-text-indexing-wizard.md).

## <a name="set-up-full-text-search-with-transact-sql"></a>Configurar una búsqueda de texto completo con Transact-SQL 
 En el siguiente ejemplo, compuesto por dos partes, se crea un catálogo de texto completo denominado `AdvWksDocFTCat` en la base de datos de ejemplo AdventureWorks y luego se crea un índice de texto completo en la tabla `Document` de la base de datos de ejemplo. Esta instrucción creará el catálogo de texto completo en el directorio predeterminado especificado durante la instalación de SQL Server. La carpeta denominada `AdvWksDocFTCat` se encuentra en el directorio predeterminado.  
  
1.  Para crear un catálogo de texto completo denominado `AdvWksDocFTCat`, en el ejemplo se usa una instrucción [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) :  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
    Para obtener más información, vea [Create and Manage Full-Text Catalogs](../../relational-databases/search/create-and-manage-full-text-catalogs.md) (Crear y administrar catálogos de texto completo).
 
2.  Para crear un índice de texto completo en la tabla Document, antes debe asegurarse de que dicha tabla tiene un índice único, de una sola columna y que no admite valores NULL. La siguiente instrucción [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) crea un índice único, `ui_ukDoc`, en la columna DocumentID de la tabla Document:  
  
    ```sql 
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  

3.  Después de tener una clave única, puede crear un índice de texto completo en la tabla `Document` mediante la siguiente instrucción [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) .  
  
    ```sql  
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
  
     El elemento TYPE COLUMN definido en este ejemplo especifica la columna de tipo de la tabla que contiene el tipo del documento en cada fila de la columna "Document" (que es del tipo binario). La columna de tipo almacena la extensión de archivo proporcionada por el usuario (".doc", ".xls", etc.) del documento en una fila determinada. El motor de búsqueda de texto completo utiliza la extensión de archivo almacenada en una fila determinada para invocar el filtro adecuado para analizar los datos de esa fila. Cuando el filtro haya analizado los datos binarios de la fila, el separador de palabras especificado analiza el contenido. (En este ejemplo, se usa el separador de palabras para inglés del Reino Unido). Para obtener más información, vea [Configurar y administrar filtros para búsquedas](../../relational-databases/search/configure-and-manage-filters-for-search.md).  

    Para obtener más información, vea [Create and Manage Full-Text Indexes](../../relational-databases/search/create-and-manage-full-text-indexes.md) (Crear y administrar índices de texto completo).

##  <a name="options"></a> Elegir opciones para un índice de texto completo 
  
### <a name="choose-a-language"></a>Elegir un idioma  
 Para información sobre cómo elegir el idioma de la columna, consulte [Elegir un idioma al crear un índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
### <a name="choose-a-filegroup"></a>Elegir un grupo de archivos  
 El proceso de creación de un índice de texto completo realiza un uso bastante intensivo de E/S. En resumen, consiste en leer datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y luego propagar los datos filtrados a todo el índice de texto completo. Como práctica recomendada, busque en el grupo de archivos de bases de datos el índice de texto completo que mejor maximice el rendimiento de E/S o busque los índices de texto completo en un grupo de archivos diferente de otro volumen.
  
### <a name="choose-a-full-text-catalog"></a>Elegir un catálogo de texto completo   
 
 Recomendamos asociar las tablas que tienen las mismas características de actualización (como un número reducido de cambios frente a un número elevado de cambios, o tablas que suelen cambiar durante un período determinado del día) bajo el mismo catálogo de texto completo. Al configurar la programación del rellenado de catálogos de texto completo, los índices de texto completo permanecen sincronizados con las tablas sin que ello afecte negativamente al uso de los recursos del servidor de bases de datos en momentos en los que la actividad de la base de datos es más intensa.  
  
 Tenga en cuenta las directrices siguientes:  
  
-   Si indiza una tabla con millones de filas, asigne la tabla a su propio catálogo de texto completo.  
  
-   Tenga en cuenta la cantidad de cambios que se producen en las tablas con índices de texto completo, así como el número total de filas. Si el número total de filas que van a cambiar, junto con el número de filas existentes en la tabla durante el último rellenado de texto, asciende a varios millones, asigne a la tabla su propio catálogo de texto completo.  

### <a name="associate-a-unique-index"></a>Asociar un índice único
Seleccione siempre el índice exclusivo más pequeño disponible para la clave exclusiva de texto completo. (Un índice de tipo entero de cuatro bytes es el más apropiado.) Esto reduce considerablemente los recursos necesarios para el servicio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search en el sistema de archivos. Si la clave principal es grande (más de 100 bytes), considere la posibilidad de elegir otro índice exclusivo en la tabla (o de crear otro índice exclusivo) como clave exclusiva de texto completo. Si, por el contrario, el tamaño de la clave exclusiva de texto completo supera el tamaño máximo permitido (900 bytes), no se podrá realizar un rellenado de texto.  
 
### <a name="associate-a-stoplist"></a>Asociar una lista de palabras irrelevantes   
  Una *lista de palabras irrelevantes* es una lista de palabras sin importancia. Cada índice de texto completo tiene asociada una lista de palabras irrelevantes, y las palabras de dicha lista se aplican a las consultas de texto completo que se realizan en ese índice. De forma predeterminada, a cada índice de texto completo nuevo se asocia la lista de palabras irrelevantes del sistema. También puede crear y usar su propia lista de palabras irrelevantes.   
  
 Por ejemplo, la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) crea una lista de palabras irrelevantes de texto completo denominada myStoplist al copiar la lista de palabras irrelevantes del sistema:  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) modifica una lista de palabras irrelevantes denominada myStoplist; para ello, agrega la palabra "en", primero para el idioma español y luego para el francés:  
  
```sql  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).

## <a name="update-a-full-text-index"></a>Actualizar un índice de texto completo  
 Al igual que los índices normales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los índices de texto completo se pueden actualizar automáticamente cuando se modifican los datos de las tablas asociadas. Este es el comportamiento predeterminado. Como alternativa, puede mantener actualizados los índices de texto completo de forma manual o durante los intervalos programados especificados. Rellenar un índice de texto completo puede consumir mucho tiempo y muchos recursos. Por consiguiente, la actualización del índice se suele realizar como un proceso asincrónico que se ejecuta en segundo plano para mantenerlo al día después de haber llevado a cabo modificaciones en la tabla base. 
 
Actualizar un índice de texto completo inmediatamente después de cada cambio realizado en la tabla también consume muchos recursos. Por tanto, si el porcentaje de actualizaciones, inserciones y eliminaciones es muy elevado, es posible que experimente una disminución en el rendimiento de las consultas. Si se da esta situación, plantéese la posibilidad de programar las actualizaciones provocadas por el seguimiento de cambios manual; es decir, en lugar de disputarse los recursos con las consultas, lleve a cabo una actualización de vez en cuando.  
  
Para obtener más información, vea [Populate Full-Text Indexes](../../relational-databases/search/populate-full-text-indexes.md) (Rellenar índices de texto completo). 

## <a name="next-steps"></a>Pasos siguientes
Después de configurar la búsqueda de texto completo de SQL Server, está listo para ejecutar consultas de texto completo. Para obtener más información, vea [Query with Full-Text Search](../../relational-databases/search/query-with-full-text-search.md) (Consultar con búsqueda de texto completo).
