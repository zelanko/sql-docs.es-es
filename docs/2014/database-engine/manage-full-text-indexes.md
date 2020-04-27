---
title: Administrar índices de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 28ff17dc-172b-4ac4-853f-990b5dc02fd1
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 459bdc20c9698a8b6271092c57ed0de936c4d7f2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775047"
---
# <a name="manage-full-text-indexes"></a>Administrar índices de texto completo
     
##  <a name="viewing-and-changing-the-properties-of-a-full-text-index"></a><a name="view"></a>Ver y cambiar las propiedades de un índice de texto completo  
  
#### <a name="to-view-or-change-the-properties-of-a-full-text-index-in-management-studio"></a>Para ver o cambiar las propiedades de un índice de texto completo en Management Studio  
  
1.  En el Explorador de objetos, expanda el servidor.  
  
2.  Expanda **Bases de datos**y, después, la base de datos que contiene el índice de texto completo.  
  
3.  Expanda **Tablas**.  
  
4.  Haga clic con el botón derecho en la tabla en la que esté definido el índice de texto completo, seleccione **Índice de texto completo**y, en el menú contextual **Índice de texto completo** , haga clic en **Propiedades**. De esta forma se abre el cuadro de diálogo **Propiedades del índice de texto completo** .  
  
5.  En el panel **Seleccionar una página** , puede seleccionar cualquiera de las páginas siguientes:  
  
    |Página|Descripción|  
    |----------|-----------------|  
    |**General**|Muestra las propiedades básicas de un índice de texto completo. Entre estas propiedades se incluyen varias propiedades modificables y varias propiedades invariables, como el nombre de base de datos, el nombre de tabla y el nombre de columna de clave de texto completo. Las propiedades modificables son:<br /><br /> **Lista de palabras irrelevantes de índice de texto completo**<br /><br /> **Indexación de texto completo habilitada**<br /><br /> **Seguimiento de cambios**<br /><br /> **Lista de propiedades de búsqueda**<br /><br /> <br /><br /> Para obtener más información, vea [Propiedades del índice de texto completo &#40;página General&#41;](full-text-index-properties-general-page.md).|  
    |**Columnas**|Muestra las columnas de tabla que están disponibles para la indización de texto completo. La columna o columnas seleccionadas son de índices de texto completo. Puede seleccionar tantas columnas disponibles como desee incluir en el índice de texto completo. Para obtener más información, vea [Propiedades del índice de texto completo &#40;página Columnas&#41;](../../2014/database-engine/full-text-index-properties-columns-page.md).|  
    |**Programaciones**|Utilice esta página para crear o administrar programaciones para un trabajo del Agente SQL Server que inicie un rellenado de tabla incremental para los rellenados del índice de texto completo. Para obtener más información, vea [Rellenar índices de texto completo](../relational-databases/indexes/indexes.md).<br /><br /> <strong> \* Importante \* \* </strong> Después de salir del cuadro de diálogo **propiedades del índice de texto completo** , cualquier programación recién creada se asocia a una agente SQL Server trabajo (iniciar rellenado de tabla incremental en *database_name*.* table_name*).|  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] para guardar cualquier cambio y salir del cuadro de diálogo **Propiedades del índice de texto completo**.  
  
##  <a name="viewing-the-properties-of-indexed-tables-and-columns"></a><a name="props"></a>Ver las propiedades de las tablas y columnas indizadas  
 Varias de las funciones de [!INCLUDE[tsql](../includes/tsql-md.md)], como OBJECTPROPERTYEX, se pueden usar para obtener el valor de diversas propiedades de indización de texto completo. Esta información es útil para administrar y solucionar problemas de la búsqueda de texto completo.  
  
 En la siguiente tabla se enumeran las propiedades de texto completo relacionadas con las tablas y columnas indexadas y sus funciones de [!INCLUDE[tsql](../includes/tsql-md.md)] relacionadas.  
  
|Propiedad|Descripción|Función|  
|--------------|-----------------|--------------|  
|`FullTextTypeColumn`|TYPE COLUMN de la tabla que contiene la información del tipo de documento de la columna.|[COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql)|  
|`IsFulltextIndexed`|Si una columna se ha habilitado para la indización de texto completo.|COLUMNPROPERTY|  
|`IsFulltextKey`|Si el índice es la clave de texto completo de una tabla.|[INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql)|  
|**TableFulltextBackgroundUpdateIndexOn**|Si una tabla tiene actualización de índices de texto completo en segundo plano.|[OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql)|  
|`TableFulltextCatalogId`|Identificador del catálogo de texto completo en el que residen los datos de índice de texto completo para la tabla.|OBJECTPROPERTYEX|  
|`TableFulltextChangeTrackingOn`|Si una tabla tiene habilitado el seguimiento de cambios de texto completo.|OBJECTPROPERTYEX|  
|`TableFulltextDocsProcessed`|Número de filas procesadas desde el comienzo de la indización de texto completo.|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|Número de filas no indizadas por Búsqueda de texto completo.|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|Número de filas para las que se crearon índices de texto completo correctamente.|OBJECTPROPERTYEX|  
|`TableFulltextKeyColumn`|Proporciona el identificador de la columna de clave única de texto completo.|OBJECTPROPERTYEX|  
|`TableFullTextMergeStatus`|Si una tabla que tiene un índice de texto completo se está combinando actualmente.|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|Número de entradas de seguimiento de cambios pendientes de procesamiento.|OBJECTPROPERTYEX|  
|`TableFulltextPopulateStatus`|Estado del rellenado de una tabla de texto completo.|OBJECTPROPERTYEX|  
|`TableHasActiveFulltextIndex`|Si la tabla tiene un índice de texto completo activo.|OBJECTPROPERTYEX|  
  
##  <a name="getting-information-about-the-full-text-key-column"></a><a name="key"></a>Obtener información sobre la columna de clave de texto completo  
 Normalmente, el resultado de las funciones de valores de conjunto de filas CONTAINSTABLE o FREETEXTTABLE tiene que combinarse con la tabla base. En esos casos, necesita conocer el nombre de la columna de clave única. Puede consultar si un índice único determinado se utiliza como clave de texto completo y obtener el identificador de la columna de clave de texto completo.  
  
#### <a name="to-inquire-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>Para consultar si un índice único determinado se utiliza como columna de clave de texto completo  
  
1.  Utilice una instrucción [SELECT](/sql/t-sql/queries/select-transact-sql) para llamar a la función [INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql) . En la llamada de función, use la función OBJECT_ID para convertir el nombre de la tabla (*TABLE_NAME*) en el identificador de tabla, especifique el nombre de un índice único para la tabla y `IsFulltextKey` especifique la propiedad de índice de la siguiente manera:  
  
    ```  
    SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
    ```  
  
     Esta instrucción devuelve el valor 1 si el índice se usa para exigir la exclusividad de la columna de clave de texto completo; de lo contrario, se devuelve 0.  
  
 **Ejemplo**  
  
 El ejemplo siguiente consulta si el índice `PK_Document_DocumentID` se usa para exigir la exclusividad de la columna de clave de texto completo como sigue:  
  
```  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentID',  'IsFulltextKey' )  
```  
  
 Este ejemplo devuelve 1 si el índice `PK_Document_DocumentID` se utiliza para exigir la exclusividad de la columna de clave de texto completo. De lo contrario, devuelve 0 o NULL. NULL implica que está usando un nombre de índice no válido, el nombre de índice no corresponde a la tabla, la tabla no existe, etcétera.  
  
#### <a name="to-find-the-identifier-of-the-full-text-key-column"></a>Para buscar el identificador de la columna de clave de texto completo  
  
1.  Todas las tablas habilitadas para texto completo tienen una columna que se usa para aplicar las filas únicas de la tabla (*columna de clave**única*). La propiedad `TableFulltextKeyColumn` obtenida mediante la función OBJECTPROPERTY proporciona la identidad de esta columna de clave única.  
  
     Para obtener este identificador, puede utilizar una instrucción SELECT con el fin de llamar a la función OBJECTPROPERTYEX. Utilice la función OBJECT_ID para convertir el nombre de la tabla (*TABLE_NAME*) en el identificador de tabla y especificar `TableFulltextKeyColumn` la propiedad, como se indica a continuación:  
  
    ```  
    SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
    ```  
  
 **Ejemplos**  
  
 En el ejemplo siguiente se devuelve el identificador de la columna de clave de texto completo o NULL. NULL implica que está usando un nombre de índice no válido, el nombre de índice no corresponde a la tabla, la tabla no existe, etcétera.  
  
```  
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 En el ejemplo siguiente se muestra cómo usar el identificador de la columna de clave única para obtener el nombre de la columna.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 Este ejemplo devuelve una columna de conjunto de resultados denominada `Unique Key Column`, que muestra una única fila que contiene el nombre de la columna de clave única de la tabla Document, DocumentID. Tenga en cuenta que, si esta consulta contuviera un nombre de índice no válido, el nombre del índice no correspondiera a la tabla, la tabla no existiera, etc., devolvería NULL.  
  
##  <a name="disabling-or-re-enabling-a-table-for-full-text-indexing"></a><a name="disable"></a>Deshabilitar o volver a habilitar una tabla para la indización de texto completo  
 En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], todas las bases de datos creadas por el usuario están habilitadas para texto completo de forma predeterminada. Además, una tabla individual se habilitará automáticamente para la indización de texto completo en cuanto se cree un índice de texto completo en la misma y se agregue una columna al índice. Una tabla se deshabilitará automáticamente para la indización de texto completo cuando se quite la última columna de su índice de texto completo.  
  
 En una tabla que tiene un índice de texto completo, se puede deshabilitar o volver a habilitar manualmente una tabla para la indización de texto completo utilizando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-enable-a-table-for-full-text-indexing"></a>Para habilitar una tabla para la indización de texto completo  
  
1.  Expanda el grupo de servidores, expanda **Bases de datos**y luego expanda la base de datos que contenga la tabla que quiera habilitar para la indexación de texto completo.  
  
2.  Expanda **Tablas**y haga clic con el botón derecho en la tabla que quiere deshabilitar o volver a habilitar para la indexación de texto completo.  
  
3.  Seleccione **Índice de texto completo**y luego haga clic en **Deshabilitar índice de texto completo** o en **Habilitar índice de texto completo**.  
  
##  <a name="removing-a-full-text-index-from-a-table"></a><a name="remove"></a>Quitar un índice de texto completo de una tabla  
  
#### <a name="to-remove-a-full-text-index-from-a-table"></a>Para quitar un índice de texto completo de una tabla  
  
1.  En el Explorador de objetos, haga clic con el botón secundario en la tabla que contiene el índice de texto completo que desea eliminar.  
  
2.  Seleccione **Eliminar índice de texto completo**.  
  
3.  Cuando se le pida, haga clic en **Aceptar** para confirmar que quiere eliminar el índice de texto completo.  
  
  
