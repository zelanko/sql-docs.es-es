---
title: Relleno de índices de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d6f871fabba547268736dca990215b89ae84e9eb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011177"
---
# <a name="populate-full-text-indexes"></a>Rellenar índices de texto completo
  La creación y el mantenimiento de un índice de texto completo implica el rellenado del índice mediante un proceso denominado *rellenado* (también se denomina *rastreo*).  
  
##  <a name="types-of-population"></a><a name="types"></a>Tipos de rellenado  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]admite los siguientes tipos de rellenado: rellenado completo, rellenado automático o manual basado en el seguimiento de cambios y rellenado incremental basado en la marca de tiempo.  
  
### <a name="full-population"></a>Rellenado completo  
 Durante un rellenado completo, se crean entradas de índice para todas las filas de una tabla o vista indizada. Un rellenado completo de un índice de texto completo genera entradas de índice para todas las filas de la tabla base o vista indizada.  
  
 De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena totalmente un nuevo índice de texto completo en cuanto se crea. Sin embargo, un rellenado completo puede consumir una cantidad significativa de recursos. Por consiguiente, al crear un índice de texto completo durante los períodos de máxima actividad, suele ser aconsejable retrasar el rellenado completo hasta un momento de menor uso, particularmente si la tabla base de un índice de texto completo es grande. Sin embargo, el catálogo de texto completo al que pertenece el índice no se puede usar hasta que se rellenan todos sus índices de texto completo. Para crear un índice de texto completo sin rellenarlo inmediatamente, especifique la cláusula CHANGE_TRACKING OFF, NO POPULATION en la instrucción CREATE FULLTEXT INDEX. Si especifica CHANGE_TRACKING MANUAL, el motor de búsqueda de texto completo usa la instrucción. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no rellenará el nuevo índice de texto completo hasta que se ejecute una instrucción ALTER FULLTEXT INDEX mediante la cláusula START FULL POPULATION o START INCREMENTAl POPULATION. Para obtener más información, vea los ejemplos "A. Crear un índice de texto completo sin ejecutar un rellenado completo" y "B. Ejecutar un rellenado completo en la tabla", posteriormente en este tema.  
  

  
### <a name="change-tracking-based-population"></a>Rellenado basado en el seguimiento de cambios  
 Si se desea, se puede usar el seguimiento de cambios para mantener un índice de texto completo después de su rellenado completo inicial. El seguimiento de cambios provoca una pequeña sobrecarga de trabajo porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene una tabla en la que realiza el seguimiento de los cambios de la tabla base desde el último rellenado. Cuando se utiliza el seguimiento de cambios, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene un registro de las filas de la tabla base o la vista indizada que se han modificado con las actualizaciones, eliminaciones o inserciones. Los cambios realizados en los datos con WRITETEXT y UPDATETEXT no se reflejan en el índice de texto completo y no se recopilan con el seguimiento de cambios.  
  
> [!NOTE]  
>  Para las tablas que contienen una columna `timestamp`, puede utilizar los rellenados incrementales.  
  
 Cuando el seguimiento de cambios está habilitado durante la creación de índices, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena totalmente el nuevo índice de texto completo justo después de crearse. Después de esto, los cambios se siguen y propagan al índice de texto completo. Hay dos tipos de seguimiento de cambios: automático (opción CHANGE_TRACKING AUTO) y manual (opción CHANGE_TRACKING MANUAL). El seguimiento de cambios automático es el comportamiento predeterminado.  
  
 El tipo de seguimiento de cambios determina cómo se rellena el índice de texto completo, de la forma siguiente:  
  
-   Rellenado automático  
  
     De forma predeterminada, o si especifica CHANGE_TRACKING AUTO, el motor de búsqueda de texto completo utiliza el rellenado automático en el índice de texto completo. Una vez completado el rellenado total inicial, se realiza el seguimiento de los cambios cuando los datos se modifican en la tabla base y los cambios sometidos a seguimiento se propagan de forma automática. Sin embargo, el índice de texto completo se actualiza en segundo plano, de modo que los cambios propagados podrían no reflejarse inmediatamente en el índice.  
  
     **Para configurar el seguimiento de los cambios con rellenado automático**  
  
    -   [crear índice de texto completo](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... CON CHANGE_TRACKING AUTO  
  
    -   [ALTER fulltext index](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... ESTABLECER CHANGE_TRACKING AUTOMÁTICO  
  
     Para obtener más información, vea el ejemplo "E. Modificar un índice de texto completo para utilizar el seguimiento de cambios automático", posteriormente en este tema.  
  
-   Rellenado manual  
  
     Si especifica CHANGE_TRACKING MANUAL, el motor de búsqueda de texto completo utiliza el rellenado manual en el índice de texto completo. Una vez completado el rellenado total inicial, se realiza el seguimiento de los cambios a medida que los datos se modifiquen en la tabla base. Sin embargo, no se propagan al índice de texto completo hasta que se ejecuta una instrucción ALTER FULLTEXT INDEX... INICIAR la instrucción UPDATE POPULATION. Puede utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para llamar a esta instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma periódica.  
  
     **Para iniciar el seguimiento de cambios con rellenado manual**  
  
    -   [crear índice de texto completo](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... CON CHANGE_TRACKING MANUAL  
  
    -   [ALTER fulltext index](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... ESTABLECER CHANGE_TRACKING MANUAL  
  
     Para obtener más información, vea los ejemplos "C. Crear un índice de texto completo con seguimiento de cambios manual" y "D. Ejecutar un rellenado manual", posteriormente en este tema.  
  
 **Para desactivar el seguimiento de cambios**  
  
-   [crear índice de texto completo](/sql/t-sql/statements/create-fulltext-index-transact-sql) ... CON CHANGE_TRACKING DESACTIVADO  
  
-   [ALTER fulltext index](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ... ESTABLECER CHANGE_TRACKING DESACTIVADO  
  

  
### <a name="incremental-timestamp-based-population"></a>Rellenado basado en la marca de tiempo incremental  
 Un rellenado incremental es un mecanismo alternativo para rellenar un índice de texto completo manualmente. Puede ejecutar un llenado incremental de un índice de texto completo que tenga CHANGE_TRACKING configurado en MANUAL o en OFF. Si el primer llenado de un índice de texto completo es un llenado incremental, indiza todas las filas, lo que lo hace equivalente a un llenado completo.  
  
 Para realizar un llenado incremental, es necesario que la tabla indizada tenga una columna del tipo de datos `timestamp`. Si no existe una columna de tipo `timestamp`, no puede llevarse a cabo un llenado incremental. Si se solicita un rellenado incremental en una tabla sin una columna de tipo `timestamp`, se llevará a cabo un rellenado completo. Además, si alguno de los metadatos que afectan al índice de texto completo de la tabla ha cambiado desde el último rellenado, las solicitudes de rellenado incremental se implementan como rellenados completos. Esto incluye los cambios en los metadatos ocasionados al alterar la definición de una columna, índice o índice de texto completo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la columna `timestamp` para identificar las filas que han cambiado desde el último rellenado. El rellenado incremental actualiza entonces el índice de texto completo de las filas que se hayan agregado, eliminado o modificado desde el último rellenado o en el curso del último rellenado. Si una tabla experimenta un volumen alto de inserciones, el rellenado incremental puede ser más eficaz que el rellenado manual.  
  
 Al final de un proceso de rellenado, el motor de texto completo registra un nuevo valor de tipo `timestamp`. Este valor es el valor de `timestamp` mayor que el recopilador de SQL ha encontrado. Se usará cuando se inicie un rellenado incremental posterior.  
  
 Para ejecutar un rellenado incremental, ejecute una instrucción ALTER FULLTEXT INDEX con la cláusula START INCREMENTAL POPULATION.  
  

  
##  <a name="examples-of-populating-full-text-indexes"></a><a name="examples"></a>Ejemplos de rellenar índices de texto completo  
  
> [!NOTE]  
>  En los ejemplos de esta sección se usa la tabla `Production.Document` o `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks` .  
  
### <a name="a-creating-a-full-text-index-without-running-a-full-population"></a>A. Crear un índice de texto completo sin ejecutar un rellenado completo  
 En el ejemplo siguiente se crea un índice de texto completo en la tabla `Production.Document` de la base de datos de ejemplo `AdventureWorks` . En este ejemplo se usa WITH CHANGE_TRACKING OFF, NO POPULATION para retrasar el rellenado completo inicial.  
  
```  
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
  
### <a name="b-running-a-full-population-on-table"></a>B. Ejecutar un rellenado completo en la tabla  
 En el ejemplo siguiente se ejecuta un rellenado completo en la tabla `Production.Document` de la base de datos de ejemplo `AdventureWorks` .  
  
```  
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
  
### <a name="c-creating-a-full-text-index-with-manual-change-tracking"></a>C. Crear un índice de texto completo con seguimiento de cambios manual  
 En el ejemplo siguiente se crea un índice de texto completo que utilizará el seguimiento de cambios con rellenado manual en la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks` .  
  
```  
USE AdventureWorks;  
GO  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH CHANGE_TRACKING=MANUAL;  
GO  
```  
  
### <a name="d-running-a-manual-population"></a>D. Ejecutar un rellenado manual  
 En el ejemplo siguiente se ejecuta un rellenado manual en el índice de texto completo sometido a seguimiento de la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks` .  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
GO  
```  
  
### <a name="e-altering-a-full-text-index-to-use-automatic-change-tracking"></a>E. Modificar un índice de texto completo para usar el seguimiento de cambios automático  
 En el ejemplo siguiente se cambia el índice de texto completo de la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo `AdventureWorks` para usar el seguimiento de cambios con rellenado automático.  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
GO   
```  
  

  
##  <a name="creating-or-changing-a-schedule-for-incremental-population"></a><a name="create"></a>Crear o cambiar una programación para el rellenado incremental  
  
#### <a name="to-create-or-change-a-schedule-for-incremental-population-in-management-studio"></a>Para crear o modificar una programación para el rellenado incremental en Management Studio  
  
1.  En el Explorador de objetos, expanda el servidor.  
  
2.  Expanda **Bases de datos**y, después, la base de datos que contiene el índice de texto completo.  
  
3.  Expanda **Tablas**.  
  
 Haga clic con el botón derecho en la tabla en la que esté definido el índice de texto completo, seleccione **Índice de texto completo**y, en el menú contextual **Índice de texto completo** , haga clic en **Propiedades**. De esta forma se abre el cuadro de diálogo **Propiedades del índice de texto completo** .  
  
1.  En el panel **seleccionar una página** , seleccione programaciones.  
  
     Utilice esta página para crear o administrar las programaciones para un trabajo del Agente SQL Server que inicia un rellenado de tabla incremental en la tabla base o vista indizada del índice de texto completo.  
  
    > [!IMPORTANT]  
    >  Si la tabla base o la vista no contienen ninguna columna del tipo de datos `timestamp`, se realiza un rellenado completo.  
  
     Las opciones son las siguientes:  
  
    -   Para crear una nueva programación, haga clic en **Nuevo**.  
  
         De esta forma se abre el cuadro de diálogo **Nueva programación de tabla de indexación de texto completo** , donde puede crear una programación. Para guardar la programación, haga clic en **Aceptar**.  
  
        > [!IMPORTANT]  
        >  Un trabajo del Agente SQL Server (Iniciar rellenado de tabla incremental en *nombre_base_de_datos*.*nombre_tabla*) se asocia a una nueva programación después de salir del cuadro de diálogo **Propiedades del índice de texto completo** . Si crea varias programaciones para el índice de texto completo, todas utilizan el mismo trabajo.  
  
    -   Para cambiar una programación, selecciónela y haga clic en **Editar**.  
  
         De esta forma se abre el cuadro de diálogo **Nueva programación de tabla de indexación de texto completo** , donde puede modificar una programación.  
  
        > [!NOTE]  
        >  Para obtener información sobre cómo modificar un trabajo, vea [Modificar un trabajo](../../ssms/agent/modify-a-job.md).  
  
    -   Para quitar una programación, selecciónela y haga clic en **Eliminar**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  

  
##  <a name="troubleshooting-errors-in-a-full-text-population-crawl"></a><a name="crawl"></a>Solucionar errores en un rellenado de texto completo (rastreo)  
 Cuando se produce un error durante un rastreo, la función de registro de rastreo de la búsqueda de texto completo crea y mantiene un registro de rastreo, que es un archivo sin formato. Cada registro de rastreo se corresponde con un determinado catálogo de texto completo. De forma predeterminada, los registros de rastreo de una instancia dada, en este caso la primera instancia, se ubican en la carpeta %Archivos de programa%\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\LOG. El archivo de registro de rastreo sigue el siguiente esquema de nomenclatura:  
  
 SQLFT\<DatabaseID>\<FullTextCatalogID>. LOG [\<n>]  
  
 <`DatabaseID`>  
 El identificador de una base de datos. <`dbid`> es un número de cinco dígitos con ceros a la izquierda.  
  
 <`FullTextCatalogID`>  
 Identificador de catálogo de texto completo. <`catid`> es un número de cinco dígitos con ceros a la izquierda.  
  
 <`n`>  
 Es un entero que indica la existencia de uno o varios registros de rastreo del mismo catálogo de texto completo.  
  
 Por ejemplo, SQLFT0000500008.2 es el archivo de registro de rastreo para un identificador de base de datos = 5 y un identificador de catálogo de texto completo = 8. El 2 al final del nombre de archivo indica que existen dos archivos de registro de rastreo para esta pareja de base de datos y catálogo.  
  

  
## <a name="see-also"></a>Consulte también  
 [Sys. dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)   
 [Introducción a la búsqueda de texto completo](get-started-with-full-text-search.md)   
 [Crear y administrar índices de texto completo](create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
