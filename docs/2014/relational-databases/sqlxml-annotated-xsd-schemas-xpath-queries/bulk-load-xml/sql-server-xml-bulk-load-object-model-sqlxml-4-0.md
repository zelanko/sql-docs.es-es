---
title: Modelo de objeto para la carga de forma masiva SQL Server XML (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bb60aaf57869dbbd108c0815ed3fc02b07ed4bf5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202473"
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>Modelo de objetos de carga masiva XML de SQL Server (SQLXML 4.0)
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sqlxmlbulkload, objeto está formada por el modelo de objetos de carga masiva XML. Este objeto admite los métodos y propiedades siguientes.  
  
## <a name="methods"></a>Métodos  
 Execute  
 Realiza cargas masivas de los datos utilizando los archivos de esquema y de datos (o flujo) proporcionados como parámetros.  
  
## <a name="properties"></a>Propiedades  
 Carga masiva  
 Especifica si se debe realizar una carga masiva. Esta propiedad es útil si desea generar únicamente los esquemas (vea las propiedades SchemaGen, SGDropTables y SGUseID que van a continuación) y no pueda realizar una carga masiva. Ésta es una propiedad Boolean. Cuando la propiedad está establecida en TRUE, se ejecuta la carga masiva XML. Cuando está establecida en FALSE, no se ejecuta la carga masiva XML.  
  
 El valor predeterminado es TRUE.  
  
 CheckConstraints  
 Especifica si se deben comprobar las restricciones (como las restricciones debido a la relación de clave principal/clave externa entre las columnas) especificadas en la columna cuando la carga masiva XML inserta los datos en las columnas. Ésta es una propiedad Boolean.  
  
 Cuando la propiedad está establecida en TRUE, la carga masiva XML comprueba las restricciones para cada valor insertado (lo que significa que una infracción de restricción produce un error).  
  
> [!NOTE]  
>  Para dejar esta propiedad como FALSE, debe tener **ALTER TABLE** permisos en las tablas de destino. Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 El valor predeterminado es FALSE. Cuando está establecida en FALSE, la carga masiva XML omite las restricciones durante una operación de inserción. En la implementación actual, debe definir las tablas en el orden de relaciones de clave principal y clave externa en el esquema de asignación. Es decir, se debe definir una tabla con una clave principal antes de la tabla correspondiente con la clave externa; de lo contrario, no se podrá realizar la carga masiva XML.  
  
 Tenga en cuenta que si se realiza la propagación de identificadores, esta opción no se aplica y quedará activa la comprobación de restricciones. Esto se produce cuando `KeepIdentity=False` y hay una relación definida donde el elemento primario es un campo de identidad y se proporciona el valor al elemento secundario cuando se genera.  
  
 ConnectionCommand  
 Identifica un objeto de conexión existente (por ejemplo, el objeto de comando ADO o ICommand) que debe usar la carga masiva XML. Puede usar la propiedad ConnectionCommand en lugar de especificar una cadena de conexión con la propiedad ConnectionString. La propiedad de transacción debe establecerse en TRUE si utiliza ConnectionCommand.  
  
 Si usa propiedades tanto la cadena de conexión y ConnectionCommand, carga masiva XML usa la última propiedad especificada.  
  
 El valor predeterminado es NULL.  
  
 ConnectionString  
 Identifica la cadena de conexión OLE DB que proporciona la información necesaria para establecer una conexión a una instancia de la base de datos. Si usa propiedades tanto la cadena de conexión y ConnectionCommand, carga masiva XML usa la última propiedad especificada.  
  
 El valor predeterminado es NULL.  
  
 ErrorLogFile  
 Especifica el nombre de archivo en el que la carga masiva XML registra errores y mensajes. El valor predeterminado es una cadena vacía, en cuyo caso el registro no tiene lugar.  
  
 FireTriggers  
 Especifica si los desencadenadores definidos en las tablas de destino se deben activar durante la operación de carga masiva. El valor predeterminado es FALSE.  
  
 Cuando se establece en TRUE, los desencadenadores se activan de forma normal durante las operaciones de inserción.  
  
> [!NOTE]  
>  Para dejar esta propiedad como FALSE, debe tener **ALTER TABLE** permisos en las tablas de destino. Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 Tenga en cuenta que si se realiza la propagación de identificadores, no se aplica esta opción y se quedarán activos los desencadenadores. Esto se produce cuando `KeepIdentity=False` y hay una relación definida donde el elemento primario es un campo de identidad y se proporciona el valor al elemento secundario cuando se genera.  
  
 ForceTableLock  
 Especifica si las tablas en las que la carga masiva XML copia los datos se deben bloquear el tiempo que dura la carga masiva. Ésta es una propiedad Boolean. Cuando la propiedad está establecida en TRUE, la carga masiva XML adquiere los bloqueos de la tabla el tiempo que dura la carga masiva. Cuando está establecida en FALSE, la carga masiva XML adquiere un bloqueo de la tabla cada vez que inserta un registro en una tabla.  
  
 El valor predeterminado es FALSE.  
  
 IgnoreDuplicateKeys  
 Especifica qué hacer si se intenta insertar valores duplicados en una columna de clave. Si esta propiedad está establecida en TRUE y se intenta insertar un registro con un valor duplicado en una columna de clave, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no inserta ese registro. Pero inserta el registro subsiguiente; así, no se produce un error en la operación de carga masiva. Si esta propiedad está establecida en FALSE, se produce un error en la carga masiva cuando se intenta insertar un valor duplicado en una columna de clave.  
  
 Cuando la propiedad IgnoreDuplicateKeys se establece en TRUE, se emite una instrucción COMMIT para cada registro insertado en la tabla. Esto ralentiza el rendimiento. La propiedad puede establecerse en TRUE solo cuando la propiedad de transacción se establece en FALSE, porque el comportamiento transaccional se implementa utilizando los archivos.  
  
 El valor predeterminado es FALSE.  
  
 KeepIdentity  
 Especifica cómo solucionar los valores de una columna de tipo Identity del archivo de código fuente. Ésta es una propiedad Boolean. Cuando la propiedad está establecida en TRUE, la carga masiva XML asigna los valores especificados en el archivo de código fuente a la columna de identidad. Cuando la propiedad está establecida en FALSE, la operación de carga masiva omite los valores de columna de identidad especificados en el código fuente. En este caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asigna un valor a la columna de identidad.  
  
 Si la carga masiva implica una columna que es una clave externa que hace referencia a una columna de identidad en la que se almacenan los valores generados por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la carga masiva propaga adecuadamente estos valores de identidad a la columna de clave externa.  
  
 El valor de esta propiedad se aplica a todas las columnas implicadas en la carga masiva. El valor predeterminado es TRUE.  
  
> [!NOTE]  
>  Para dejar esta propiedad como TRUE, debe tener **ALTER TABLE** permisos en las tablas de destino. De lo contrario, debe estar establecida en un valor de FALSE. Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 KeepNulls  
 Especifica qué valor se va a utilizar para una columna a la que le falta un atributo o elemento secundario correspondiente en el documento XML. Ésta es una propiedad Boolean. Cuando la propiedad está establecida en TRUE, la carga masiva XML asigna un valor nulo a la columna. No asigna el valor predeterminado de la columna, si existe, como está establecido en el servidor. El valor de esta propiedad se aplica a todas las columnas implicadas en la carga masiva.  
  
 El valor predeterminado es FALSE.  
  
 SchemaGen  
 Especifica si se van a crear las tablas necesarias antes de realizar una operación de carga masiva. Ésta es una propiedad Boolean. Si esta propiedad está establecida en TRUE, se crean las tablas identificadas en el esquema de asignación (debe existir la base de datos) . Si una o varias de las tablas ya existen en la base de datos, sgdroptables, propiedad determina si estas tablas preexistentes se quitará y volver a crear.  
  
 El valor predeterminado de la propiedad SchemaGen es FALSE. SchemaGen no crea restricciones PRIMARY KEY en las tablas recién creadas. SchemaGen, crear sin embargo, las restricciones FOREIGN KEY en la base de datos si puede encontrar coincidencia `sql:relationship` y `sql:key-fields` anotaciones en el esquema de asignación y si el campo de clave está compuesto de una sola columna.  
  
 Tenga en cuenta que si establece la propiedad SchemaGen en TRUE, carga masiva XML hace lo siguiente:  
  
-   Crea las tablas necesarias a partir de los nombres de atributo y elemento. Por consiguiente, es importante que no utilice las palabras reservadas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para los nombres de atributo y elemento en el esquema.  
  
-   Devuelve datos del desbordamiento para las columnas designadas utilizando la [SQL: overflow-campo](annotation-interpretation-sql-overflow-field.md) en [tipo de datos xml](/sql/t-sql/xml/xml-transact-sql) formato.  
  
 SGDropTables  
 Especifica si se deben quitar las tablas existentes y volver a crearlas. Utilice esta propiedad cuando la propiedad SchemaGen está establecida en TRUE. Si SGDropTables es FALSE, se conservan las tablas existentes. Cuando esta propiedad es TRUE, se eliminan las tablas existentes y se vuelven a crear.  
  
 El valor predeterminado es FALSE.  
  
 SGUseID  
 Especifica si el atributo del esquema de asignación que se identifica como tipo `id` se puede utilizar para crear una restricción PRIMARY KEY cuando se crea la tabla. Utilice esta propiedad cuando la propiedad SchemaGen está establecida en TRUE. Si SGUseID es TRUE, la utilidad SchemaGen utiliza un atributo para el que `dt:type="id"` se especifica como columna de clave principal y agrega la restricción PRIMARY KEY adecuada al crear la tabla.  
  
 El valor predeterminado es FALSE.  
  
 TempFilePath  
 Especifica la ruta de acceso del archivo donde la carga masiva XML crea los archivos temporales para una carga masiva llevada a cabo. (Esta propiedad solo es útil cuando la propiedad Transaction está establecida en TRUE). Debe asegurarse de que la cuenta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se utiliza para la carga masiva XML tiene acceso a esta ruta. Si no se establece esta propiedad, la carga masiva XML almacena los archivos temporales en la ubicación especificada en la variable de entorno TEMP.  
  
 Transaction  
 Especifica si la carga masiva se debe hacer como una transacción, en cuyo caso se garantiza la reversión si se produce un error en la carga masiva. Ésta es una propiedad Boolean. Si la propiedad está establecida en TRUE, la carga masiva se produce en un contexto transaccional. La propiedad TempFilePath es útil solo cuando la transacción se establece en TRUE.  
  
> [!NOTE]  
>  Si va a cargar los datos binarios (como bin.hex, bin.base64 tipos de datos XML del archivo binario, de la imagen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos), la propiedad de transacción debe establecerse en FALSE.  
  
 El valor predeterminado es FALSE.  
  
 XMLFragment  
 Especifica si los datos de origen son fragmentos XML. Un fragmento XML es un documento XML sin un elemento de nivel superior (raíz) único. Ésta es una propiedad Boolean. Esta propiedad debe estar establecida en TRUE si el archivo de código fuente está compuesto de un fragmento XML.  
  
 El valor predeterminado es FALSE.  
  
  
