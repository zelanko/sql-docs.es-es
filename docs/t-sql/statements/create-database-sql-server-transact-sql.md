---
title: CREATE DATABASE (SQL Server Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE_TSQL
- DATABASE
- CONTAINMENT_TSQL
- CREATE DATABASE
- CREATE_DATABASE_TSQL
- CONTAINS_FILESTREAM_TSQL
- CONTAINS FILESTREAM
- CONTAINMENT
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], creating
- databases [SQL Server], creating
- model database [SQL Server], database creation
- mounted drives [SQL Server]
- CREATE DATABASE
- CREATE DATABASE statement
- file creation [SQL Server]
- creating databases
- containment
- filegroups [SQL Server], database creation
- database creation [SQL Server], CREATE DATABASE statement
- moving databases
- attaching databases [SQL Server], CREATE DATABASE...FOR ATTACH
ms.assetid: 29ddac46-7a0f-4151-bd94-75c1908c89f8
caps.latest.revision: 212
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 356a00b1c83220e0be211ee0357d2736533a3906
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-database-sql-server-transact-sql"></a>CREATE DATABASE (Transact-SQL de SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una nueva base de datos y los archivos que se usan para almacenar la base de datos, una instantánea de base de datos, o adjunta una base de datos a partir de los archivos separados de una base de datos creada anteriormente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  

Crear una base de datos    

```  
CREATE DATABASE database_name   
[ CONTAINMENT = { NONE | PARTIAL } ]  
[ ON   
      [ PRIMARY ] <filespec> [ ,...n ]   
      [ , <filegroup> [ ,...n ] ]   
      [ LOG ON <filespec> [ ,...n ] ]   
]   
[ COLLATE collation_name ]  
[ WITH  <option> [,...n ] ]  
[;]  
  
<option> ::=  
{  
      FILESTREAM ( <filestream_option> [,...n ] )  
    | DEFAULT_FULLTEXT_LANGUAGE = { lcid | language_name | language_alias }  
    | DEFAULT_LANGUAGE = { lcid | language_name | language_alias }  
    | NESTED_TRIGGERS = { OFF | ON }  
    | TRANSFORM_NOISE_WORDS = { OFF | ON}  
    | TWO_DIGIT_YEAR_CUTOFF = <two_digit_year_cutoff>   
    | DB_CHAINING { OFF | ON }  
    | TRUSTWORTHY { OFF | ON }  
}  
  
<filestream_option> ::=  
{  
      NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
    | DIRECTORY_NAME = 'directory_name'   
}  
  
<filespec> ::=   
{  
(  
    NAME = logical_file_name ,  
    FILENAME = { 'os_file_name' | 'filestream_path' }   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB | % ] ]  
)  
}  
  
<filegroup> ::=   
{  
FILEGROUP filegroup name [ [ CONTAINS FILESTREAM ] [ DEFAULT ] | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    <filespec> [ ,...n ]  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
}  
  
```  
 
Adjuntar una base de datos    

```  
CREATE DATABASE database_name   
    ON <filespec> [ ,...n ]   
    FOR { { ATTACH [ WITH <attach_database_option> [ , ...n ] ] }  
        | ATTACH_REBUILD_LOG }  
[;]  
  
<attach_database_option> ::=  
{  
      <service_broker_option>  
    | RESTRICTED_USER  
    | FILESTREAM ( DIRECTORY_NAME = { 'directory_name' | NULL } )  
}   
```  
  
Crear una instantánea de base de datos    

```  
CREATE DATABASE database_snapshot_name   
    ON   
    (  
        NAME = logical_file_name,  
        FILENAME = 'os_file_name'   
    ) [ ,...n ]   
    AS SNAPSHOT OF source_database_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la nueva base de datos. Los nombres de base de datos deben ser únicos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *database_name* puede tener 128 caracteres como máximo, a menos que no se especifique un nombre lógico para el archivo de registro. Si no se especifica un nombre de archivo de registro lógico, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera *logical_file_name* y *os_file_name* para el registro, anexando un sufijo a *database_name*. Esto limita *database_name* a 123 caracteres, por lo que el nombre de archivo lógico generado tiene como máximo 128 caracteres.  
  
 Si no se especifica el nombre de archivo de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza *database_name* como el *logical_file_name* y como *os_file_name*. La ruta de acceso predeterminada se obtiene del Registro. La ruta de acceso predeterminada se puede cambiar utilizando las **Propiedades del servidor (página de configuración de base de datos)** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para cambiar la ruta de acceso predeterminada se requiere reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 CONTAINMENT = { NONE | PARTIAL }  

**Se aplica a**: de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica el estado de contención de la base de datos. NONE = base de datos dependiente. PARTIAL = base de datos parcialmente independiente.  
  
 ON  
 Especifica que los archivos de disco utilizados para almacenar las secciones de datos de la base de datos (archivos de datos) se definen explícitamente. ON es obligatorio cuando va seguido de una lista de elementos \<filespec> separados por comas que definen los archivos de datos del grupo de archivos principal. Detrás de la lista de archivos del grupo de archivos principal se puede colocar una lista opcional de elementos \<filegroup> separados por comas que definan los grupos de archivos de usuario y sus archivos.  
  
 PRIMARY  
 Especifica que la lista de elementos \<filespec> asociada define el archivo principal. El primer archivo especificado en la entrada \<filespec> del grupo de archivos principal se convierte en el archivo principal. Una base de datos solo puede tener un archivo principal. Para más información, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 Si no se especifica PRIMARY, el primer archivo enumerado en la instrucción CREATE DATABASE se convierte en el archivo principal.  
  
 LOG ON  
 Especifica que los archivos de disco utilizados para almacenar el registro de la base de datos (archivos de registro) se definen explícitamente. LOG ON va seguido de una lista de elementos \<filespec> separados por comas que definen los archivos de registro. Si no se especifica LOG ON, se crea automáticamente un archivo de registro cuyo tamaño es el 25 % de la suma de los tamaños de todos los archivos de datos de la base de datos o 512 KB, el valor que sea mayor. Este archivo se coloca en la ubicación del archivo de registro predeterminado. Para obtener más información sobre esta ubicación, consulte [Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
 LOG ON no se puede especificar en una instantánea de base de datos.  
  
 COLLATE *collation_name*  
 Especifica la intercalación predeterminada de la base de datos. El nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Si no se especifica, se asigna a la base de datos la intercalación predeterminada de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No se puede especificar un nombre de intercalación en una instantánea de base de datos.  
  
 No se puede especificar un nombre de intercalación con las cláusulas FOR ATTACH o FOR ATTACH_REBUILD_LOG. Para obtener información acerca de cómo cambiar la intercalación de una base de datos adjuntada, visite este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?linkid=16419&kbid=325335).  
  
 Para obtener más información sobre los nombres de intercalación de Windows y SQL, vea [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
> [!NOTE]  
>  Las bases de datos independientes se intercalan de modo diferente al de las bases de datos dependientes. Para obtener más información, consulte [Intercalaciones de bases de datos independientes](../../relational-databases/databases/contained-database-collations.md).  
  
 WITH \<option>  
 -   **\<filestream_options>** 
  
     NON_TRANSACTED_ACCESS = { **OFF** | READ_ONLY | FULL }  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     Especifica el nivel de acceso no transaccional de FILESTREAM a la base de datos.  
  
    |Valor|Description|  
    |-----------|-----------------|  
    |OFF|El acceso no transaccional está deshabilitado.|  
    |READONLY|Los procesos no transaccionales pueden leer los datos de FILESTREAM en esta base de datos.|  
    |FULL|El acceso no transaccional total a objetos FileTable de FILESTREAM está habilitado.|  
  
     DIRECTORY_NAME = \<directory_name> **Se aplica**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     Un nombre de directorio compatible con Windows. Este nombre debe ser único entre todos los nombres de Database_Directory en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La comparación de unicidad no distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opción se debe establecer antes de crear un objeto FileTable en esta base de datos.  
  
 Las opciones siguientes se permiten solo cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.  
  
-   **DEFAULT_FULLTEXT_LANGUAGE = \<lcid> | \<nombre de idioma> | \<alias de idioma>**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     See [Configure the default full-text language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) for a full description of this option.  
  
-   **DEFAULT_LANGUAGE = \<lcid> | \<nombre de idioma> | \<alias de idioma>**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     See [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) for a full description of this option.  
  
-   **NESTED_TRIGGERS = { OFF | ON}**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     See [Configure the nested triggers Server Configuration Option](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) for a full description of this option.  
  
-   **TRANSFORM_NOISE_WORDS = { OFF | ON}**  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     See [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)for a full description of this option.  
  
-   **TWO_DIGIT_YEAR_CUTOFF = { 2049 | \<cualquier año entre 1753 y 9999> }**  
  
     Cuatro dígitos que representan un año. El valor predeterminado es 2049. Para obtener más información, consulte [Establecer la opción de configuración del servidor Fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).  
  
-   **DB_CHAINING { OFF | ON }**  
  
     Si se especifica ON, la base de datos puede ser el origen o destino de una cadena de propiedad entre bases de datos.  
  
     Si es OFF, la base de datos no puede participar en encadenamientos de propiedad entre bases de datos. El valor predeterminado es OFF.  
  
    > [!IMPORTANT]  
    >  La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconoce esta configuración si la opción del servidor cross db ownership chaining server es 0 (OFF). Si cross db ownership chaining es 1 (ON), todas las bases de datos de usuario pueden participar en cadenas de propiedad entre bases de datos, independientemente del valor de esta opción. Esta opción se establece mediante [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
     Para establecer esta opción, debe pertenecer al rol fijo de servidor sysadmin. La opción DB_CHAINING no se puede establecer en estas bases de datos del sistema: master, model, tempdb.  
  
-   **TRUSTWORTHY { OFF | ON }**  
  
     Cuando se especifica ON, los módulos de base de datos (por ejemplo, vistas, funciones definidas por el usuario o procedimientos almacenados) que utilicen un contexto de suplantación pueden tener acceso a recursos externos a la base de datos.  
  
     Si es OFF, los módulos de base de datos en un contexto de suplantación no pueden tener acceso a recursos externos a la base de datos. El valor predeterminado es OFF.  
  
     TRUSTWORTHY se establece en OFF siempre que la base de datos se adjunta.  
  
     De forma predeterminada, el valor TRUSTWORTHY se establece en OFF en todas las bases de datos de sistema, excepto msdb. El valor no se puede cambiar en las bases de datos model ni tempdb. Se recomienda no establecer la opción TRUSTWORTHY en ON en la base de datos maestra.  
  
     Para establecer esta opción, debe pertenecer al rol fijo de servidor sysadmin.  
  
 FOR ATTACH [ WITH \< attach_database_option > ] Especifica que la base de datos se crea [adjuntando](../../relational-databases/databases/database-detach-and-attach-sql-server.md) un conjunto existente de archivos del sistema operativo. Debe haber una entrada \<filespec> que especifique el archivo principal. Las demás entradas \<filespec> que son necesarias son las correspondientes a los archivos con una ruta de acceso diferente de la que tenían cuando la base de datos se creó por primera vez o se adjuntó por última vez. Debe especificarse una entrada \<filespec> para estos archivos.  
  
 FOR ATTACH tiene los siguientes requisitos:  
  
-   Todos los archivos de datos (MDF y NDF) deben estar disponibles.  
  
-   Si hay varios archivos de registro, todos ellos deben estar disponibles.  
  
 Si una base de datos de lectura/escritura tiene un único archivo de registro que no está disponible actualmente y si la base de datos se cerró sin usuarios o transacciones abiertas antes de la operación de adjuntar, FOR ATTACH regenera automáticamente el archivo de registro y actualiza el archivo principal. En cambio, en el caso de una base de datos de solo lectura, el registro no se puede volver a generar porque el archivo principal no se puede actualizar. Por lo tanto, cuando se adjunta una base de datos de solo lectura con un registro que no está disponible, se deben proporcionar los archivos de registro o los archivos de la cláusula FOR ATTACH.  
  
> [!NOTE]  
>  Una base de datos creada por una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede adjuntarse en versiones anteriores.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los archivos de texto completo que formen parte de la base de datos que se va a adjuntar se adjuntarán con la base de datos. Para especificar una nueva ruta de acceso al catálogo de texto completo, escriba la nueva ubicación sin incluir el nombre de archivo de texto completo del sistema operativo. Para obtener más información, vea la sección Ejemplos.  
  
 Si se adjunta una base de datos que contiene una opción FILESTREAM de "Nombre de directorio" en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se solicitará a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que compruebe que el nombre de Database_Directory es único. Si no lo es, la operación de adjuntar sufrirá un error con el mensaje "El nombre de FILESTREAM Database_Directory \<nombre> no es único en esta instancia de SQL Server". Para evitar este error, se debe pasar a esta operación el parámetro opcional *directory_name*.  
  
 FOR ATTACH no se puede especificar en una instantánea de base de datos.  
  
 FOR ATTACH puede especificar la opción RESTRICTED_USER. RESTRICTED_USER permite que solamente se conecten a la base de datos los miembros del rol fijo de base de datos db_owner y de los roles fijos de servidor dbcreator y sysadmin, aunque no limita su número. Los intentos de los usuarios no calificados se rechazarán.  
  
 Si la base de datos usa [!INCLUDE[ssSB](../../includes/sssb-md.md)], emplee WITH \<service_broker_option> en la cláusula FOR ATTACH: 
  
 \<service_broker_option> Controla la entrega de mensajes de [!INCLUDE[ssSB](../../includes/sssb-md.md)] y el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] para la base de datos. Las opciones de [!INCLUDE[ssSB](../../includes/sssb-md.md)] solo se pueden especificar cuando se usa la cláusula FOR ATTACH.  
  
 ENABLE_BROKER  
 Indica que se habilite [!INCLUDE[ssSB](../../includes/sssb-md.md)] para la base de datos especificada. En otras palabras, se inicia la entrega de mensajes y se establece is_broker_enabled en True en la vista de catálogo sys.databases. La base de datos conserva el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.  
  
 NEW_BROKER  
 Crea un valor service_broker_guid en sys.databases y en la base de datos restaurada y finaliza todos los extremos de conversación con limpieza. El agente se habilita, pero no se envía ningún mensaje a los extremos de conversación remotos. Cualquier ruta que haga referencia al identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] anterior se debe volver a crear con el nuevo identificador.  
  
 ERROR_BROKER_CONVERSATIONS  
 Finaliza todas las conversaciones con un error que indica que la base de datos está adjunta o restaurada. El agente está deshabilitado hasta que finaliza esta operación y, después, se habilita. La base de datos conserva el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.  
  
 Si adjunta una base de datos replicada que fue copiada en lugar de ser separada, tenga en cuenta lo siguiente:  
  
-   Si adjunta la base de datos a la misma versión e instancia de servidor que la base de datos original, no es necesario realizar ningún paso adicional.  
  
-   Si adjunta la base de datos a la misma instancia de servidor pero con una versión actualizada, debe ejecutar [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) para actualizar la replicación una vez que se complete la operación de adjuntar.  
  
-   Si adjunta la base de datos a una instancia de servidor diferente, independientemente de la versión, debe ejecutar [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para quitar la replicación una vez que se complete la operación de adjuntar.  
  
> [!NOTE]  
> Adjunte los trabajos con el formato de almacenamiento **vardecimal**, pero el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se debe actualizar al menos a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2. No puede adjuntar ninguna base de datos que use el formato de almacenamiento vardecimal a una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre el formato de almacenamiento **vardecimal**, consulte [Compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
 La primera vez que se adjunta una base de datos o se restaura en una instancia nueva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aún no se ha almacenado una copia de la clave maestra de la base de datos (cifrada por la clave maestra de servicio) en el servidor. Debe usar la instrucción **OPEN MASTER KEY** para descifrar la clave maestra de la base de datos (DMK). Una vez que se ha descifrado la clave maestra de la base de datos, tiene la posibilidad de habilitar el descifrado automático en el futuro usando la instrucción **ALTER MASTER KEY REGENERATE** para proporcionar al servidor una copia de la clave maestra de la base de datos cifrada con la clave maestra de servicio (SMK). Cuando una base de datos se haya actualizado desde una versión anterior, se debe volver a generar la DMK para usar el algoritmo AES más reciente. Para obtener más información sobre cómo volver a generar la DMK, vea [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). El tiempo necesario para volver a generar la DMK con el fin de actualizarse a AES depende del número de objetos protegidos por la DMK. Solo es necesario volver a generar la DMK una vez y no tiene ningún efecto sobre las nuevas generaciones futuras como parte de una estrategia de rotación de claves. Para obtener información sobre cómo actualizar una base de datos mediante el uso de adjuntar, vea [Actualizar una base de datos mediante Separar y Adjuntar &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md).  
  
> [!IMPORTANT]  
> Se recomienda no adjuntar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos.  
  
> [!NOTE]  
> Las opciones **TRUSTWORTHY** y **DB_CHAINING** no tienen ningún efecto cuando se adjunta una base de datos.  
  
 FOR ATTACH_REBUILD_LOG  
 Especifica que la base de datos se crea adjuntando un conjunto existente de archivos del sistema operativo. Esta opción está limitada a las bases de datos de lectura y escritura. Debe haber una entrada *\<filespec>* que especifique el archivo principal. Si no se encuentran uno o varios archivos de registro de transacciones, se volverá a generar el archivo de registro. ATTACH_REBUILD_LOG crea automáticamente un nuevo archivo de registro de 1 MB. Este archivo se coloca en la ubicación del archivo de registro predeterminado. Para obtener más información sobre esta ubicación, consulte [Ver o cambiar las ubicaciones predeterminadas de los archivos de datos y registro &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
> [!NOTE]  
>  Si los archivos de registro están disponibles, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] utiliza esos archivos en lugar de volver a generar los archivos de registro.  
  
 FOR ATTACH_REBUILD_LOG requiere lo siguiente:  
  
-   Un cierre limpio de la base de datos.  
  
-   Todos los archivos de datos (MDF y NDF) deben estar disponibles.  
  
> [!IMPORTANT]  
> Esta operación interrumpe la cadena de copias de seguridad de registros. Se recomienda realizar una copia de seguridad completa de la base de datos después de finalizar la operación. Para obtener más información, vea [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
 Normalmente, FOR ATTACH_REBUILD_LOG se utiliza cuando se copia una base de datos de lectura/escritura con un registro grande en otro servidor donde la copia se va a utilizar mayoritariamente, o únicamente, para operaciones de lectura y, por lo tanto, requiere menos espacio de registro que la base de datos original.  
  
 FOR ATTACH_REBUILD_LOG no se puede especificar en una instantánea de base de datos.  
  
 Para obtener más información sobre cómo se adjuntan y separan las bases de datos, vea [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
 \<filespec>  
 Controla las propiedades de archivo.  
  
 NAME *logical_file_name*  
 Especifica un nombre lógico para el archivo. NAME es obligatorio si se especifica FILENAME, excepto cuando se especifica una de las cláusulas FOR ATTACH. Un grupo de archivos FILESTREAM no se puede denominar PRIMARY.  
  
 *logical_file_name*  
 Es el nombre lógico utilizado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se hace referencia al archivo. *Logical_file_name* debe ser único en la base de datos y debe cumplir las mismas reglas que los [identificadores](../../relational-databases/databases/database-identifiers.md). El nombre puede ser una constante de caracteres o Unicode, o un identificador regular o delimitado.  
  
 FILENAME { **'***os_file_name***'** | **'***filestream_path***'** }  
 Especifica el nombre de archivo (físico) del sistema operativo.  
  
 **'** *os_file_name* **'**  
 Es la ruta de acceso y el nombre de archivo que el sistema operativo utiliza cuando se crea el archivo. El archivo debe residir en uno de los siguientes dispositivos: el servidor local en el que se ha instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], una red de área de almacenamiento (SAN) o una red basada en iSCSI. La ruta de acceso especificada debe existir antes de ejecutar la instrucción CREATE DATABASE. Para obtener más información, vea "Archivos y grupos de archivos de base de datos" en la sección Comentarios.  
  
 Los parámetros SIZE, MAXSIZE y FILEGROWTH se pueden establecer si se ha especificado una ruta UNC para el archivo.  
  
 Si el archivo se encuentra en una partición sin formato, *os_file_name* solo debe indicar la letra de unidad de una partición sin formato existente. Solo se puede crear un archivo de datos en cada partición sin procesar.  
  
 Los archivos de datos no deben guardarse en sistemas de archivo comprimidos a menos que se trate de archivos secundarios de solo lectura o que la base de datos sea de solo lectura. Los archivos de registro no se deben almacenar en sistemas de archivos comprimidos.  
  
 **'** *filestream_path* **'**  
 Para un grupo de archivos FILESTREAM, FILENAME hace referencia a la ruta de acceso donde se almacenarán los datos FILESTREAM. La ruta de acceso hasta la última carpeta debe existir y la última carpeta no debe existir. Por ejemplo, si especifica la ruta de acceso C:\MyFiles\MyFilestreamData, C:\MyFiles debe existir antes de ejecutar ALTER DATABASE, pero la carpeta MyFilestreamData no debe existir.  
  
 El grupo de archivos y el archivo (`<filespec>`) se deben crear en la misma instrucción.  
  
 Las propiedades SIZE y FILEGROWTH no se aplican a un grupo de archivos FILESTREAM.  
  
 SIZE *size*  
 Especifica el tamaño del archivo.  
  
 SIZE no se puede especificar si se especifica *os_file_name* como ruta UNC. SIZE no se aplica a un grupo de archivos FILESTREAM.  
  
 *size*  
 Es el tamaño inicial del archivo.  
  
 Cuando no se suministra *size* para el archivo principal, [!INCLUDE[ssDE](../../includes/ssde-md.md)] utiliza el tamaño del archivo principal de la base de datos modelo. El tamaño predeterminado del modelo es de 8 MB (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) o 1 MB (para versiones anteriores). Cuando se especifica un archivo de datos secundario o un archivo de registro, pero no se especifica *size* para el archivo, [!INCLUDE[ssDE](../../includes/ssde-md.md)] hace que el tamaño del archivo sea de 8 MB (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) o 1 MB (para versiones anteriores). El tamaño especificado para el archivo principal debe tener al menos el tamaño del archivo principal de la base de datos model.  
  
 Se pueden utilizar los sufijos kilobyte (KB), megabyte (MB), gigabyte (GB) o terabyte (TB). El valor predeterminado es MB. Especifique un número entero; no incluya decimales. *Size* es un valor entero. Para valores mayores que 2147483647, utilice unidades más grandes.  
  
 MAXSIZE *max_size*  
 Especifica el tamaño máximo que puede alcanzar el archivo. MAXSIZE no se puede especificar si se especifica *os_file_name* como ruta UNC.  
  
 *max_size*  
 Es el tamaño máximo del archivo. Se pueden utilizar los sufijos KB, MB, GB y TB. El valor predeterminado es MB. Especifique un número entero; no incluya decimales. Si no se especifica *max_size*, el archivo aumenta de tamaño hasta que el disco esté lleno. *Max_size* es un valor entero. Para valores mayores que 2147483647, utilice unidades más grandes.  
  
 UNLIMITED  
 Especifica que el archivo crecerá hasta que el disco esté lleno. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si se especifica un crecimiento ilimitado para un archivo de registro, su tamaño máximo será de 2 TB, y para un archivo de datos será de 16 TB.  
  
> [!NOTE]  
> No hay un tamaño máximo cuando esta opción se especifica para un contenedor de FILESTREAM. Continúa creciendo hasta que el disco se completa.  
  
 FILEGROWTH *growth_increment*  
 Especifica el incremento de crecimiento automático del archivo. El valor FILEGROWTH de un archivo no puede superar el valor MAXSIZE. FILEGROWTH no se puede especificar si se especifica *os_file_name* como ruta UNC. FILEGROWTH no se aplica a un grupo de archivos FILESTREAM.  
  
 *growth_increment*  
 Es la cantidad de espacio que se agrega al archivo siempre que se necesita más espacio.  
  
 El valor se puede especificar en MB, KB, GB, TB o como porcentaje (%). Si se especifica un número sin los sufijos MB, KB o %, el valor predeterminado es MB. Cuando se especifica %, el incremento de crecimiento es el porcentaje especificado del tamaño del archivo en el momento en que tiene lugar el incremento. El tamaño especificado se redondea al múltiplo de 64 KB más cercano y el valor mínimo es 64 KB.  
  
 El valor 0 indica que el crecimiento automático está desactivado y no se permite más espacio.  
  
 Si no se especifica FILEGROWTH, los valores predeterminados son:  
  
|Versión|Valores predeterminados|  
|-------------|--------------------|  
|A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Datos: 64 MB. Archivos de registro: 64 MB.|  
|A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Datos: 1 MB. Archivos de registro: 10 %.|  
|Antes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Datos: 10 %. Archivos de registro: 10 %.|  
  
 \<filegroup>  
 Controla las propiedades del grupo de archivos. Filegroup no se puede especificar en una instantánea de base de datos.  
  
 FILEGROUP *filegroup_name*  
 Es el nombre lógico del grupo de archivos.  
  
 *filegroup_name*  
 *filegroup_name* debe ser único en la base de datos y no puede ser los nombres PRIMARY ni PRIMARY_LOG suministrados por el sistema. El nombre puede ser una constante de caracteres o Unicode, o un identificador regular o delimitado. El nombre debe cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 CONTAINS FILESTREAM  
 Especifica que el grupo de archivos almacena objetos binarios grandes (BLOB) de FILESTREAM en el sistema de archivos.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**Se aplica a**: de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica que el grupo de archivos almacena los datos memory_optimized en el sistema de archivos. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Solo se admite un grupo de archivos MEMORY_OPTIMIZED_DATA por cada base de datos. Para que los ejemplos de código que crean un grupo de archivos almacenen datos optimizados para memoria, consulte [Crear una tabla con optimización para memoria y un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
 DEFAULT  
 Especifica que el grupo de archivos indicado es el grupo de archivos predeterminado de la base de datos.  
  
 *database_snapshot_name*  
 Es el nombre de la nueva instantánea de base de datos. Los nombres de instantánea de base de datos deben ser únicos dentro de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cumplir las reglas de los identificadores. *database_snapshot_name* puede tener un máximo de 128 caracteres.  
  
 ON **(** NAME **=***logical_file_name***,** FILENAME **='***os_file_name***')** [ **,**... *n* ]  
 Para la creación de una instantánea de base de datos, especifica una lista de archivos de la base de datos de origen. Para que la instantánea funcione, todos los archivos de datos deben especificarse individualmente. Sin embargo, no se permiten archivos de registro para las instantáneas de base de datos. Los grupos de archivos FILESTREAM no son compatibles con instantáneas de base de datos. Si se incluye un archivo de datos FILESTREAM en una cláusula CREATE DATABASE ON, se producirá un error en la instrucción y se generará el mensaje correspondiente.  
  
 Para obtener las descripciones de NAME y FILENAME y sus valores, vea las descripciones de los valores equivalentes de \<filespec>.  
  
> [!NOTE]  
> Cuando se crea una instantánea de base de datos, no se admiten las demás opciones de \<filespec> ni la palabra clave PRIMARY.  
  
 AS SNAPSHOT OF *nombre_de_base_de_datos_de_origen*  
 Indica que la base de datos que se va a crear es una instantánea de base de datos de origen especificada en *source_database_name*. La instantánea y la base de datos de origen deben estar en la misma instancia.  
  
 Para obtener más información, vea "Instantáneas de base de datos" en la sección Comentarios.  
  
## <a name="remarks"></a>Notas  
 Cada vez que se crea, modifica o quita una base de datos de usuario, se debe hacer una copia de seguridad de la [base de datos maestra](../../relational-databases/databases/master-database.md).  
  
 La instrucción CREATE DATABASE debe ejecutarse en modo de confirmación automática (el modo predeterminado de administración de transacciones) y no se permite en una transacción explícita o implícita.  
  
 Se puede usar una instrucción CREATE DATABASE para crear una base de datos y los archivos donde se almacena. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa la instrucción CREATE DATABASE de la siguiente manera:  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza una copia de la [base de datos modelo](../../relational-databases/databases/model-database.md) para inicializar la base de datos y sus metadatos.  
  
2.  Se asigna un GUID de Service Broker a la base de datos.  
  
3.  A continuación, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] rellena el resto de la base de datos con páginas vacías, excepto las páginas que tengan datos internos que registren cómo se emplea el espacio en la base de datos.  
  
 En una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se pueden especificar 32.767 bases de datos como máximo.  
  
 Cada base de datos tiene un propietario que puede realizar actividades especiales en ella. El propietario es el usuario que crea la base de datos. El propietario de la base de datos se puede cambiar utilizando [sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md).  

Algunas características de la base de datos dependen de características o capacidades que están en el sistema de archivos para que la base de datos funcione completamente. Estos son algunos ejemplos de características que dependen de un conjunto de características del sistema de archivos:
- DBCC CHECKDB
- Secuencia de archivos
- Copias de seguridad en línea con VSS e instantáneas de archivos
- Creación de instantáneas de bases de datos
- Grupo de archivos de datos optimizados para memoria
   
## <a name="database-files-and-filegroups"></a>Archivos y grupos de archivos de base de datos  
 Todas las bases de datos tienen al menos dos archivos (un *archivo principal* y un *archivo de registro de transacciones*) y un grupo de archivos como mínimo. Para cada base de datos pueden especificarse hasta 32.767 archivos y 32.767 grupos de archivos.  
  
 Cuando cree una base de datos, defina el mayor tamaño posible para los archivos de datos según la cantidad de datos máxima prevista para la base datos.  
  
 Se recomienda usar una red de área de almacenamiento (SAN), una red basada en iSCSI o un disco conectado localmente para almacenar los archivos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], porque esta configuración optimiza el rendimiento y la confiabilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="database-snapshots"></a>Instantáneas de base de datos  
 Se puede utilizar la instrucción CREATE DATABASE para crear una vista estática de solo lectura, es decir, una *instantánea de base de datos* de la *base de datos de origen*. Desde el punto de vista transaccional, una instantánea de base de datos es coherente con la base de datos de origen tal como se encontraba en el momento de crear la instantánea. Una base de datos de origen puede tener varias instantáneas.  
  
> [!NOTE]  
> Cuando se crea una instantánea de base de datos, la instrucción CREATE DATABASE no puede hacer referencia a archivos de registro, archivos sin conexión, archivos de restauración ni archivos inactivos.  
  
 Si se produce un error al crear una instantánea de base de datos, se sospecha de la instantánea y debe eliminarse. Para obtener más información, vea [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Las instantáneas se conservan hasta que se eliminan mediante DROP DATABASE.  
  
 Para más información, vea [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="database-options"></a>Opciones de base de datos  
 Cuando se crea una base de datos, se establecen automáticamente varias opciones de base de datos. Para obtener una lista de estas opciones, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="the-model-database-and-creating-new-databases"></a>Base de datos modelo y creación de nuevas bases de datos  
 Todos los objetos definidos por el usuario en la [base de datos modelo](../../relational-databases/databases/model-database.md) se copiarán en todas las bases de datos recién creadas. Puede agregar a la base de datos model todos los objetos (tablas, vistas, procedimientos almacenados, tipos de datos, etc.) que desee incluir en todas las bases de datos creadas recientemente.  
  
 Cuando se especifica una instrucción CREATE DATABASE *database_name* sin parámetros de tamaño adicionales, el archivo de datos principal pasa a tener el mismo tamaño que el archivo principal de la base de datos model.  
  
 A menos que se especifique FOR ATTACH, todas las bases de datos nuevas heredan los valores de las opciones de la base de datos model. Por ejemplo, la opción de base de datos de reducción automática se establece en **true** en la base de datos model y en cualquier base de datos nueva que se cree. Si se cambian las opciones de la base de datos model, los nuevos valores de estas opciones se utilizarán en las nuevas bases de datos que se creen. Las operaciones de modificación de la base de datos model no afectan a las bases de datos existentes. Si se especifica FOR ATTACH en la instrucción CREATE DATABASE, la nueva base de datos hereda los valores de las opciones de la base de datos original.  
  
## <a name="viewing-database-information"></a>Ver la información de la base de datos  
 Se pueden utilizar vistas de catálogo, funciones del sistema y procedimientos almacenados del sistema para devolver información sobre bases de datos, archivos y grupos de archivos. Para obtener más información, vea [Vistas del sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CREATE DATABASE, CREATE ANY DATABASE o ALTER ANY DATABASE.  
  
 Para mantener el control del uso del disco en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el permiso para crear bases de datos suele limitarse a un número reducido de cuentas de inicio de sesión.  
  
 En el ejemplo siguiente se proporciona el permiso para crear una base de datos al usuario de base de datos Fay.  
  
```sql  
USE master;  
GO  
GRANT CREATE DATABASE TO [Fay];  
GO  
```  
  
### <a name="permissions-on-data-and-log-files"></a>Permisos en archivos de datos y de registro  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], algunos permisos se establecen en los archivos de datos y de registro de cada base de datos. Siempre que se realizan las operaciones siguientes en una base de datos, se establecen estos permisos:  
  
|||  
|-|-|  
|Creado|Modificada para agregar un nuevo archivo|  
|Adjuntada|Realización de copia de seguridad|  
|Separada|Restaurada|  
  
 Los permisos evitan que los archivos se modifiquen accidentalmente si residen en un directorio sin restricción de permisos.  
  
> [!NOTE]  
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] no establece permisos en archivos de datos y de registro.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-database-without-specifying-files"></a>A. Crear una base de datos sin especificar archivos  
 En este ejemplo se crea la base de datos `mytest`, y los archivos principal y de registro de transacciones correspondientes. Debido a que la instrucción no tiene elementos \<filespec>, el archivo de la base de datos principal tiene el tamaño del archivo principal de la base de datos model. El registro de transacciones se establece en el mayor de estos valores: 512 KB o el 25 % del tamaño del archivo de datos principal. Como no se ha especificado MAXSIZE, los archivos pueden crecer hasta llenar todo el espacio disponible en el disco. En este ejemplo también se muestra la forma de quitar la base de datos denominada `mytest` si existe, antes de crear la base de datos `mytest`.  
  
```sql  
USE master;  
GO  
IF DB_ID (N'mytest') IS NOT NULL
DROP DATABASE mytest;
GO
CREATE DATABASE mytest;  
GO  
-- Verify the database files and sizes  
SELECT name, size, size*1.0/128 AS [Size in MBs]   
FROM sys.master_files  
WHERE name = N'mytest';  
GO  
```  
  
### <a name="b-creating-a-database-that-specifies-the-data-and-transaction-log-files"></a>B. Crear una base de datos que especifica los archivos de datos y de registro de transacciones  
 En el ejemplo siguiente se crea la base de datos `Sales`. Debido a que no se usa la palabra clave PRIMARY, el primer archivo (`Sales_dat`) se convierte en el principal. Como no se especifica MB ni KB en el parámetro SIZE del archivo `Sales_dat` , se utiliza MB y el tamaño se asigna en megabytes. Cada vez que se crea, modifica o quita una base de datos de usuario, se debe hacer una copia de seguridad de la base de datos `Sales_log` se asigna en megabytes porque el sufijo `MB` se ha indicado explícitamente en el parámetro `SIZE` .  
  
```sql  
USE master;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>C. Crear una base de datos especificando múltiples archivos de datos y de registro de transacciones  
 En el ejemplo siguiente se crea la base de datos `Archive`, que tiene tres archivos de datos de `100-MB` y dos archivos de registro de transacciones de `100-MB`. El archivo principal es el primer archivo de la lista y se especifica explícitamente con la palabra clave `PRIMARY`. Los archivos de registro de transacciones se especifican a continuación de las palabras clave `LOG ON`. Tenga en cuenta las extensiones usadas para los archivos en la opción `FILENAME`: `.mdf` se usa para archivos de datos principales, `.ndf` para archivos de datos secundarios y `.ldf` para archivos de registro de transacciones. En este ejemplo se coloca la base de datos en la unidad `D:`, en lugar de con la base de datos `master`.  
  
```sql  
USE master;  
GO  
CREATE DATABASE Archive   
ON  
PRIMARY    
    (NAME = Arch1,  
    FILENAME = 'D:\SalesData\archdat1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch2,  
    FILENAME = 'D:\SalesData\archdat2.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch3,  
    FILENAME = 'D:\SalesData\archdat3.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20)  
LOG ON   
   (NAME = Archlog1,  
    FILENAME = 'D:\SalesData\archlog1.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
   (NAME = Archlog2,  
    FILENAME = 'D:\SalesData\archlog2.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20) ;  
GO  
```  
  
### <a name="d-creating-a-database-that-has-filegroups"></a>D. Crear una base de datos que tenga grupos de archivos  
 En el ejemplo siguiente se crea la base de datos `Sales`, que tiene los siguientes grupos de archivos:  
  
-   El grupo de archivos principal, con los archivos `Spri1_dat` y `Spri2_dat`. El incremento de FILEGROWTH para estos archivos se especifica como `15%`.  
  
-   Un grupo de archivos denominado `SalesGroup1`, con los archivos `SGrp1Fi1` y `SGrp1Fi2`.  
  
-   Un grupo de archivos denominado `SalesGroup2`, con los archivos `SGrp2Fi1` y `SGrp2Fi2`.  
  
 En este ejemplo se colocan los archivos de datos y de registro en discos diferentes para mejorar el rendimiento.  
  
```sql  
USE master;  
GO  
CREATE DATABASE Sales  
ON PRIMARY  
( NAME = SPri1_dat,  
    FILENAME = 'D:\SalesData\SPri1dat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
( NAME = SPri2_dat,  
    FILENAME = 'D:\SalesData\SPri2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
FILEGROUP SalesGroup1  
( NAME = SGrp1Fi1_dat,  
    FILENAME = 'D:\SalesData\SG1Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp1Fi2_dat,  
    FILENAME = 'D:\SalesData\SG1Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
FILEGROUP SalesGroup2  
( NAME = SGrp2Fi1_dat,  
    FILENAME = 'D:\SalesData\SG2Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp2Fi2_dat,  
    FILENAME = 'D:\SalesData\SG2Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'E:\SalesLog\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="e-attaching-a-database"></a>E. Adjuntar una base de datos  
 En el ejemplo siguiente se separa la base de datos `Archive` creada en el ejemplo D y, a continuación, se adjunta mediante la cláusula `FOR ATTACH`. `Archive` se ha definido para contener varios archivos de datos y de registro. Sin embargo, dado que la ubicación de los archivos no ha cambiado desde que se crearon, solo es necesario especificar el archivo principal en la cláusula `FOR ATTACH`. A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], los archivos de texto completo que formen parte de la base de datos que se va a adjuntar se adjuntarán con la base de datos.  
  
```sql  
USE master;  
GO  
sp_detach_db Archive;  
GO  
CREATE DATABASE Archive  
      ON (FILENAME = 'D:\SalesData\archdat1.mdf')   
      FOR ATTACH ;  
GO  
```  
  
### <a name="f-creating-a-database-snapshot"></a>F. Crear una instantánea de base de datos  
 En el ejemplo siguiente se crea la instantánea de base de datos `sales_snapshot0600`. Debido a que la instantánea de base de datos es de solo lectura, no se puede especificar un archivo de registro. De acuerdo con la sintaxis, se especifican todos los archivos de la base de datos de origen, pero los grupos de archivos no se especifican.  
  
 La base de datos de origen en este ejemplo es la base de datos `Sales` creada en el ejemplo D.  
  
```sql  
USE master;  
GO  
CREATE DATABASE sales_snapshot0600 ON  
    ( NAME = SPri1_dat, FILENAME = 'D:\SalesData\SPri1dat_0600.ss'),  
    ( NAME = SPri2_dat, FILENAME = 'D:\SalesData\SPri2dt_0600.ss'),  
    ( NAME = SGrp1Fi1_dat, FILENAME = 'D:\SalesData\SG1Fi1dt_0600.ss'),  
    ( NAME = SGrp1Fi2_dat, FILENAME = 'D:\SalesData\SG1Fi2dt_0600.ss'),  
    ( NAME = SGrp2Fi1_dat, FILENAME = 'D:\SalesData\SG2Fi1dt_0600.ss'),  
    ( NAME = SGrp2Fi2_dat, FILENAME = 'D:\SalesData\SG2Fi2dt_0600.ss')  
AS SNAPSHOT OF Sales ;  
GO  
```  
  
### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. Crear una base de datos y especificar un nombre de intercalación y sus opciones  
 En el ejemplo siguiente se crea la base de datos `MyOptionsTest`. Se especifica un nombre de intercalación y las opciones `TRUSTYWORTHY` y `DB_CHAINING` se establecen en `ON`.  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE French_CI_AI  
WITH TRUSTWORTHY ON, DB_CHAINING ON;  
GO  
--Verifying collation and option settings.  
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>H. Adjuntar un catálogo de texto completo que se ha movido  
 En el ejemplo siguiente se adjunta el catálogo de texto completo `AdvWksFtCat` junto con los archivos de datos y de registro de `AdventureWorks2012`. En el ejemplo, el catálogo de texto completo se mueve desde su ubicación predeterminada hasta una nueva ubicación `c:\myFTCatalogs`. Los archivos de datos y de registro permanecen en sus ubicaciones predeterminadas.  
  
```sql  
USE master;  
GO  
--Detach the AdventureWorks2012 database  
sp_detach_db AdventureWorks2012;  
GO  
-- Physically move the full text catalog to the new location.  
--Attach the AdventureWorks2012 database and specify the new location of the full-text catalog.  
CREATE DATABASE AdventureWorks2012 ON   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_data.mdf'),   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf'),  
    (FILENAME = 'c:\myFTCatalogs\AdvWksFtCat')  
FOR ATTACH;  
GO  
```  
  
### <a name="i-creating-a-database-that-specifies-a-row-filegroup-and-two-filestream-filegroups"></a>I. Crear una base de datos que especifique un grupo de archivos de filas y dos grupos de archivos FILESTREAM  
 En el ejemplo siguiente se crea la base de datos `FileStreamDB`. La base de datos se crea con un grupo de archivos de filas y dos grupos de archivos FILESTREAM. Cada grupo de archivos contiene un archivo:  
  
-   `FileStreamDB_data` contiene los datos de fila. Contiene un archivo, `FileStreamDB_data.mdf` con la ruta de acceso predeterminada.  
  
-   `FileStreamPhotos` contiene los datos FILESTREAM. Contiene dos contenedores de datos FILESTREAM: `FSPhotos`, que se encuentra en `C:\MyFSfolder\Photos`, y `FSPhotos2`, que se encuentra en `D:\MyFSfolder\Photos`. Se marca como el grupo de archivos FILESTREAM predeterminado.  
  
-   `FileStreamResumes` contiene los datos FILESTREAM. Contiene un contenedor de datos FILESTREAM, `FSResumes`, que se encuentra en `C:\MyFSfolder\Resumes`.  
  
```sql  
USE master;  
GO  
-- Get the SQL Server data path.  
DECLARE @data_path nvarchar(256);  
SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)  
                  FROM master.sys.master_files  
                  WHERE database_id = 1 AND file_id = 1);  
  
 -- Execute the CREATE DATABASE statement.   
EXECUTE ('CREATE DATABASE FileStreamDB  
ON PRIMARY   
    (  
    NAME = FileStreamDB_data   
    ,FILENAME = ''' + @data_path + 'FileStreamDB_data.mdf''  
    ,SIZE = 10MB  
    ,MAXSIZE = 50MB  
    ,FILEGROWTH = 15%  
    ),  
FILEGROUP FileStreamPhotos CONTAINS FILESTREAM DEFAULT  
    (  
    NAME = FSPhotos  
    ,FILENAME = ''C:\MyFSfolder\Photos''  
-- SIZE and FILEGROWTH should not be specified here.  
-- If they are specified an error will be raised.  
, MAXSIZE = 5000 MB  
    ),  
    (  
      NAME = FSPhotos2  
      , FILENAME = ''D:\MyFSfolder\Photos''  
      , MAXSIZE = 10000 MB  
     ),  
FILEGROUP FileStreamResumes CONTAINS FILESTREAM  
    (  
    NAME = FileStreamResumes  
    ,FILENAME = ''C:\MyFSfolder\Resumes''  
    )   
LOG ON  
    (  
    NAME = FileStream_log  
    ,FILENAME = ''' + @data_path + 'FileStreamDB_log.ldf''  
    ,SIZE = 5MB  
    ,MAXSIZE = 25MB  
    ,FILEGROWTH = 5MB  
    )'  
);  
GO  
```  
  
### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>J. Crear una base de datos que tenga un grupo de archivos FILESTREAM con varias filas  
 En el ejemplo siguiente se crea la base de datos `BlobStore1`. La base de datos se crea con un grupo de archivos de filas y un grupo de archivos FILESTREAM, `FS`. El grupo de archivos FILESTREAM contiene dos archivos, `FS1` y `FS2`. Después, la base de datos se altera agregando un tercer archivo, `FS3`, al grupo de archivos FILESTREAM.  
  
```sql  
USE master;  
GO  
  
CREATE DATABASE [BlobStore1]  
CONTAINMENT = NONE  
ON PRIMARY   
(   
    NAME = N'BlobStore1',   
    FILENAME = N'C:\BlobStore\BlobStore1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = UNLIMITED,  
    FILEGROWTH = 1MB  
),   
FILEGROUP [FS] CONTAINS FILESTREAM DEFAULT   
(  
    NAME = N'FS1',  
    FILENAME = N'C:\BlobStore\FS1',  
    MAXSIZE = UNLIMITED  
),   
(  
    NAME = N'FS2',  
    FILENAME = N'C:\BlobStore\FS2',  
    MAXSIZE = 100MB  
)  
LOG ON   
(  
    NAME = N'BlobStore1_log',  
    FILENAME = N'C:\BlobStore\BlobStore1_log.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 1GB,  
    FILEGROWTH = 1MB  
);  
GO  
  
ALTER DATABASE [BlobStore1]  
ADD FILE  
(  
    NAME = N'FS3',  
    FILENAME = N'C:\BlobStore\FS3',  
    MAXSIZE = 100MB  
)  
TO FILEGROUP [FS];  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [Instantáneas de bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [Mover archivos de base de datos](../../relational-databases/databases/move-database-files.md)   
 [Bases de datos](../../relational-databases/databases/databases.md)   
 [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  

