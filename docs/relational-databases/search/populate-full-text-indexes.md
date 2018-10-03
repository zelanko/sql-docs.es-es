---
title: Relleno de índices de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c80abd458a0275aeed00c2e97f29d07b0ce17f07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715033"
---
# <a name="populate-full-text-indexes"></a>Rellenar índices de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La creación y el mantenimiento de un índice de texto completo implica el rellenado del índice mediante un proceso denominado *rellenado* (también se denomina *rastreo*).  
  
##  <a name="types"></a> Types of population  
Un índice de texto completo admite los siguientes tipos de rellenado:
-   Rellenado **completo**
-   Rellenado automático o manual basado en el **seguimiento de cambios**
-   Rellenado incremental basado en una **marca de tiempo**
  
## <a name="full-population"></a>Rellenado completo  
 Durante un rellenado completo, se crean entradas de índice para todas las filas de una tabla o vista indizada. Un rellenado completo de un índice de texto completo genera entradas de índice para todas las filas de la tabla base o vista indizada.  
  
De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena totalmente un nuevo índice de texto completo en cuanto se crea.
-   Por otro lado, un rellenado completo puede consumir una cantidad significativa de recursos. Por consiguiente, al crear un índice de texto completo durante los períodos de máxima actividad, suele ser aconsejable retrasar el rellenado completo hasta un momento de menor uso, particularmente si la tabla base de un índice de texto completo es grande.
-   Además, el catálogo de texto completo al que pertenece el índice no se puede usar hasta que se rellenan todos sus índices de texto completo.

Para crear un índice de texto completo sin rellenarlo inmediatamente, especifique la cláusula `CHANGE_TRACKING OFF, NO POPULATION` en la instrucción `CREATE FULLTEXT INDEX`. Si especifica `CHANGE_TRACKING MANUAL`, el motor de texto completo no rellena el nuevo índice de texto completo hasta que se ejecute una instrucción `ALTER FULLTEXT INDEX` mediante la cláusula `START FULL POPULATION` o `START INCREMENTAL POPULATION`. 

### <a name="example---create-a-full-text-index-without-running-a-full-population"></a>Ejemplo: Creación de un índice de texto completo sin ejecutar un rellenado completo  
 En el ejemplo siguiente se crea un índice de texto completo en la tabla `Production.Document` de la base de datos de ejemplo `AdventureWorks` . Este ejemplo utiliza `WITH CHANGE_TRACKING OFF, NO POPULATION` para retrasar el rellenado completo inicial.  
  
```sql
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="example---run-a-full-population-on-a-table"></a>Ejemplo: Ejecución de un rellenado completo en una tabla  
 En el ejemplo siguiente se ejecuta un rellenado completo en la tabla `Production.Document` de la base de datos de ejemplo `AdventureWorks` .  
  
```sql
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
   
## <a name="population-based-on-change-tracking"></a>Rellenado basado en el seguimiento de cambios
 Si se desea, se puede usar el seguimiento de cambios para mantener un índice de texto completo después de su rellenado completo inicial. El seguimiento de cambios provoca una pequeña sobrecarga de trabajo porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene una tabla en la que realiza el seguimiento de los cambios de la tabla base desde el último rellenado. Cuando se utiliza el seguimiento de cambios, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene un registro de las filas de la tabla base o la vista indexada que se han modificado con las actualizaciones, eliminaciones o inserciones. Los cambios realizados en los datos con WRITETEXT y UPDATETEXT no se reflejan en el índice de texto completo y no se recopilan con el seguimiento de cambios.  
  
> [!NOTE]  
>  Para las tablas que contienen una columna **timestamp**, puede usar el rellenado incremental en lugar del de seguimiento de cambios.  
  
 Cuando el seguimiento de cambios está habilitado durante la creación de índices, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena totalmente el nuevo índice de texto completo justo después de crearse. Después de esto, los cambios se siguen y propagan al índice de texto completo.

### <a name="enable-change-tracking"></a>Enable change tracking
Hay dos tipos de seguimiento de cambios:
-   Automático (opción `CHANGE_TRACKING AUTO`). El seguimiento de cambios automático es el comportamiento predeterminado.
-   Manual (opción `CHANGE_TRACKING MANUAL`).   
  
 El tipo de seguimiento de cambios determina cómo se rellena el índice de texto completo, de la forma siguiente:  
  
-   **Rellenado automático**  
  
     De forma predeterminada, o si especifica `CHANGE_TRACKING AUTO`, el motor de búsqueda de texto completo utiliza el rellenado automático en el índice de texto completo. Una vez completado el rellenado total inicial, se realiza el seguimiento de los cambios cuando los datos se modifican en la tabla base y los cambios sometidos a seguimiento se propagan de forma automática. Sin embargo, el índice de texto completo se actualiza en segundo plano, de modo que los cambios propagados podrían no reflejarse inmediatamente en el índice.  
  
     **Para iniciar el seguimiento de los cambios con rellenado automático**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING AUTO  
  
    **Ejemplo: Modificación de un índice de texto completo para utilizar el seguimiento de cambios automático**  
    En el ejemplo siguiente se cambia el índice de texto completo de la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks` para usar el seguimiento de cambios con rellenado automático.  
  
    ```sql  
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
    GO   
    ```  
  
-   **Rellenado manual**  
  
     Si especifica CHANGE_TRACKING MANUAL, el motor de búsqueda de texto completo utiliza el rellenado manual en el índice de texto completo. Una vez completado el rellenado total inicial, se realiza el seguimiento de los cambios a medida que los datos se modifiquen en la tabla base. Sin embargo, no se propagan al índice de texto completo hasta que se ejecuta una instrucción ALTER FULLTEXT INDEX… START UPDATE POPULATION . Puede utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para llamar a esta instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma periódica.  
  
     **Para iniciar el seguimiento de cambios con rellenado manual**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING MANUAL  
  
    **Ejemplo: Creación de un índice de texto completo con seguimiento de cambios manual**  
    En el ejemplo siguiente se crea un índice de texto completo que utilizará el seguimiento de cambios con rellenado manual en la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks` .  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
    CREATE FULLTEXT CATALOG ft AS DEFAULT;  
    CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
       KEY INDEX ui_ukJobCand   
       WITH CHANGE_TRACKING=MANUAL;  
    GO  
    ```  
  
    **Ejemplo: Ejecución de un rellenado manual**  
    En el ejemplo siguiente se ejecuta un rellenado manual en el índice de texto completo sometido a seguimiento de la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks` .  
  
    ```sql 
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
    GO  
    ```
   
### <a name="disable-change-tracking"></a>Deshabilitación del seguimiento de cambios 
  
-   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING OFF  
   
  
## <a name="incremental-population-based-on-a-timestamp"></a>Rellenado incremental basado en una marca de tiempo  
 Un rellenado incremental es un mecanismo alternativo para rellenar un índice de texto completo manualmente. Si una tabla experimenta un volumen alto de inserciones, el rellenado incremental puede ser más eficaz que el rellenado manual.
 
 Puede ejecutar un llenado incremental de un índice de texto completo que tenga CHANGE_TRACKING configurado en MANUAL o en OFF. 
  
 Para realizar un llenado incremental, es necesario que la tabla indizada tenga una columna del tipo de datos **timestamp** . Si no existe una columna de tipo **timestamp** , no puede llevarse a cabo un llenado incremental.   

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la columna **timestamp** para identificar las filas que han cambiado desde el último rellenado. El rellenado incremental actualiza entonces el índice de texto completo de las filas que se hayan agregado, eliminado o modificado desde el último rellenado o en el curso del último rellenado. Al final de un proceso de rellenado, el motor de texto completo registra un nuevo valor de tipo **timestamp** . Este valor es el valor de **timestamp** mayor que el recopilador de SQL ha encontrado. Se usará cuando se inicie un rellenado incremental posterior.  
 
En algunos casos, la solicitud de un rellenado incremental produce un llenado completo.
-   Si se solicita un rellenado incremental en una tabla sin una columna de tipo **timestamp** , se llevará a cabo un rellenado completo.
-   Si el primer llenado de un índice de texto completo es un llenado incremental, indiza todas las filas, lo que lo hace equivalente a un llenado completo. 
-   Si alguno de los metadatos que afectan al índice de texto completo de la tabla ha cambiado desde el último rellenado, las solicitudes de rellenado incremental se implementan como rellenados completos. Esto incluye los cambios en los metadatos ocasionados al alterar la definición de una columna, índice o índice de texto completo. 

### <a name="run-an-incremental-population"></a>Ejecución de un rellenado incremental
  
 Para ejecutar un rellenado incremental, ejecute una instrucción `ALTER FULLTEXT INDEX` mediante la cláusula `START INCREMENTAL POPULATION`.  
  
###  <a name="create"></a> Creación o modificación de una programación para el rellenado incremental   
  
1.  En el Explorador de objetos de Management Studio, expanda el servidor.  
  
2.  Expanda **Bases de datos**y, después, la base de datos que contiene el índice de texto completo.  
  
3.  Expanda **Tablas**.  
  
    Haga clic con el botón derecho en la tabla en la que esté definido el índice de texto completo, seleccione **Índice de texto completo**y, en el menú contextual **Índice de texto completo** , haga clic en **Propiedades**. De esta forma se abre el cuadro de diálogo **Propiedades del índice de texto completo** .  

    > [!IMPORTANT]  
    >  Si la tabla base o la vista no contienen ninguna columna del tipo de datos **timestamp**, no se puede realizar un rellenado incremental.
      
1.  En el panel **Seleccionar una página**, seleccione **Programaciones**.  
  
     Utilice esta página para crear o administrar las programaciones para un trabajo del Agente SQL Server que inicia un rellenado de tabla incremental en la tabla base o vista indizada del índice de texto completo.  

     Las opciones son las siguientes:  
  
    -   Para **crear** una nueva programación, haga clic en **Nuevo**.  
  
        De esta forma se abre el cuadro de diálogo **Nueva programación de tabla de indexación de texto completo** , donde puede crear una programación. Para guardar la programación, haga clic en **Aceptar**.  
  
        > [!IMPORTANT]  
        >  Un trabajo del Agente SQL Server (Iniciar rellenado de tabla incremental en *nombre_base_de_datos*.*nombre_tabla*) se asocia a una nueva programación después de salir del cuadro de diálogo **Propiedades del índice de texto completo** . Si crea varias programaciones para el mismo índice de texto completo, todas utilizan el mismo trabajo.  
  
    -   Para **cambiar** una programación existente, seleccione la programación existente y haga clic en **Editar**.  
  
         De esta forma se abre el cuadro de diálogo **Nueva programación de tabla de indexación de texto completo** , donde puede modificar una programación.  
  
        > [!NOTE]  
        >  Para obtener información sobre cómo modificar un trabajo del Agente SQL Server, vea [Modificar un trabajo](../../ssms/agent/modify-a-job.md).  
  
    -   Para **eliminar** una programación existente, seleccione la programación existente y haga clic en **Eliminar**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]   
  
##  <a name="crawl"></a> Solución de errores en un rellenado de texto completo (rastreo)  
Cuando se produce un error durante un rastreo, la función de registro de rastreo de la búsqueda de texto completo crea y mantiene un registro de rastreo, que es un archivo sin formato. Cada registro de rastreo se corresponde con un determinado catálogo de texto completo. De forma predeterminada, los registros de rastreo de una instancia determinada (en este ejemplo, la instancia predeterminada) se encuentran en la carpeta `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG`.
 
El archivo de registro de rastreo sigue el siguiente esquema de nomenclatura:  
  
`SQLFT<DatabaseID><FullTextCatalogID>.LOG[<n>]`
  
Las partes variables del nombre de archivo de registro de rastreo son las siguientes.
-   <**DatabaseID**> - El identificador de una base de datos. <**dbid**> es un número de cinco dígitos con ceros a la izquierda.  
-   <**FullTextCatalogID**> - Identificador de catálogo de texto completo. <**catid**> es un número de cinco dígitos con ceros a la izquierda.  
-   <**n**> - Es un entero que indica la existencia de uno o varios registros de rastreo del mismo catálogo de texto completo.  
  
 Por ejemplo, `SQLFT0000500008.2` es el archivo de registro de rastreo para un identificador de base de datos = 5 y un identificador de catálogo de texto completo = 8. El 2 al final del nombre de archivo indica que existen dos archivos de registro de rastreo para esta pareja de base de datos y catálogo.  

## <a name="see-also"></a>Ver también  
 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)   
 [Introducción a la búsqueda de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
