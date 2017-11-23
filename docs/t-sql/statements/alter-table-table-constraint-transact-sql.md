---
title: table_constraint (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CONSTRAINT_TSQL
dev_langs: TSQL
helpviewer_keywords: table_constraint
ms.assetid: ac2a11e0-cc77-4e27-b107-4fe5bc6f5195
caps.latest.revision: "59"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 464ce13d973f975fe36a73f94ec9b12cd0eb1bf3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="alter-table-tableconstraint-transact-sql"></a>ALTER TABLE table_constraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica las propiedades de una PRIMARY KEY, UNIQUE, FOREIGN KEY, una restricción CHECK o una definición DEFAULT agregada a una tabla mediante el uso de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        [ WITH ( <index_option>[ , ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ... )  
          | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )  
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | DEFAULT constant_expression FOR column [ WITH VALUES ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 CONSTRAINT  
 Especifica el inicio de una definición para una restricción PRIMARY KEY, UNIQUE, FOREIGN KEY o CHECK o una definición DEFAULT.  
  
 *constraint_name*  
 Es el nombre de la restricción. Nombres de restricción deben seguir las reglas para [identificadores](../../relational-databases/databases/database-identifiers.md), excepto en que el nombre no puede comenzar con un signo de número (#). Si no se proporciona el parámetro constraint_name, se asigna a la restricción un nombre generado por el sistema.  
  
 PRIMARY KEY  
 Es una restricción que aplica la integridad de entidad para una columna o columnas especificadas mediante un índice único. Solo se puede crear una restricción PRIMARY KEY por cada tabla.  
  
 UNIQUE  
 Es una restricción que proporciona integridad de entidad para una columna o columnas especificadas mediante un índice único.  
  
 CLUSTERED | NONCLUSTERED  
 Especifica que se ha creado un índice clúster o no clúster para la restricción PRIMARY KEY o UNIQUE. Las restricciones PRIMARY KEY tienen el valor predeterminado CLUSTERED. Las restricciones UNIQUE tienen el valor predeterminado NONCLUSTERED.  
  
 Si en una tabla ya existe una restricción o índice agrupado, no se puede especificar CLUSTERED. Si en una tabla ya existe una restricción o índice agrupado, el valor predeterminado de la restricción PRIMARY KEY es NONCLUSTERED.  
  
 Las columnas de la **ntext**, **texto**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, o **imagen** tipos de datos no se puede especificar como columnas de un índice.  
  
 *columna*  
 Es una columna o lista de columnas especificadas entre paréntesis que se utilizan en una nueva restricción.  
  
 [ **ASC** | DESC]  
 Especifica cómo se ordenan la columna o las columnas que participan en las restricciones de la tabla. El valor predeterminado es ASC.  
  
 CON valor de FILLFACTOR  **=**  *fillfactor*  
 Especifica cuánto se debe llenar cada página de índice del [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizada para almacenar los datos de índice. Especificado por el usuario *fillfactor* los valores pueden ser entre 1 y 100. Si no se especifica un valor, el valor predeterminado es 0.  
  
> [!IMPORTANT]  
>  Documentación de WITH FILLFACTOR = *fillfactor* como la única opción de índice que se aplica a las restricciones PRIMARY KEY o UNIQUE se mantiene por compatibilidad con versiones anteriores, pero no se documentará de esta manera en futuras versiones. Otras opciones de índice pueden especificarse en el [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md) cláusula de ALTER TABLE.  
  
 ON { *partition_scheme_name***(***partition_column_name***)** | *archivos* |  **"**predeterminado**"** }  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la ubicación de almacenamiento del índice creado para la restricción. Si *partition_scheme_name* se especifica, el índice tiene particiones y las particiones se asignan a los grupos de archivos que se especifican mediante *partition_scheme_name*. Si *archivos* se especifica, el índice se crea en el grupo de archivos con nombre. Si **"**predeterminado**"** se especifica o si no se especifica ON en absoluto, el índice se crea en el mismo grupo de archivos que la tabla. Si se especifica ON al agregar un índice clúster para una restricción PRIMARY KEY o UNIQUE, la tabla completa se mueve al grupo de archivos especificado cuando se crea el índice clúster.  
  
 En este contexto, valor predeterminado no es una palabra clave; es un identificador para el grupo de archivos predeterminado y debe delimitarse, como en ON **"**predeterminado**"** u ON **[**predeterminado**]**. Si **"**predeterminado**"** se especifica, la opción QUOTED_IDENTIFIER debe ser ON para la sesión actual. Esta es la configuración predeterminada.  
  
 FOREIGN KEY REFERENCES  
 Es una restricción que proporciona integridad referencial para los datos de la columna. Las restricciones FOREIGN KEY exigen que cada valor de la columna exista en la columna especificada de la tabla a la que se hace referencia.  
  
 *referenced_table_name*  
 Es la tabla a la que hace referencia la restricción FOREIGN KEY.  
  
 *ref_column*  
 Es una columna o lista de columnas entre paréntesis a la que hace referencia la nueva restricción FOREIGN KEY.  
  
 AL ELIMINAR { **NINGUNA ACCIÓN** | CASCADE | ESTABLECER COMO NULL | ESTABLECER UN VALOR PREDETERMINADO}  
 Especifica la acción que se produce en las filas de la tabla modificada, si esas filas tienen una relación referencial y la fila a la que se hace referencia se elimina de la tabla primaria. El valor predeterminado es NO ACTION.  
  
 NO ACTION  
 El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] genera un error y se revierte la acción de eliminación de la fila de la tabla primaria.  
  
 CASCADE  
 Si esa fila se elimina de la tabla primaria, las filas correspondientes se eliminan de la tabla de referencia.  
  
 SET NULL  
 Cuando se elimina la fila correspondiente de la tabla primaria, todos los valores que componen la clave externa se establecen en NULL. Para que esta restricción se ejecute, las columnas de clave externa deben aceptar valores NULL.  
  
 SET DEFAULT  
 Cuando se elimina la fila correspondiente de la tabla primaria, todos los valores que componen la clave externa se establecen en sus valores predeterminados. Para que esta restricción se ejecute, todas las columnas de clave externa deben tener definiciones predeterminadas. Si una columna acepta valores NULL y no se ha establecido un valor predeterminado explícito, NULL se convierte en el valor predeterminado explícito de dicha columna.  
  
 No especifique CASCADE si la tabla se va a incluir en una publicación de combinación que utiliza registros lógicos. Para obtener más información sobre los registros lógicos, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 No se puede definir la acción ON DELETE CASCADE si ya existe un desencadenador INSTEAD OF en ON DELETE en la tabla que se está modificando.  
  
 Por ejemplo, en la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos, el **ProductVendor** tabla tiene una relación referencial con la **proveedor** tabla. El **ProductVendor.VendorID** referencias de clave externa del **Vendor.VendorID** clave principal.  
  
 Si se ejecuta una instrucción DELETE en una fila de la **proveedor** se especifica la tabla y una acción ON DELETE CASCADE para **ProductVendor.VendorID**, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba si hay una o varias filas dependientes en la **ProductVendor** tabla. Si las hay, las filas dependientes de la **ProductVendor** tabla eliminarán, así como la fila que se hace referencia en el **proveedor** tabla.  
  
 Por el contrario, si se especifica NO ACTION, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y revierte la acción de eliminación de la **proveedor** fila cuando hay al menos una fila en la **ProductVendor** tabla que hace referencia a él.  
  
 EN ACTUALIZACIÓN { **NINGUNA ACCIÓN** | CASCADE | ESTABLECER COMO NULL | ESTABLECER UN VALOR PREDETERMINADO}  
 Especifica la acción que se produce en las filas de la tabla modificada cuando esas filas tienen una relación referencial y la fila a la que se hace referencia se actualiza en la tabla primaria. El valor predeterminado es NO ACTION.  
  
 NO ACTION  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y se revierte la acción de actualización de la fila de la tabla primaria.  
  
 CASCADE  
 Si esa fila se actualiza en la tabla primaria, las filas correspondientes se actualizan en la tabla de referencia.  
  
 SET NULL  
 Cuando se actualiza la fila correspondiente en la tabla primaria, todos los valores que componen la clave externa se establecen en NULL. Para que esta restricción se ejecute, las columnas de clave externa deben aceptar valores NULL.  
  
 SET DEFAULT  
 Cuando se actualiza la fila correspondiente en la tabla primaria, todos los valores que componen la clave externa se establecen en sus valores predeterminados. Para que esta restricción se ejecute, todas las columnas de clave externa deben tener definiciones predeterminadas. Si una columna acepta valores NULL y no se ha establecido un valor predeterminado explícito, NULL se convierte en el valor predeterminado explícito de dicha columna.  
  
 No especifique CASCADE si la tabla se va a incluir en una publicación de combinación que utiliza registros lógicos. Para obtener más información sobre los registros lógicos, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 No se puede definir ON UPDATE CASCADE, SET NULL o SET DEFAULT si ya existe un desencadenador INSTEAD OF en ON UPDATE en la tabla que se va a modificar.  
  
 Por ejemplo, en la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos, el **ProductVendor** tabla tiene una relación referencial con la **proveedor** tabla. El **ProductVendor.VendorID** referencias de clave externa del **Vendor.VendorID** clave principal.  
  
 Si se ejecuta una instrucción UPDATE en una fila en la **proveedor** tabla y una acción ON UPDATE CASCADE se especifica para **ProductVendor.VendorID**, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba si hay una o varias filas dependientes en la **ProductVendor** tabla. Si existe alguna, la fila dependiente de la **ProductVendor** tabla se actualizará, así como la fila que se hace referencia en el **proveedor** tabla.  
  
 Por el contrario, si se especifica NO ACTION, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error y revierte la acción de actualización de la **proveedor** fila cuando hay al menos una fila en la **ProductVendor** tabla que hace referencia a él.  
  
 NOT FOR REPLICATION  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se puede especificar para restricciones FOREIGN KEY y CHECK. Si se especifica esta cláusula para una restricción, la restricción no se aplica cuando los agentes de replicación realizan operaciones de inserción, actualización o eliminación.  
  
 DEFAULT  
 Especifica el valor predeterminado de la columna. Las definiciones DEFAULT se pueden utilizar para proporcionar valores a una nueva columna de las filas existentes de datos. Las definiciones DEFAULT no se pueden agregar a las columnas que tienen un **timestamp** tipo de datos, una propiedad IDENTITY, una definición DEFAULT existente o un valor predeterminado enlazado. Si la columna tiene un valor predeterminado existente, éste debe quitarse para poder agregar uno nuevo. Si se especifica un valor predeterminado para una columna de tipo definido por el usuario, el tipo debe admitir una conversión implícita de *expresiónConstante* para el tipo definido por el usuario. Para mantener la compatibilidad con las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se puede asignar un nombre de restricción a DEFAULT.  
  
 *expresiónConstante*  
 Es un valor literal, un valor NULL o una función del sistema que se utiliza como valor predeterminado de la columna. Si *expresiónConstante* se usa junto con una columna definida como de un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipo definido por el usuario, la implementación del tipo debe admitir una conversión implícita de la *constant_ expresión* para el tipo definido por el usuario.  
  
 PARA *columna*  
 Especifica la columna asociada a una definición DEFAULT de nivel de tabla.  
  
 WITH VALUES  
 Especifica que el valor dado en DEFAULT *expresiónConstante* se almacena en una nueva columna que se agrega a las filas existentes. WITH VALUES solo puede especificarse cuando se especifique DEFAULT en una cláusula de columna ADD. Si la columna agregada permite valores NULL y se ha especificado WITH VALUES, el valor predeterminado se almacena en la nueva columna que se agrega a las filas existentes. Si no se especifica WITH VALUES para las columnas que permiten valores NULL, el valor NULL se almacena en la nueva columna en las filas existentes. Si la nueva columna no permite valores NULL, el valor predeterminado se almacena en las nuevas filas, independientemente de que se especifique o no WITH VALUES.  
  
 CHECK  
 Es una restricción que exige la integridad del dominio al limitar los valores posibles que se pueden escribir en una o varias columnas.  
  
 *Filter*  
 Es una expresión lógica empleada en una restricción CHECK que devuelve TRUE o FALSE. *Filter* utilizado con comprobación de restricciones no se puede hacer referencia a otra tabla, pero puede hacer referencia a otras columnas de la misma tabla para la misma fila. La expresión no puede hacer referencia a un tipo de datos de alias.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se agregan restricciones FOREIGN KEY o CHECK, se comprueba si hay infracciones de restricción en todos los datos existentes a menos que se especifique la opción WITH NOCHECK. Si se produce alguna infracción, ALTER TABLE no se ejecuta correctamente y se devuelve un error. Cuando se agrega una nueva restricción PRIMARY KEY o UNIQUE a una columna existente, los datos de las columnas deben ser únicos. Si se detectan valores duplicados, ALTER TABLE no se ejecuta correctamente. La opción WITH NOCHECK no tiene efecto cuando se agregan restricciones PRIMARY KEY o UNIQUE.  
  
 Cada restricción PRIMARY KEY y UNIQUE genera un índice. El número de restricciones UNIQUE y PRIMARY KEY no puede hacer que el número de índices de la tabla supere 999 índices no clúster y 1 índice clúster. Las restricciones de clave externa no generan automáticamente un índice. Sin embargo, las columnas de clave externa suelen emplearse en los criterios de combinación en consultas mediante la correspondencia de la columna o columnas de la restricción de clave externa de una tabla y la columna o columnas de la clave única o principal de la otra tabla. Un índice de las columnas de clave externa permite al [!INCLUDE[ssDE](../../includes/ssde-md.md)] buscar con rapidez datos relacionados en la tabla de clave externa.  
  
## <a name="examples"></a>Ejemplos  
 Para obtener ejemplos, vea [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
