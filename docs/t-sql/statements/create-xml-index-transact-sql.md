---
title: "Crear índice XML (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- XML_TSQL
- CREATE_XML_INDEX_TSQL
- XML INDEX
- CREATE_XML_TSQL
- XML
- CREATE XML
- CREATE XML INDEX
- XML_INDEX_TSQL
- FOR_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- CREATE INDEX statement
- index creation [SQL Server], XML indexes
- XML indexes [SQL Server], creating
ms.assetid: c510cfbc-68be-4736-b3cc-dc5b7aa51f14
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9e235df8fe59bc86522ece554a75e22954fef1b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-xml-index-transact-sql"></a>CREATE XML INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea un índice XML en una tabla especificada. Se puede crear un índice antes de que la tabla posea datos. Es posible crear índices XML sobre tablas de otra base de datos si se especifica un nombre de base de datos completo.  
  
> [!NOTE]  
>  Para crear un índice relacional, vea [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md). Para obtener información sobre cómo crear un índice espacial, vea [CREATE SPATIAL INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Create XML Index   
CREATE [ PRIMARY ] XML INDEX index_name   
    ON <object> ( xml_column_name )  
    [ USING XML INDEX xml_index_name   
        [ FOR { VALUE | PATH | PROPERTY } ] ]  
    [ WITH ( <xml_index_option> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_name  
}  
  
<xml_index_option> ::=  
{   
    PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [PRIMARY] XML  
 Crea un índice XML en las clases **xml** columna. Cuando se especifica PRIMARY, se crea un índice clúster con la clave clúster formada a partir de la clave de agrupación en clústeres de la tabla de usuario y un identificador del nodo XML. Cada tabla puede tener hasta 249 índices XML. Observe lo siguiente cuando cree un índice XML:  
  
-   Debe existir un índice clúster en la clave principal de la tabla de usuario.  
  
-   La clave de agrupación en clústeres de la tabla de usuario tiene un límite de 15 columnas.  
  
-   Cada **xml** columna de una tabla puede tener un índice XML principal y varios índices XML secundarios.  
  
-   Un índice XML principal en un **xml** columna debe existir antes de poder crear un índice XML secundario en la columna.  
  
-   Solo se puede crear un índice XML en un único servidor **xml** columna. No se puede crear un índice XML en no**xml** columna, ni tampoco puede crear un índice relacional en una **xml** columna.  
  
-   No se puede crear un índice XML principal o secundario, en un **xml** columna en una vista, en una variable con valores de tabla con **xml** columnas, o **xml** variables de tipo.  
  
-   No se puede crear un índice XML principal en una calculada **xml** columna.  
  
-   La configuración de la opción SET debe ser la misma que la requerida para vistas indizadas e índices de columnas calculadas. En concreto, la opción ARITHABORT debe establecerse en ON cuando se crea un índice XML y al insertar, eliminar o actualizar valores en el **xml** columna.  
  
 Para obtener más información, consulte [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
 *index_name*  
 Es el nombre del índice. Los nombres de índice deben ser únicos en una tabla, pero no es necesario que sean únicos en una base de datos. Los nombres de índice deben seguir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 Los nombres de índice XML principal no pueden empezar con los siguientes caracteres:  **#** ,  **##** ,  **@** , o  **@@**  .  
  
 *xml_column_name*  
 Es el **xml** en que se basa el índice de columna. Solo un **xml** columna puede especificarse en una única definición de índice XML; sin embargo, pueden crearse varios índices XML secundarios en un **xml** columna.  
  
 USING XML INDEX *xml_index_name*  
 Especifica el índice XML principal que se usará para la creación de un índice XML secundario.  
  
 FOR { VALUE | PATH | PROPERTY }  
 Especifica el tipo de índice XML secundario.  
  
 Value  
 Crea un índice XML secundario en las columnas en las que se encuentran las columnas de clave (ruta y valor del nodo) del índice XML principal.  
  
 PATH  
 Crea un índice XML secundario en las columnas generadas a partir de valores de ruta y de nodo del índice XML principal. En el índice secundario PATH, los valores de ruta y de nodo son las columnas de clave que permiten exploraciones eficaces en la búsqueda de rutas.  
  
 PROPERTY  
 Crea un índice XML secundario en las columnas (PK, y valor de ruta y de nodo) del índice XML principal, donde PK es la clave principal de la tabla base.  
  
 **\<objeto >:: =**  
  
 Es el objeto completo o no que se indizará.  
  
 *database_name*  
 Es el nombre de la base de datos.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la tabla.  
  
 *table_name*  
 Es el nombre de la tabla que va a indizarse.  
  
 **\<xml_index_option >:: =** 
  
 Especifica las opciones que se van a utilizar en la creación del índice.  
  
 PAD_INDEX  **=**  {ON | **OFF** }  
 Especifica el relleno del índice. El valor predeterminado es OFF.  
  
 ON  
 El porcentaje de espacio disponible especificado por *fillfactor* se aplica a las páginas de nivel intermedio del índice.  
  
 DESACTIVAR o *fillfactor* no se ha especificado  
 Las páginas de nivel intermedio se llenan casi al máximo de su capacidad y dejan espacio suficiente para al menos una fila del tamaño máximo que puede tener el índice, considerando el conjunto de claves incluidas en las páginas de nivel intermedio.  
  
 La opción PAD_INDEX solamente resulta útil si también se especifica FILLFACTOR, porque PAD_INDEX utiliza el mismo porcentaje especificado por FILLFACTOR. Si el porcentaje especificado para FILLFACTOR no es lo suficientemente grande como para admitir una fila, [!INCLUDE[ssDE](../../includes/ssde-md.md)] invalida internamente el porcentaje para permitir el valor mínimo. El número de filas de una página de índice intermedio es nunca inferior a dos, independientemente de lo bajo el valor de *fillfactor*.  
  
 Valor de FILLFACTOR  **=**  *fillfactor*  
 Especifica un porcentaje que indica cuánto debe llenar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] el nivel hoja de cada página de índice durante la creación o nueva generación de los índices. *valor de FILLFACTOR* debe ser un valor entero entre 1 y 100. El valor predeterminado es 0. Si *fillfactor* es 100 ó 0, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea índices con páginas hoja rellenadas en capacidad.  
  
> [!NOTE]  
>  Los valores de fill factor 0 y 100 son idénticos.  
  
 La configuración de FILLFACTOR solo se aplica cuando se crea o se vuelve a generar el índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mantiene dinámicamente el porcentaje especificado de espacio disponible de las páginas. Para ver el valor de factor de relleno, use la [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo.  
  
> [!IMPORTANT]  
>  La creación de un índice clúster con un valor de FILLFACTOR menor que 100 afecta a la cantidad de espacio de almacenamiento que ocupan los datos, porque [!INCLUDE[ssDE](../../includes/ssde-md.md)] vuelve a distribuir los datos cuando crea el índice clúster.  
  
 Para obtener más información, vea [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 SORT_IN_TEMPDB  **=**  {ON | **OFF** }  
 Especifica si se debe almacenar los resultados de ordenación temporales en **tempdb**. El valor predeterminado es OFF.  
  
 ON  
 Los resultados de orden intermedio que se usan para generar el índice se almacenan en **tempdb**. Esto puede reducir el tiempo necesario para crear un índice si **tempdb** está en un conjunto diferente de discos que en la base de datos de usuario. Sin embargo, esto aumenta la cantidad de espacio en disco utilizado durante la generación del índice.  
  
 OFF  
 Los resultados de orden intermedios se almacenan en la misma base de datos que el índice.  
  
 Además del espacio necesario en la base de datos de usuario para crear el índice, **tempdb** debe tener la misma cantidad de espacio adicional para almacenar los resultados de orden intermedio. Para obtener más información, consulte [opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY **= OFF**  
 No tiene ningún efecto sobre los índices XML porque el tipo de índice nunca es único. No establezca esta opción en ON porque, de lo contrario, se producirá un error.  
  
 DROP_EXISTING  **=**  {ON | **OFF** }  
 Especifica que se quite y vuelva a generarse el índice XML con nombre preexistente. El valor predeterminado es OFF.  
  
 ON  
 El índice existente se quita y se vuelve a generar. El nombre de índice especificado debe ser el mismo que el de un índice actualmente existente; sin embargo, la definición se puede modificar. Por ejemplo, puede especificar columnas, criterio de ordenación, esquema de particionamiento u opciones de índice diferentes.  
  
 OFF  
 Se muestra un error si ya existe el nombre de índice especificado.  
  
 El tipo de índice no puede cambiarse utilizando DROP_EXISTING. Asimismo, un índice XML principal no puede volver a definirse como un índice XML secundario, o viceversa.  
  
 EN LÍNEA **= OFF**  
 Especifica que las tablas subyacentes y los índices asociados no están disponibles para la realización de consultas y modificaciones de datos durante la operación del índice. En esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no se admiten generaciones de índices en línea para los índices XML. Si esta opción se establece en ON para un índice XML, se produce un error. Omita la opción ONLINE o establezca ONLINE en OFF.  
  
 Una operación de índice sin conexión para crear, volver a crear o quitar un índice XML adquiere un bloqueo de modificación del esquema (Sch-M) de la tabla. Esto evita que todos los usuarios tengan acceso a la tabla subyacente durante la operación.  
  
> [!NOTE]  
>  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** | {OFF}  
 Especifica si se permiten los bloqueos de fila. El valor predeterminado es ON.  
  
 ON  
 Los bloqueos de fila se admiten al obtener acceso al índice. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina cuándo se usan los bloqueos de fila.  
  
 OFF  
 No se usan los bloqueos de fila.  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** | {OFF}  
 Especifica si se permiten bloqueos de página. El valor predeterminado es ON.  
  
 ON  
 Los bloqueos de página se permiten al obtener acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina el momento en que se usan los bloqueos de página.  
  
 OFF  
 No se utilizan bloqueos de página.  
  
 MAXDOP  **=**  *max_degree_of_parallelism*  
 Invalida el [configurar la max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) opción de configuración para la duración de la operación de índice. Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.  
  
> [!IMPORTANT]  
>  Aunque la opción MAXDOP se admite sintácticamente para todos los índices XML, para un índice XML primario, CREATE XML INDEX utiliza un solo procesador.  
  
 *max_degree_of_parallelism* puede ser:  
  
 1  
 Suprime la generación de planes paralelos.  
  
 \>1  
 Restringe el número máximo de procesadores utilizados en una operación de índice paralelo al número especificado o a un número inferior, en función de la actual carga de trabajo del sistema.  
  
 0 (predeterminado)  
 Usa el número real de procesadores o menos, según la carga de trabajo actual del sistema.  
  
 Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Operaciones de índice en paralelo no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="remarks"></a>Comentarios  
 Las columnas calculadas derivadas de **xml** pueden ser tipos de datos como una columna sin clave incluida o de clave indizar siempre que el tipo de datos de columna calculada esté disponible como una columna de clave de índice o columna sin clave. No se puede crear un índice XML principal en una calculada **xml** columna.  
  
 Para ver información sobre los índices XML, use la [sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md) vista de catálogo.  
  
 Para obtener más información sobre los índices XML, vea [índices XML &#40; SQL Server &#41; ](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="additional-remarks-on-index-creation"></a>Notas adicionales sobre la creación de índices  
 Para obtener más información acerca de la creación de índices, vea la sección "Comentarios" en [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-primary-xml-index"></a>A. Crear un índice XML principal  
 El ejemplo siguiente crea un índice XML principal en la columna `CatalogDescription` de la tabla `Production.ProductModel`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT * FROM sys.indexes  
            WHERE name = N'PXML_ProductModel_CatalogDescription')  
    DROP INDEX PXML_ProductModel_CatalogDescription   
        ON Production.ProductModel;  
GO  
CREATE PRIMARY XML INDEX PXML_ProductModel_CatalogDescription  
    ON Production.ProductModel (CatalogDescription);  
GO  
```  
  
### <a name="b-creating-a-secondary-xml-index"></a>B. Crear un índice XML secundario  
 El ejemplo siguiente crea un índice XML secundario en la columna `CatalogDescription` de la tabla `Production.ProductModel`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.indexes  
            WHERE name = N'IXML_ProductModel_CatalogDescription_Path')  
    DROP INDEX IXML_ProductModel_CatalogDescription_Path  
        ON Production.ProductModel;  
GO  
CREATE XML INDEX IXML_ProductModel_CatalogDescription_Path   
    ON Production.ProductModel (CatalogDescription)  
    USING XML INDEX PXML_ProductModel_CatalogDescription FOR PATH ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [Crear índice espacial &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Sys.xml_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  


