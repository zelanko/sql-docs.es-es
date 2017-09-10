---
title: "definición_de_columna (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_definition
- column_definition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column_definition
- ALTER TABLE statement
- column properties [SQL Server]
- column definitions [SQL Server]
ms.assetid: a1742649-ca29-4d9b-9975-661cdbf18f78
caps.latest.revision: 78
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c63dcea3473198ded46ebf84053fa9d8b36330f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-columndefinition-transact-sql"></a>ALTER TABLE definición_de_columna (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica las propiedades de una columna que se agregan a una tabla mediante [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
column_name <data_type>  
[ FILESTREAM ]  
[ COLLATE collation_name ]   
[ NULL | NOT NULL ]  
[   
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression [ WITH VALUES ]   
    | IDENTITY [ ( seed , increment ) ] [ NOT FOR REPLICATION ]   
]  
[ ROWGUIDCOL ]   
[ SPARSE ]   
[ ENCRYPTED WITH  
  ( COLUMN_ENCRYPTION_KEY = key_name ,  
      ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
      ALGORITHM =  'AEAD_AES_256_CBC_HMAC_SHA_256'   
  ) ]  
[ MASKED WITH ( FUNCTION = ' mask_function ') ]  
[ <column_constraint> [ ...n ] ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *column_name*  
 Es el nombre de la columna que se va a modificar, agregar o quitar. *column_name* puede tener de 1 a 128 caracteres. Para las columnas nuevas creadas con un tipo de datos de marca de tiempo, *column_name* puede omitirse. Si no hay ningún *column_name* se especifica para un **timestamp** columna tipo de datos, el nombre **marca de tiempo** se utiliza.  
  
 [ *type_schema_name***.** ] *type_name*  
 Es el tipo de datos de la columna agregada y el esquema al que pertenece.  
  
 *TYPE_NAME* puede ser:  
  
-   A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos del sistema.  
  
-   Un tipo de datos del alias basado en el tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los tipos de datos de alias deben crearse mediante CREATE TYPE para poder utilizarse en una definición de tabla.  
  
-   A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipo definido por el usuario y el esquema al que pertenece. Un tipo de datos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] definido por el usuario debe crearse mediante CREATE TYPE para poder utilizarse en una definición de tabla.  
  
 Si *type_schema_name* no se especifica, el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] referencias *type_name* en el siguiente orden:  
  
-   El tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El esquema predeterminado del usuario actual en la base de datos actual.  
  
-   El esquema **dbo** de la base de datos actual.  
  
*precisión*  
 Es la precisión del tipo de datos especificado. Para obtener más información acerca de los valores de precisión válidos, consulte [precisión, escala y longitud &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
*escala*  
 Es la escala del tipo de datos especificado. Para obtener más información acerca de los valores de escala válidos, consulte [precisión, escala y longitud &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
**max**  
 Solo se aplica a la **varchar**, **nvarchar**, y **varbinary** tipos de datos. Éstos se utilizan para almacenar 2^31 bytes de datos de caracteres y binarios y 2^30 bytes de datos Unicode.  
  
**CONTENIDO**  
 Especifica que cada instancia de la **xml** tipo de datos en *column_name* puede incluir varios elementos de nivel superior. El contenido se aplica solo a la **xml** datos escriba y se puede especificar únicamente si *xml_schema_collection* también se especifica. Si no se especifica este último parámetro, CONTENT es el comportamiento predeterminado.  
  
DOCUMENT  
 Especifica que cada instancia de la **xml** tipo de datos en *column_name* puede incluir un único elemento de nivel superior. DOCUMENTO solo se aplica a la **xml** datos escriba y se puede especificar únicamente si *xml_schema_collection* también se especifica.  
  
 *xml_schema_collection*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a la **xml** tipo de datos para asociar una colección de esquemas XML con el tipo. Antes de escribir un **xml** columna a un esquema, el esquema debe crearse en la base de datos mediante el uso de [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
FILESTREAM  
 Opcionalmente, especifica el atributo de almacenamiento FILESTREAM para la columna que tiene un *type_name* de **varbinary (max)**.  
  
 Si se especifica FILESTREAM para una columna, la tabla también debe tener una columna de la **uniqueidentifier** tipo de datos que tiene el atributo ROWGUIDCOL. Esta columna no debe permitir valores nulos y debe tener una restricción de columna única UNIQUE o PRIMARY KEY. El valor GUID para la columna debe ser suministrado por una aplicación cuando se insertan los datos o por una restricción DEFAULT que utiliza la función NEWID ().  
  
 No se puede quitar la columna ROWGUIDCOL ni se pueden cambiar las restricciones relacionadas si hay definida una columna FILESTREAM para la tabla. Solamente se puede quitar la columna ROWGUIDCOL después de quitarse la última columna FILESTREAM.  
  
 Si se especifica el atributo de almacenamiento FILESTREAM para una columna, todos los valores para dicha columna se almacenan en un contenedor de datos de FILESTREAM del sistema de archivos.  
  
 Para obtener un ejemplo que muestra cómo utilizar la definición de columna, vea [FILESTREAM &#40; SQL Server &#41; ](../../relational-databases/blob/filestream-sql-server.md).  
  
COLLATE *collation_name*  
 Especifica la intercalación de la columna. Si no se especifica, se asigna a la columna la intercalación predeterminada de la base de datos. Nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Para obtener una lista y obtener más información, vea [nombre de intercalación de Windows &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) y [SQL nombre de intercalación de servidor &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 La cláusula COLLATE se puede utilizar para especificar únicamente las intercalaciones de columnas de la **char**, **varchar**, **nchar**, y **nvarchar** tipos de datos .  
  
 Para obtener más información acerca de la cláusula COLLATE, consulte [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
 NULL | NOT NULL  
 Determina si se permiten valores NULL en la columna. NULL no es estrictamente una restricción, pero se puede especificar, al igual que NOT NULL.  
  
[Restricción *constraint_name* ]  
 Especifica el inicio de una definición de valor DEFAULT. Para mantener la compatibilidad con las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se puede asignar un nombre de restricción a DEFAULT. *constraint_name* debe cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md), excepto en que el nombre no puede comenzar con un signo de número (#). Si *constraint_name* no se especifica, se asigna un nombre generado por el sistema a la definición DEFAULT.  
  
DEFAULT  
 Es una palabra clave que especifica el valor predeterminado de la columna. Las definiciones DEFAULT se pueden utilizar para proporcionar valores a una nueva columna de las filas existentes de datos. Las definiciones DEFAULT no se puede aplicar a **timestamp** columnas o columnas con una propiedad IDENTITY. Si se especifica un valor predeterminado para una columna de tipo definido por el usuario, el tipo debe admitir una conversión implícita de *expresiónConstante* para el tipo definido por el usuario.  
  
*expresiónConstante*  
 Es un valor literal, un valor NULL o una función de sistema que se usa como el valor de columna predeterminado. Si se usa junto con una columna definida como de un [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipo definido por el usuario, la implementación del tipo debe admitir una conversión implícita de la *expresiónConstante* para el tipo definido por el usuario.  
  
WITH VALUES  
 Especifica que el valor dado en DEFAULT *expresiónConstante* se almacena en una nueva columna agregada a las filas existentes. Si la columna agregada permite valores NULL y se ha especificado WITH VALUES, el valor predeterminado se almacena en la nueva columna agregada a las filas existentes. Si no se especifica WITH VALUES para las columnas que permiten valores NULL, el valor NULL se almacena en la nueva columna en las filas existentes. Si la nueva columna no permite valores NULL, el valor predeterminado se almacena en las nuevas filas, independientemente de que se especifique o no WITH VALUES.  
  
IDENTITY  
 Especifica que la nueva columna es una columna de identidad. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] proporciona un valor incremental único para la columna. Al agregar columnas de identificadores a tablas existentes, los números de identidad se agregan a las filas existentes de la tabla con los valores de inicialización e incremento. No se garantiza el orden en que las filas se actualizan. También se generan números de identidad para las filas nuevas que se añadan.  
  
 Las columnas de identidad se utilizan normalmente junto con restricciones PRIMARY KEY para que actúen como identificador exclusivo de fila para la tabla. La propiedad IDENTITY se puede asignar a un **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)**, o **numeric(p,0)** columna. Solo se puede crear una columna de identidad para cada tabla. La palabra clave DEFAULT y los valores predeterminados enlazados no se pueden utilizar con una columna de identidad. En este caso, debe especificarse tanto el valor de inicialización como el incremento o ninguno. Si se especifica ninguno, el valor predeterminado es (1,1).  
  
> [!NOTE]  
>  No puede modificar una columna de tabla existente para agregar la propiedad IDENTITY.  
  
 No se permite agregar una columna de identidad a una tabla publicada, puesto que esta operación puede dar lugar a una falta de convergencia cuando la columna se replica en el suscriptor. Los valores de la columna de identidad en el publicador dependen del orden en que se almacenen físicamente las filas de la tabla afectada. Las filas se pueden almacenar de forma diferente en el suscriptor; por lo tanto, el valor de la columna de identidad puede ser distinto para las mismas filas.  
  
 Para deshabilitar la propiedad IDENTITY de una columna al permitir que los valores que se pueden insertar de forma explícita, use [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md).  
  
*valor de inicialización*  
 Es el valor que se utiliza para la primera fila cargada en la tabla.  
  
*incremento*  
 Es el valor incremental que se agrega al valor de identidad de la fila cargada anteriormente.  
  
NOT FOR REPLICATION  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se puede especificar para la propiedad IDENTITY. Si se especifica esta cláusula para la propiedad IDENTITY, los valores de las columnas de identidad no aumentan cuando los agentes de replicación realizan operaciones de inserción.  
  
ROWGUIDCOL  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que la columna es una columna de identificador único global de la fila. ROWGUIDCOL solo puede asignarse a un **uniqueidentifier** columna y solo uno **uniqueidentifier** se puede designar la columna por tabla como columna ROWGUIDCOL. ROWGUIDCOL no se puede asignar a columnas con tipos de datos definidos por el usuario.  
  
 ROWGUIDCOL no impone la unicidad de los valores almacenados en la columna. Asimismo, tampoco genera automáticamente valores para nuevas filas que se insertan en la tabla. Para generar valores únicos para cada columna, utilice la función NEWID en instrucciones INSERT o especifique la función NEWID como la predeterminada para la columna. Para obtener más información, vea [NEWID &#40; Transact-SQL &#41; ](../../t-sql/functions/newid-transact-sql.md)y [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
SPARSE  
 Indica que la columna es una columna dispersa. El almacenamiento de columnas dispersas está optimizado para los valores NULL. Las columnas dispersas no se pueden designar como NOT NULL. Para obtener más información sobre las columnas dispersas y restricciones adicionales, consulte [usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).  
  
\<column_constraint >  
 Las definiciones de los argumentos de restricción de columna, vea [column_constraint &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-column-constraint-transact-sql.md).  
  
 CIFRADO CON  
 Especifica el cifrado de columnas mediante la [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) característica.  
  
 COLUMN_ENCRYPTION_KEY = *key_name*  
 Especifica la clave de cifrado de columna. Para obtener más información, vea [CREATE COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
ENCRYPTION_TYPE = {DETERMINISTA | ALEATORIO}  
 El**cifrado determinista** usa un método que genera siempre el mismo valor cifrado para cualquier valor de texto no cifrado concreto. Uso del cifrado determinista permite búsquedas mediante la comparación de igualdad, agrupación y la unión de tablas con combinaciones de igualdad en función de los valores cifrados, pero también puede permitir que los usuarios no autorizados averigüen la información acerca de los valores cifrados examinando los patrones en la columna cifrada. Combina dos tablas en columnas cifradas de manera determinista sólo es posible si ambas columnas se cifran con la misma clave de cifrado de columna. El cifrado determinista debe usar una intercalación de columna con un criterio de ordenación binario 2 para columnas de caracteres.  
  
 El**cifrado aleatorio** utiliza un método que cifra los datos de una manera menos predecible. El cifrado aleatorio es más seguro, pero impide las búsquedas de igualdad, agrupación y la unión en columnas cifradas. No se pueden indizar las columnas que se usa el cifrado aleatorio.  
  
 Utilice el cifrado determinista para las columnas que va a ser parámetros de búsqueda o parámetros de agrupación, por ejemplo un número de identificación de gobierno. Utilice el cifrado aleatorio, para los datos como un número de tarjeta de crédito, que no es agrupado con otros registros, ni se usa para combinar tablas y no que se busca como utilizar otras columnas (por ejemplo, un número de transacciones) para buscar la fila que contiene el cifrado columna de interés.  
  
 Columnas deben ser aplicables al tipo de datos.  
  
ALGORITMO  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
Debe ser **'AEAD_AES_256_CBC_HMAC_SHA_256'**.  
  
 Para obtener más información, incluidas las restricciones de característica, vea [Always Encrypted &#40; motor de base de datos &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
   
Agregar enmascarada con (función = ' *mask_function* ')  
 **Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica una máscara dinámica de datos. *mask_function* es el nombre de la función de enmascaramiento con los parámetros adecuados. Las funciones siguientes están disponibles:  
  
-   es default()  
  
-   Email()  
  
-   Partial()  
  
-   Random()  
  
 Para los parámetros de función, vea [Dynamic Data Masking](../../relational-databases/security/dynamic-data-masking.md).  
  
## <a name="remarks"></a>Comentarios  
 Si se agrega una columna con un **uniqueidentifier** tipo de datos, se puede definir con un valor predeterminado que usa la función NEWID() para proporcionar los valores de identificador único de la nueva columna para cada fila existente en la tabla.  
  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no aplica un orden para especificar DEFAULT, IDENTITY, ROWGUIDCOL o las restricciones de columna en una definición de columna.  
  
 La instrucción ALTER TABLE generará un error si la adición de la columna hace que el tamaño de las filas de datos supere los 8060 bytes.  
  
## <a name="examples"></a>Ejemplos  
 Para obtener ejemplos, vea [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  

